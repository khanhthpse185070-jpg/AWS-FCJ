---
title : "Xây dựng lớp phân tích riêng tư"

weight : 4 
chapter : false
pre : " <b> 5.4. </b> "
---

## 5.4.1 Tiếp cận Phân tích Tối thiểu (phù hợp với phạm vi/chi phí)

- **Nguồn dữ liệu đáng tin cậy (Source of truth)**: Nhật ký API có cấu trúc của CloudWatch (các sự kiện và số liệu yêu cầu)

- **Lưu trữ**: Giữ nhật ký trong CloudWatch với thời gian lưu giữ hợp lý (ví dụ: 30–90 ngày).

- **Đường dẫn Xuất (Export path)**: Kích hoạt xuất từ CloudWatch → S3 để phân tích ad-hoc (theo nhu cầu) khi cần.

- **Truy vấn**: Sử dụng CloudWatch Log Insights để xem nhanh; sử dụng Athena trên các nhật ký S3 đã xuất để phân tích sâu hơn.

Phương pháp này tránh một Kho dữ liệu (DWH) riêng biệt mà vẫn cung cấp khả năng hiển thị về hành vi và độ tin cậy.

## 5.4.2 ETL nhẹ tùy chọn (nếu cần)

- Thiết lập một tác vụ xuất (hàng ngày) từ CloudWatch Logs sang một S3 bucket (`logs/<yyyy>/<mm>/<dd>/`)
- Trong Athena, tạo một bảng ngoài (external table) dựa trên JSON đã xuất; phân vùng theo ngày.

- Tạo một `events` (view) events duy nhất với các trường chính: `eventName`, `userId`, `sessionId`, `productId`, `statusCode`, `latencyMs`, `timestamp`.

- Giữ chi phí thấp bằng cách:
    - Nén dữ liệu xuất (GZIP).

    - Bỏ các trường nhiễu có tính đa dạng cao (high-cardinality noise fields).

    - Hạn chế thời gian lưu giữ trong S3 (vòng đời sang Glacier/hết hạn sau X ngày).
    
## 5.4.3 Bảo mật và Quyền truy cập 

- **Không có điểm cuối phân tích công khai (No public analytics endpoints)**: dữ liệu xuất vẫn nằm trong một S3 bucket riêng tư.

- **Quyền hạn IAM tối thiểu** (IAM least privilege):

    - Vai trò instance API: Quyền đọc Secrets Manager, quyền ghi CloudWatch logs, quyền S3 put cho dữ liệu xuất (nếu được sử dụng).
    
    - CloudFront chỉ đọc từ bucket hình ảnh; các lượt tải lên vẫn riêng tư thông qua presigned PUT.
    
- **Bí mật (Secrets)**: Mật khẩu DB + tên bucket được lưu trữ trong Secrets Manager; xoay vòng thông qua runbook.

- **Mã hóa (Encryption)**: HTTPS ở mọi nơi; S3 bucket được bật mã hóa; bucket xuất riêng tư.

## 5.4.4 Kiểm tra Vận hành (Operational checks)

- Báo động (Alarms) về tỷ lệ mã lỗi 5xx của API, độ trễ p95, lỗi xác thực.

- Xác thực định kỳ:

    - Các tác vụ xuất CloudWatch thành công (nếu được bật).
    
    - Xác minh JWT của Cognito vẫn vượt qua sau các thay đổi cấu hình.
    
    - Quyền tải lên được ký trước vẫn được giới hạn phạm vi (content-type, tiền tố key).
    
## 5.4.5 Mở rộng trong Tương lai (ngoài phạm vi hiện tại)

- Giới thiệu một bản sao đọc RDS nhỏ (small RDS read-replica) hoặc một DB phân tích chuyên dụng nếu các truy vấn tăng lên.

- Thêm Lambda transform để chuẩn hóa các sự kiện vào một bảng events (batch hàng ngày).

- Thêm công cụ BI (Business Intelligence) như QuickSight trên Athena hoặc DB phân tích để có dashboard phong phú hơn.



