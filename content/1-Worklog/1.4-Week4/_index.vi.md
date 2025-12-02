---
title: "Worklog Tuần 4"
 
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 4:

* Triển khai và tích hợp an toàn các cơ sở dữ liệu quan hệ (RDS) và NoSQL (DynamoDB).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Thiết lập VPC 2-Tầng (Public/Private Subnets, IGW, Bảng định tuyến).                                                                                           | 27/09/2025   | 29/09/2025      | <https://cloudjourney.awsstudygroup.com/>|
| 3   | - Triển khai NAT Gateway/Instance để cấp Internet cho Private Subnet.                                            | 28/09/2025   | 30/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Hiểu và áp dụng Nhóm bảo mật (Security Group) và ACL mạng (NACL).  | 30/09/2025   | 01/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Cấu hình S3 Bucket cho lưu trữ Trang web Tĩnh (Static Website Hosting).                  | 01/10/2025   | 02/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Thực hành quản lý Lớp lưu trữ S3 (Storage Classes) và Chính sách vòng đời (Lifecycle Policies).                                                                                         | 02/10/2025   | 03/10/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 4:

* Triển khai quan hệ An toàn: Triển khai thành công một phiên bản Amazon RDS được quản lý hoàn toàn:

    * Triển khai cơ sở dữ liệu vào Private Subnet, đảm bảo cách ly.

    * Quyền truy cập được kiểm soát nghiêm ngặt thông qua Nhóm bảo mật chuyên dụng, chỉ cho phép kết nối từ Tầng Ứng dụng EC2.

* Thành thạo NoSQL: Nắm vững sự khác biệt chính giữa các mô hình quan hệ và NoSQL:

    * Tạo một bảng DynamoDB có khả năng mở rộng, được tối ưu hóa bằng Partition/Sort Keys.

    * Thực hiện các thao tác CRUD cơ bản bằng cả AWS Console và CLI/SDK.

* Nguyên tắc nâng cao Hiệu suất:

    * Có kiến thức lý thuyết về các dịch vụ bộ nhớ đệm trong bộ nhớ như Amazon ElastiCache (Redis/Memcached).

    * Hiểu vai trò kiến trúc của nó trong việc giảm tải cơ sở dữ liệu và cải thiện độ trễ ứng dụng.