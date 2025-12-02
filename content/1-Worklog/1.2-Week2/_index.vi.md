---
title: "Worklog Tuần 2"
 
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 2:

* Triển khai VPC đa tầng an toàn và nắm vững các tính năng lưu trữ S3 nâng cao.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Thiết lập VPC 2-Tầng (Public/Private Subnets, IGW, Bảng định tuyến).                                                                                    | 15/09/2025   | 17/09/2025      | <https://cloudjourney.awsstudygroup.com/>|
| 3   | - Triển khai NAT Gateway/Instance để cấp Internet cho Private Subnet.                                            | 16/09/2025   | 18/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Hiểu và áp dụng Nhóm bảo mật (Security Group) và ACL mạng (NACL). | 16/09/2025   | 18/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Cấu hình S3 Bucket cho lưu trữ Trang web Tĩnh (Static Website Hosting).                  | 17/09/2025   | 19/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Thực hành quản lý Lớp lưu trữ S3 (Storage Classes) và Chính sách vòng đời (Lifecycle Policies).                                                                                         | 17/09/2025   | 19/09/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 2:

* Triển khai mạng Nâng cao: Thiết kế và triển khai một kiến trúc VPC 2-Tầng mạnh mẽ, xác nhận các khái niệm mạng cơ bản:
    * Thiết lập các Subnet Public và Private riêng biệt trên hai Vùng sẵn sàng (AZ) để có khả năng phục hồi cao.

    * Cấu hình NAT Gateway an toàn để kiểm soát truy cập Internet đi ra từ Private Subnets.

* Thực hiện kiểm soát Bảo mật: Hiểu sự khác biệt giữa và triển khai thành công Security Groups và Network ACLs. 

* Cấu hình lưu trữ Doanh nghiệp: Nắm vững và cấu hình Amazon S3 cho các trường hợp sử dụng nâng cao:
    * Thiết lập Chính sách Bucket và bật Tính năng lưu trữ Trang web Tĩnh.

    * Triển khai Chính sách Vòng đời (Lifecycle Policy) toàn diện để tự động chuyển đổi dữ liệu sang các tầng chi phí thấp hơn