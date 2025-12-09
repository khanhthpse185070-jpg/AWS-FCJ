---
title : "Hướng dẫn kiến trúc"

weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

![Architecture](/images/5-Workshop/architecture.png)
<p align="center"><em>Figure: AWS Jewelry Web deployment (adapted from workshop layout).</em></p>

---

## 5.2.1 Người dùng & Frontend (Giao diện người dùng)
- **Trình duyệt**: Khách hàng xem danh mục, chi tiết sản phẩm, giỏ hàng, thanh toán.

- **CloudFront + S3 (Lưu trữ tĩnh)**: Bản dựng React được phục vụ trên toàn cầu với ACM TLS (Bảo mật lớp truyền tải); Route 53 ánh xạ tên miền. CloudFront có quyền truy cập nguồn gốc (origin access) vào S3.

- **Cognito**: User Pool cấp JWTs (JSON Web Tokens) cho việc đăng ký/đăng nhập; React sử dụng token để gọi API.Tầm quan trọng: Phân phối nhanh chóng toàn cầu (mục tiêu $<2s$), SSL tiêu chuẩn, và token xác thực cho các cuộc gọi API được bảo vệ.

## 5.2.2 API & Dữ liệu

- **API Lightsail (.NET)**: Các hoạt động CRUD (Tạo, Đọc, Cập nhật, Xóa) cho sản phẩm, giỏ hàng và điều phối việc tải lên hình ảnh. Chạy với vai trò IAM role có quyền đọc Secrets Manager.

- **Lightsail DB (MySQL/Postgres)**: Lưu trữ danh mục, người dùng, giỏ hàng/đơn hàng. Riêng tư (Private) với instance API.

- **Secrets Manager**: Giữ mật khẩu DB và tên bucket (DB_PASSWORD, APP_CONFIG). API truy xuất khi khởi động/lần sử dụng đầu tiên.

- **CloudWatch Logs**: Ghi lại nhật ký truy cập/lỗi của API; là cơ sở cho các truy vấn hoạt động và phân tích nhẹ.

- **S3 (Media bucket)**: Bucket riêng tư cho hình ảnh sản phẩm. Quy trình tải lên sử dụng URL được ký trước (presigned URLs) từ API; CloudFront đọc hình ảnh.

Điểm nổi bật về Bảo mật: HTTPS ở mọi nơi, quyền truy cập từ CloudFront đến S3 được kiểm soát, thông tin xác thực DB không bao giờ được mã hóa cứng, IAM quyền hạn tối thiểu trên vai trò API.

## 5.2.3 Danh tính & Quyền truy cập

- **Amazon Cognito**: Đăng ký/đăng nhập, cấp token; API xác thực JWT cho các tuyến đường được bảo vệ.

- **Route 53 + ACM**: Tên miền + chứng chỉ TLS cho CloudFront; tùy chọn tên miền tùy chỉnh cho API nếu được hiển thị.

- **IAM**: Vai trò instance API được giới hạn ở Secrets Manager + CloudWatch; chính sách bucket S3 cấp quyền đọc cho CloudFront; tải lên chỉ thông qua PUT được ký trước (presigned PUT).

## 5.2.4 Hoạt động & Khả năng quan sát

- **CloudWatch**: Nhật ký/số liệu API, cảnh báo cho tỷ lệ lỗi/độ trễ.

- **Sao lưu/DR (Phục hồi sau thảm họa – phiên bản nhẹ)**: Ảnh chụp nhanh DB qua lịch trình Lightsail; S3 versioning (lập phiên bản S3) là tùy chọn.

- **Tình hình Chi phí**: Lightsail cho chi phí hàng tháng dự đoán được; S3/CF/Cognito/SM/CW tối thiểu ở mức lưu lượng truy cập đã nêu.

## 5.2.5 Các Giai đoạn Triển khai (6–12 tuần kể từ đề xuất)

- **Đánh giá (Tuần 1)**: Yêu cầu, sơ đồ kiến trúc , lược đồ DB, danh sách bí mật.

- **Cơ sở hạ tầng cơ bản (Tuần 2)**: Lưu trữ S3, CloudFront+ACM, Route 53, Lightsail API/DB, thiết lập Cognito, các mục Secrets Manager, ghi nhật ký CloudWatch.

- **Backend (Tuần 3)**: Truy xuất bí mật, tải lên được ký trước, CRUD, xác minh token Cognito, nhật ký CloudWatch.

- **Frontend (Tuần 4)**: Giao diện người dùng cửa hàng React, giao diện đăng nhập Cognito, giao diện tải lên, tích hợp API, triển khai lên S3+CF.

- **Thử nghiệm & Go-live (Tuần 5)**: Tích hợp FE↔API↔S3↔DB, kiểm tra bảo mật (IAM/SM), thử nghiệm E2E (Đầu cuối).

- **Bàn giao (Tuần 6)**: Runbook cập nhật bí mật, chuyển giao quyền sở hữu, hướng dẫn vận hành.