---
title: "Worklog Tuần 6"
 
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 6:

* Xây dựng API serverless cơ bản bằng Lambda/API Gateway và sử dụng CDN (CloudFront) để phân phối nội dung.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | -  Triển khai một ứng dụng Web đơn giản trên Lightsail.                                                                                            | 12/10/2025   | 13/10/2025      |<https://cloudjourney.awsstudygroup.com/> |
| 3   | -  Viết hàm Lambda cơ bản và kích hoạt nó bằng một sự kiện (S3/SNS).                                           | 13/10/2025   | 14/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Cấu hình API Gateway (REST API) tích hợp với Lambda. | 14/10/2025   | 15/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Cấu hình CloudFront để tăng tốc và bảo vệ Trang web Tĩnh S3.                  | 15/10/2025   | 16/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Tìm hiểu về Route 53 (Các loại bản ghi, Chính sách định tuyến) và Lambda@Edge.                                                                                         | 16/10/2025   | 17/10/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 6:
* Tạo API Serverless: Triển khai thành công quy trình làm việc API Serverless cốt lõi:

  * Viết và triển khai một Hàm AWS Lambda .

  * Tích hợp hàm này với API Gateway để tạo một điểm cuối REST có thể truy cập công khai.

* Sự kiện phi tập trung: Chứng minh kiến thức về kiến trúc hướng sự kiện:

  * Cấu hình các hàm Lambda để được kích hoạt bởi nhiều nguồn sự kiện AWS khác nhau .

* Tăng tốc nội dung toàn cầu: Triển khai và cấu hình Amazon CloudFront dưới dạng Mạng phân phối nội dung (CDN):

  * Sử dụng CloudFront trước một nguồn gốc S3, cải thiện đáng kể hiệu suất phân phối tài sản.

  * Cung cấp khả năng bảo vệ DDoS cơ bản ở tầng vùng biên.

* Chuyên môn định tuyến tên miền: Đã có kinh nghiệm thực tế với Amazon Route 53:

  * Cấu hình các loại bản ghi khác nhau (A, CNAME).

  * Thử nghiệm các chính sách định tuyến nâng cao như định tuyến đơn giản, chuyển đổi dự phòng hoặc định tuyến dựa trên độ trễ.


