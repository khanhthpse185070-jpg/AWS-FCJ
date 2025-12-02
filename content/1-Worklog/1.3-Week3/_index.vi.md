---
title: "Worklog Tuần 3"
 
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 3:

* Bảo mật môi trường bằng chính sách Đặc quyền tối thiểu (IAM) và thiết lập giám sát chi phí.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Nắm vững IAM cốt lõi: Users, Groups, Roles, và cấu trúc Policy JSON.                                                                                            | 21/09/2025   | 22/09/2025      | <https://cloudjourney.awsstudygroup.com/>|
| 3   | - Áp dụng nguyên tắc Đặc quyền Tối thiểu (Least Privilege) qua Chính sách tùy chỉnh.                                            | 22/09/2025   | 23/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Tạo và gán IAM Role cho EC2 để truy cập S3 một cách an toàn. | 23/09/2025   | 24/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Thiết lập AWS Budgets để theo dõi và cảnh báo chi phí.                  | 24/09/2025   | 25/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Cấu hình Amazon SSO và MFA (Xác thực đa yếu tố) để bảo mật tài khoản.                                                                                         | 25/09/2025   | 26/09/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 3:

* Thiết kế Chính sách IAM: Đã có thể viết, kiểm tra và áp dụng các Chính sách IAM phức tạp:

   * Tạo các chính sách tùy chỉnh bằng cú pháp JSON để thực thi các quy tắc truy cập nghiêm ngặt, chi tiết.

   * Triển khai và xác minh thành công các chính sách tuân thủ Nguyên tắc Đặc quyền Tối thiểu (PoLP).

* Bảo mật giữa các Dịch vụ: Thiết lập giao tiếp an toàn giữa các dịch vụ:

   * Cấu hình IAM Role và gắn nó vào một phiên bản EC2.

* Quản trị chi phí Chủ động: Thiết lập và cấu hình AWS Budgets để kiểm soát chi tiêu dịch vụ:

    * Thiết lập ngân sách với các ngưỡng cụ thể và cơ chế cảnh báo (qua SNS).

    * Đảm bảo tuân thủ các hướng dẫn quản lý chi phí.
