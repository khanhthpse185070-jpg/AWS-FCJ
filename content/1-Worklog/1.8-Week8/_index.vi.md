---
title: "Worklog Tuần 8"
 
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 8:

* Tự động hóa triển khai cơ sở hạ tầng bằng CloudFormation
* Triển khai giám sát CloudWatch toàn diện

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Học về CloudWatch Metrics, Logs, Alarms.                                                                                             | 25/10/2025   | 26/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Thiết lập Bảng điều khiển (Dashboard) và Cảnh báo (Alarms) CloudWatch cho các dịch vụ chính.                                            | 26/10/2025   | 27/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Học về AWS CloudFormation và cấu trúc Template. | 27/10/2025   | 28/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Viết CloudFormation Template để triển khai phiên bản EC2.                  | 28/10/2025   | 29/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Viết CloudFormation Template cho VPC và sử dụng Parameters/Outputs.                                                                                         | 29/10/2025   | 30/10/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 8:

* Tự động hóa Cơ sở hạ tầng: Chứng minh sự thành thạo trong Cơ sở hạ tầng dưới dạng Mã (IaC) bằng cách tạo các template AWS CloudFormation (CFN) phức tạp:

  * Tạo một stack triển khai thành công toàn bộ môi trường mạng (VPC, Subnets, IGW, v.v.).

* Khả năng tái sử dụng Template: Áp dụng các phương pháp hay nhất để làm cho template CFN trở nên động:

  * Sử dụng Parameters để chấp nhận các giá trị đầu vào tùy chỉnh.

  * Sử dụng Outputs để cho phép các stack xuất dữ liệu để các stack phụ thuộc khác sử dụng.

* Quan sát nâng cao: Triển khai giải pháp giám sát mạnh mẽ bằng Amazon CloudWatch:

  * Thiết lập các số liệu tùy chỉnh và các nhóm nhật ký tập trung cho nhật ký ứng dụng (CloudWatch Logs).

  * Xác định Cảnh báo (Alarms) với các hành động thông báo cụ thể (qua SNS) cho các sự kiện hệ thống quan trọng.


