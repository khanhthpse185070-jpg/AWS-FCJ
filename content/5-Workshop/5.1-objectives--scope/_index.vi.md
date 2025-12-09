---
title : "Mục tiêu và Phạm vi"
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

### Bối cảnh Doanh nghiệp
Dự án AWS Jewelry Web cung cấp một trang web thương mại điện tử trang sức với các thành phần sau:

- SPA React (Ứng dụng trang đơn) được lưu trữ trên **S3 + CloudFront** (HTTPS được quản lý bởi ACM, tên miền Route 53).

- API **.NET** trên **AWS Lightsail** phục vụ các hoạt động về sản phẩm/danh mục/giỏ hàng.

- **Lightsail MySQL/Postgres** cho dữ liệu giao dịch.

- **Amazon Cognito** cho việc đăng ký/đăng nhập và ủy quyền API.

- **Amazon S3** để lưu trữ hình ảnh sản phẩm thông qua tải lên bằng URL được ký trước (presigned uploads).

- **CloudWatch** để ghi nhật ký API và **Secrets Manager** cho mật khẩu DB + cấu hình bucket.

Giả định lưu lượng truy cập: <100 nghìn yêu cầu/tháng, không yêu cầu tự động mở rộng nâng cao. Trọng tâm là độ tin cậy, xử lý phương tiện truyền thông an toàn, và phân phối nhanh chóng trên toàn cầu.

### Mục tiêu (Kết quả Workshop)

- **Rõ ràng về Kiến trúc**: Giải thích cách S3+CloudFront, Lightsail API/DB, Cognito và Secrets Manager kết hợp với nhau tạo thành một stack thương mại điện tử nhỏ nhưng an toàn.

- **Triển khai thực tế**: Dựng frontend được lưu trữ trên CDN, API liên kết với Secrets Manager, xác thực Cognito, tải lên hình ảnh an toàn lên S3 và ghi nhật ký đầu cuối trong CloudWatch.

- **Tiêu chí Thành công (theo đề xuất)**:

    - Thời gian tải trang <2 giây trên toàn cầu (CloudFront + S3).

    - API Lightsail ổn định dưới tải dự kiến.

    - Các hoạt động DB an toàn với các truy vấn nhanh.

    - Đăng ký/đăng nhập Cognito ổn định.

    - Tải lên hình ảnh an toàn vào S3.

    - Nhật ký API hiển thị trong CloudWatch.

### Phạm vi
- Các hoạt động CRUD danh mục cốt lõi, cơ bản về giỏ hàng.

- Xác thực dựa trên Cognito và xác minh token trên API.

- Tải lên S3 được ký trước cho hình ảnh sản phẩm.

- CDN + HTTPS qua CloudFront/ACM; ánh xạ tên miền Route 53.

- Ghi nhật ký/số liệu CloudWatch; Secrets Manager cho mật khẩu DB + tên bucket.

- Hướng dẫn dòng thời gian: 6–12 tuần từ đánh giá → cơ sở hạ tầng → backend → frontend → thử nghiệm → bàn giao.

### Ngoài Phạm vi (theo đề xuất)
- Các tính năng AI/ML, luồng thương mại điện tử nâng cao, xử lý hình ảnh phức tạp.

- Đa khu vực/DR (Phục hồi sau thảm họa), cổng thông tin quản trị phức tạp, tích hợp bên thứ ba.

- Tự động mở rộng nâng cao hoặc CI/CD tinh vi ngoài việc triển khai cơ bản.
