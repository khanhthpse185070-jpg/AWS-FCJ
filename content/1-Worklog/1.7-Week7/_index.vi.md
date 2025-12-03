---
title: "Worklog Tuần 7"
 
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 7:

* Đóng gói ứng dụng, triển khai trên ECS Fargate
* Sử dụng dịch vụ nhắn tin không đồng bộ (SNS/SQS).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Nắm vững Docker, viết Dockerfile và đẩy Image lên ECR.                                                                                             | 20/10/2025   | 21/10/2025      |<https://cloudjourney.awsstudygroup.com/> |
| 3   | - Triển khai ECS Cluster và Định nghĩa tác vụ (Task Definition - Fargate Launch Type).                                            | 21/10/2025   | 22/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Tạo Dịch vụ ECS (ECS Service) và tích hợp với ALB.  | 20/10/2025   | 22/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Cấu hình SNS (Simple Notification Service) và SQS (Simple Queue Service).                  | 23/10/2025   | 24/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Triển khai ứng dụng sử dụng ECS/Fargate.                                                                                         | 23/10/2025   | 24/10/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 7:

* Thành thạo quy trình Container: Phát triển một Dockerfile hoạt động, xây dựng một image ứng dụng tùy chỉnh và quản lý vòng đời container:

  * Đẩy image ứng dụng lên một kho lưu trữ Amazon Elastic Container Registry (ECR) riêng tư.

* Triển khai Container Serverless: Triển khai thành công ứng dụng được đóng gói bằng AWS ECS Fargate:

  * Loại bỏ nhu cầu quản lý các worker node EC2 cơ bản.

  * Tích hợp Dịch vụ ECS với ALB.

* Giao tiếp bất đồng bộ: Triển khai một thành phần quan trọng của kiến trúc microservices:

  * Cấu hình và sử dụng SQS (Simple Queue Service) để phân tách các thành phần ứng dụng.

  * Sử dụng SNS (Simple Notification Service) để nhắn tin fan-out tới nhiều người đăng ký.


