---
title: "Workshop"
 
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


# AWS Jewelry Web Workshop

![Architecture](/images/imageworkshop.png)
<p align="center"><em>Figure: Simplified AWS Jewelry Web architecture (CloudFront + S3, Lightsail API/DB, Cognito, Secrets, CloudWatch).</em></p>

### Tổng quan (Overview)

Tài liệu workshop này ghi lại dự án AWS Jewelry Web: một stack thương mại điện tử trang sức an toàn, ý thức về chi phí sử dụng các dịch vụ được quản lý của AWS.

- Frontend (Giao diện người dùng): React SPA trên S3 + CloudFront với TLS của ACM và tên miền Route 53.

- Backend (Hệ thống phụ trợ): Instance Lightsail chạy API .NET; Lightsail MySQL/Postgres cho dữ liệu.

- Danh tính (Identity): Amazon Cognito User Pool cho đăng ký/đăng nhập và xác minh JWT trên API.

- Media: S3 bucket riêng tư cho hình ảnh sản phẩm; tải lên thông qua presigned PUT (lệnh PUT được ký trước); CloudFront đọc các đối tượng.

- Bí mật & Khả năng Quan sát: AWS Secrets Manager cho mật khẩu DB và cấu hình bucket; CloudWatch Logs cho nhật ký API/sự kiện nghiệp vụ.

Mục tiêu thiết kế:

- Thời gian tải trang <2 giây trên toàn cầu qua CloudFront.

- API ổn định dưới lưu lượng truy cập dự kiến (dưới 100 nghìn yêu cầu/tháng).

- Các hoạt động DB an toàn; không mã hóa cứng bí mật (chỉ sử dụng Secrets Manager).

- Tải lên an toàn; ghi nhật ký API hoàn chỉnh cho vận hành và phân tích cơ bản.

### Bản đồ Nội dung (Content Map)

**[5.1. Mục tiêu và phạm vi](5.1-objectives--scope/)**

**[5.2. Hướng dẫn kiến trúc](5.2-Architecture-Walkthrough/)**

**[5.3. Thực hiện-Thu thập-Dữ liệu Clickstream](5.3-Implementing-Clickstream-Ingestion/)**

**[5.4. Xây dựng Lớp Phân tích Riêng tư](5.4-Building-the-Private-Analytics-Layer/)**

**[5.5. Trực quan hóa Phân tích bằng Shiny Dashboards](5.5-Visualizing-Analytics-with-Shiny-Dashboards/)**

**[5.6. Tóm tắt & Dọn dẹp](5.6-Summary-&-Clean-up/)**
