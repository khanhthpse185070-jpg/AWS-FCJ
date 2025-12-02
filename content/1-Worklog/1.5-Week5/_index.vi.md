---
title: "Worklog Tuần 5"
 
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 5:

* Kết nối, làm quen với các thành viên trong First Cloud Journey.
* Hiểu dịch vụ AWS cơ bản, cách dùng console & CLI.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Cấu hình Bộ cân bằng tải ứng dụng (ALB) và Nhóm đích (Target Group).                                                                                             | 05/10/2025   | 07/10/2025      |<https://cloudjourney.awsstudygroup.com/> |
| 3   | - Tạo Mẫu khởi chạy (Launch Template) cho EC2 và thiết lập Nhóm tự động mở rộng (ASG).                                           | 06/10/2025   | 08/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Triển khai kiến trúc HA/ASG Đa-AZ (Multi-AZ) gắn vào ALB. | 06/10/2025   | 08/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Cấu hình Chính sách mở rộng (Scaling Policy) dựa trên mức sử dụng CPU và thực hiện Kiểm tra tải.                  | 08/10/2025   | 09/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | -  Hoàn thành Lab tổng hợp về kiến trúc Ứng dụng Web chịu lỗi.                                                                                        | 08/10/2025   | 10/10/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 5:

* Kiến trúc chịu lỗi: Thiết kế và triển khai một kiến trúc Tính sẵn sàng cao (HA) thực sự:

  * Trải rộng thành công kiến trúc trên nhiều Vùng sẵn sàng (AZ) để có khả năng phục hồi.

* Cân bằng Tải Nâng cao: Đã cấu hình Bộ cân bằng tải ứng dụng (ALB):

  * Thiết lập Listeners (HTTP/HTTPS) và tạo Nhóm đích (Target Groups).

  * Triển khai cấu hình kiểm tra tình trạng chính xác để đảm bảo lưu lượng truy cập chỉ được định tuyến đến các phiên bản khỏe mạnh.

* Triển khai mở rộng động: Tạo một Nhóm Tự động Mở rộng (ASG) mạnh mẽ bằng cách sử dụng Mẫu Khởi chạy chi tiết:

  * Triển khai cả Chính sách Mở rộng Theo dõi Mục tiêu (Target Tracking Scaling Policies).

  * Xác thực thành công các sự kiện mở rộng ra và mở rộng vào tự động thông qua thử nghiệm tải có chủ đích.


