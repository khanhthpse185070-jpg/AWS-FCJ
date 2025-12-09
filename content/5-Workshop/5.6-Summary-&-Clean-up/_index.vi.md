---
title : " Tóm tắt và Dọn dẹp tài nguyên"

weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

## 5.6.1 Tóm tắt

Chúng tôi đã lập kế hoạch và xác định phạm vi dự án AWS Jewelry Web là một stack thương mại điện tử an toàn, ý thức về chi phí:

    - Frontend: React trên S3 + CloudFront với TLS của ACM và tên miền Route 53.
    
    - Backend: API .NET trên Lightsail; DB trên Lightsail (MySQL/Postgres); Secrets Manager cho mật khẩu DB/tên bucket.
    
    - Danh tính: Cognito User Pool cho đăng ký/đăng nhập và xác minh token API.
    
    - Media: S3 bucket riêng tư; tải lên thông qua presigned PUT; CloudFront đọc các đối tượng.
    
    - Khả năng quan sát: CloudWatch ghi nhật ký có cấu trúc cho API + các sự kiện nghiệp vụ; tùy chọn xuất sang S3/Athena để phân tích sâu hơn.
    
    Tiêu chí thành công: Tải trang $<2s$ qua CDN, API ổn định dưới lưu lượng dự kiến, hoạt động DB an toàn, xác thực Cognito ổn định, tải lên an toàn và ghi nhật ký API đầy đủ.
    
## 5.6.2 Các Điểm rút kinh nghiệm chính

- Giữ bí mật ngoài mã nguồn: Secrets Manager + IAM quyền hạn tối thiểu trên vai trò API.

- Hiệu suất từ biên: CloudFront + S3 + ACM; tối thiểu các bước nhảy backend cho nội dung tĩnh.

- Ưu tiên độ tin cậy: Ghi nhật ký mọi thứ có ý nghĩa (xác thực, tải lên, CRUD, sự kiện sản phẩm) và đặt cảnh báo về ngưỡng lỗi/độ trễ.

- Tập trung vào Chi phí: Lightsail cho chi tiêu có thể dự đoán được; điều chỉnh thời gian lưu giữ CloudWatch; phân tích tùy chọn chỉ khi cần.

## 5.6.3 Danh sách Kiểm tra Dọn dẹp (Clean-up Checklist)

- S3 + CloudFront: Hủy bỏ distribution và các đối tượng bucket nếu trang web ngừng hoạt động.

- Cognito: Xóa User Pool nếu không còn được sử dụng.

- Lightsail: Chụp nhanh (snapshot) hoặc chấm dứt (terminate) các instance API/DB; giải phóng các IP tĩnh.

- Secrets Manager: Xóa các bí mật `DB_PASSWORD` và `APP_CONFIG`

- CloudWatch: Xóa các nhóm nhật ký (log groups)/cảnh báo; vô hiệu hóa mọi tác vụ xuất dữ liệu.

- Route 53/ACM: Xóa các bản ghi/chứng chỉ không còn được sử dụng.