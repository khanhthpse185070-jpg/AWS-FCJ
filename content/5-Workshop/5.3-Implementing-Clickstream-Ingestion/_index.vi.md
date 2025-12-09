---
title : "Thực hiện-Thu thập-Dữ liệu Clickstream"

weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

## 5.3.1 Thu thập Dữ liệu (Ingestion) cho AWS Jewelry Web

Chúng tôi giữ cho quy trình thu thập dữ liệu nhẹ nhàng bằng cách sử dụng API Lightsail hiện có và nhật ký có cấu trúc của CloudWatch, thay vì một pipeline clickstream riêng biệt.

- Frontend React phát ra các sự kiện sản phẩm chính: `page_view`, `product_view`, `add_to_cart`, `checkout_start`, `checkout_complete`

- Các sự kiện được POST tới **API Lightsail**, API này xác thực và ghi chúng dưới dạng JSON có cấu trúc vào **CloudWatch Logs**.

- Việc tải lên hình ảnh sản phẩm được thực hiện thông qua **presigned URLs**  do API tạo; CloudFront đọc hình ảnh từ S3 bucket riêng tư.

Điều này đáp ứng nhu cầu quan sát (observability) trong khi vẫn nằm trong giới hạn về chi phí/phạm vi của dự án.

## 5.3.2 Lược đồ Sự kiện/Nhật ký 

- Danh tính (Identity): `userId` (nếu đã đăng nhập), `clientId`, `sessionId`, `userLoginState`, `identitySource`.

- Sự kiện (Event): `eventName`, `eventTimestamp`.

- Ngữ cảnh Sản phẩm (Product context):  `productId`, `name`, `category`, `brand`, `price`, `discountPrice`, `urlPath`.

Yêu cầu/Meta (Request/meta): `path`, `method`, `statusCode`, `latencyMs`, `userAgent`, `sourceIp`, `requestId`.

Lưu trữ dưới dạng JSON có cấu trúc trong CloudWatch để truy vấn/xuất sau này.

## 5.3.3 Trách nhiệm của API 

- `/events`: chấp nhận các payload sự kiện đã xác thực; từ chối các loại sự kiện không xác định.

- Tải lên được ký trước (Presigned uploads): cấp các URL PUT với các ràng buộc về content-type và key (khóa).

- Bí mật (Secrets): `DB_PASSWORD` and `APP_CONFIG` từ **Secrets Manager**; không mã hóa cứng bí mật.

- Ghi nhật ký (Logging): ghi các mục CloudWatch có cấu trúc cho trạng thái xác thực thành công/thất bại, các hoạt động CRUD, tải lên và các sự kiện nghiệp vụ.

## 5.3.4 Kết nối Frontend (Frontend Wiring)

- Sử dụng Cognito JWT cho các cuộc gọi đã xác thực; xử lý khách truy cập (guests) bằng cách tạo `clientId` + `sessionId`.

- Duy trì `clientId` (localStorage) và `sessionId` (sessionStorage) với thời gian chờ idle timeout.

- POST không chặn (non-blocking), fire-and-forget cho mỗi sự kiện; thử lại là tùy chọn nhưng không được chặn giao diện người dùng.

- Quy trình tải lên hình ảnh: yêu cầu URL được ký trước --> PUT file lên S3 --> gửi siêu dữ liệu/key trở lại API.

## 5.3.5 Danh sách Kiểm tra Xác thực 

1. Kích hoạt các sự kiện (duyệt, xem sản phẩm, thêm vào giỏ hàng, bắt đầu/hoàn tất thanh toán).

2. Xác nhận API trả về mã 2xx; xác minh việc tải lên S3 thành công qua URL được ký trước.

3. Trong CloudWatch Logs, xác minh các sự kiện có cấu trúc với các trường danh tính/sản phẩm.

4. Xác nhận việc đọc từ Secrets Manager (không có thông tin xác thực DB/bucket được mã hóa cứng).

5. Xác minh CORS + HTTPS đầu cuối; đảm bảo CloudFront có thể đọc bucket hình ảnh, việc tải lên là riêng tư.