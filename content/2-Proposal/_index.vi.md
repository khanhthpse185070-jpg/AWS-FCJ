---
title: "Bản đề xuất"
 
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

Tại phần này, bạn cần tóm tắt các nội dung trong workshop mà bạn **dự tính** sẽ làm.

# **Nền Tảng Thương Mại Điện Tử Trang Sức**  
## **Hệ Thống Bán Hàng Trực Tuyến Dựa Trên Cloud Sử Dụng React, .NET và MySQL trên AWS Lightsail**  

---

## **1. Tổng Quan Dự Án**

Nền Tảng Thương Mại Điện Tử Trang Sức là một hệ thống bán lẻ trực tuyến hiện đại được xây dựng trên cơ sở hạ tầng đám mây, được thiết kế dành cho các doanh nghiệp trang sức vừa và nhỏ. Dự án nhằm mục đích giúp các doanh nghiệp này chuyển đổi từ mô hình bán hàng truyền thống sang một môi trường kỹ thuật số an toàn, linh hoạt và tự động hóa.  

Nền tảng tích hợp giao diện front-end ReactJS, backend .NET Core được lưu trữ trên Amazon Lightsail, và cơ sở dữ liệu MySQL để quản lý sản phẩm, người dùng và đơn hàng một cách hiệu quả.  

Các tài nguyên tĩnh như hình ảnh sản phẩm và nội dung web được lưu trữ trên Amazon S3 và phân phối toàn cầu thông qua Amazon CloudFront, đảm bảo tốc độ và bảo mật tối ưu. Amazon Cognito xử lý xác thực người dùng, trong khi Amazon CloudWatch, AWS CloudTrail và Lightsail Snapshots cung cấp giám sát, kiểm toán và khôi phục thảm họa.  

Dự án này cung cấp một giải pháp thương mại điện tử tiết kiệm chi phí, dễ vận hành và có khả năng mở rộng được thiết kế riêng cho các doanh nghiệp trang sức vừa và nhỏ.  

### **Mục Tiêu Dự Án**
- Phát triển một trang web thương mại điện tử trang sức responsive, thân thiện với người dùng, hoạt động mượt mà trên mọi thiết bị.  
- Tập trung hóa quản lý sản phẩm, tồn kho và đơn hàng.  
- Đảm bảo thời gian hoạt động ≥99.9% thông qua sao lưu và phục hồi tự động.  
- Duy trì chi phí cơ sở hạ tầng dưới 65 USD/tháng bằng cách sử dụng Lightsail và tài nguyên AWS Free Tier.  

### **Giá Trị Kinh Doanh**
Các cửa hàng trang sức nhỏ thường gặp phải những thách thức liên quan đến chi phí cơ sở hạ tầng cao và kiến thức kỹ thuật hạn chế. Giải pháp này giúp:  
- Giảm chi phí vận hành với mức giá Lightsail có thể dự đoán được.  
- Tự động hóa các tác vụ lặp đi lặp lại, cải thiện hiệu quả.  
- Tăng cường niềm tin thương hiệu thông qua sự ổn định của hệ thống và bảo vệ dữ liệu mạnh mẽ.  

---

## **2. Phân Tích Vấn Đề**

### **2.1 Tình Hình Hiện Tại**

Thị trường bán lẻ trang sức đang nhanh chóng chuyển sang các kênh trực tuyến, được thúc đẩy bởi nhu cầu của người tiêu dùng về cá nhân hóa, minh bạch và trải nghiệm kỹ thuật số chất lượng cao — đặc biệt là ở thế hệ trẻ. Tuy nhiên, hầu hết các hệ thống thương mại điện tử hiện tại đều gặp phải những hạn chế nghiêm trọng:

- Trải nghiệm người dùng kém: Tải trang chậm, thiết kế lỗi thời và thiếu các tính năng tương tác như thử đeo AR.  
- Thiếu niềm tin: Khách hàng do dự mua các sản phẩm có giá trị cao (vàng, kim cương) do lo ngại về bảo mật dữ liệu và tính xác thực.  
- Cơ sở hạ tầng không an toàn, lỗi thời: Nhiều hệ thống cũ lưu trữ mật khẩu hoặc dữ liệu khách hàng dưới dạng văn bản thuần túy, khiến chúng dễ bị tấn công và hạn chế khả năng mở rộng.  

---

### **2.2 Những Thách Thức Chính**

- **Tốc độ và độ tin cậy:**  
  Trang sức phụ thuộc rất nhiều vào hình ảnh độ phân giải cao và nội dung tương tác (ví dụ: xem 360°, thử đeo AR). Không có CDN toàn cầu, việc tải nội dung như vậy trở nên chậm và không đáng tin cậy, dẫn đến tỷ lệ bỏ giỏ hàng cao.  

- **Rủi ro bảo mật và gian lận:**  
  Các nền tảng thương mại điện tử là mục tiêu chính cho các cuộc tấn công mạng. Không có Tường lửa Ứng dụng Web (WAF), hệ thống bị lộ với SQL injection, cross-site scripting và vi phạm dữ liệu. Lưu trữ thông tin đăng nhập trực tiếp trong mã gây ra rủi ro nghiêm trọng về truy cập trái phép.  

- **Vấn đề mất dữ liệu và khôi phục:**  
  Các giao dịch và hồ sơ tồn kho phải chính xác 100%. Lưu trữ cục bộ có nguy cơ mất dữ liệu vĩnh viễn nếu phần cứng gặp sự cố. Không có lưu trữ bền vững như Amazon S3, dữ liệu quan trọng như hóa đơn và hình ảnh sản phẩm có thể trở nên không thể khôi phục được.  

- **Giám sát và kiểm soát hạn chế:**  
  Không có các công cụ giám sát tập trung như CloudWatch, người vận hành chỉ có thể phát hiện sự cố sau khi khách hàng báo cáo, làm tăng MTTR (Thời gian Trung bình để Khôi phục) và làm tổn hại lòng tin của người dùng.  

---

### **2.3 Tác Động Đến Các Bên Liên Quan**

| **Bên liên quan** | **Tác động chính** |
|------------------|----------------|
| Khách hàng | Có được sự tự tin thông qua mua sắm trực tuyến nhanh chóng, minh bạch và an toàn. |
| Đội ngũ Vận hành | Giám sát hệ thống dễ dàng hơn, với các quy trình sao lưu và khôi phục tự động. |
| Lập trình viên | Phát triển nhanh hơn thông qua kiến trúc module với API Gateway và Lightsail. |
| Chủ doanh nghiệp | Hoạt động kinh doanh liên tục, giảm rủi ro mất dữ liệu và lợi thế cạnh tranh mạnh hơn. |

---

### **2.4 Hậu Quả Kinh Doanh**

- **Mất doanh thu:** Hiệu suất chậm và UX kém làm giảm tỷ lệ chuyển đổi và tăng tỷ lệ bỏ giỏ hàng.  
- **Rủi ro về danh tiếng và tuân thủ:** Vi phạm dữ liệu (do thiếu WAF hoặc Secrets Manager) có thể dẫn đến các hình phạt nặng và thiệt hại thương hiệu lâu dài — đặc biệt trong lĩnh vực hàng xa xỉ.  
- **Chi phí vận hành cao hơn:** Thiếu giám sát tự động và sao lưu làm tăng nhân lực và thời gian khôi phục.  
- **Khả năng mở rộng hạn chế:** Các hệ thống cũ không thích ứng được với tốc độ tăng trưởng thị trường nhanh, gây ra cơ hội kinh doanh bị bỏ lỡ.  

---

## **3. Kiến Trúc Giải Pháp**

![Sơ đồ kiến trúc](/images/image7.png)

### **3.1 Tổng Quan Kiến Trúc**
Kiến trúc đề xuất là một nền tảng thương mại điện tử hiệu suất cao được triển khai trên AWS Cloud (Khu vực Singapore) sử dụng thiết kế SPA/microservices tách biệt. Điều này cho phép xử lý động và khả năng mở rộng cao:

- **Phân Phối Frontend Tĩnh:** Các file frontend React (HTML, CSS, JS) được lưu trữ trên S3 và phục vụ qua CloudFront CDN để phân phối toàn cầu với độ trễ thấp.  
- **Xử Lý Backend Động:** Logic nghiệp vụ và dữ liệu (danh mục, giỏ hàng, đơn hàng) được xử lý thông qua API .NET được lưu trữ trên Lightsail, được hiển thị an toàn qua API Gateway.  

---

### **3.2 Các Dịch Vụ AWS Được Sử Dụng**

| **Danh mục** | **Dịch vụ AWS** | **Chức năng chính** |
|---------------|----------------|----------------------|
| Mạng & Edge | Route 53, CloudFront, WAF, ACM | Định tuyến DNS, phân phối CDN, bảo vệ web, quản lý SSL |
| Tính toán & API | API Gateway, Lightsail | Quản lý điểm cuối API và lưu trữ ứng dụng backend |
| Danh tính & Truy cập | Cognito, Secrets Manager | Xác thực/ủy quyền và quản lý thông tin đăng nhập an toàn |
| Lưu trữ & Cơ sở dữ liệu | S3, Lightsail MySQL | Lưu trữ tài sản tĩnh và cơ sở dữ liệu quan hệ cho dữ liệu giao dịch |
| Khả năng phục hồi & Sao lưu | AWS Backup, S3 Versioning, Glacier, Lightsail Snapshots | Sao lưu tự động, lưu trữ và kiểm soát phiên bản dữ liệu |
| Giám sát & Kiểm toán | CloudWatch, CloudTrail | Theo dõi hiệu suất thời gian thực và kiểm toán hoạt động API |

---

### **3.3 Thiết Kế Thành Phần**

- **Lớp Trình bày (Frontend):** Trang web React tĩnh được lưu trữ trên S3, phân phối qua CloudFront. AWS WAF cung cấp bảo vệ cấp edge khỏi các lỗ hổng phổ biến.  
- **Lớp Ứng dụng (Backend):** API Gateway xác thực token Cognito, quản lý yêu cầu API và thực thi throttling. Lightsail Instance (Ubuntu) chạy API .NET Core để xử lý logic nghiệp vụ (đơn hàng, sản phẩm, thanh toán).  
- **Lớp Dữ liệu:** Cơ sở dữ liệu MySQL trên Lightsail quản lý tất cả dữ liệu quan hệ; thông tin đăng nhập được lưu trữ an toàn trong Secrets Manager. Amazon S3 lưu trữ tải lên của người dùng, hình ảnh sản phẩm và các tài sản tĩnh khác.  

---

### **3.4 Kiến Trúc Bảo Mật**

- **Bảo vệ Edge:** WAF lọc các yêu cầu độc hại; ACM thực thi mã hóa HTTPS.  
- **Xác thực Người dùng:** Tất cả đăng nhập và đăng ký được xử lý bởi Cognito với xác thực token an toàn.  
- **Bảo mật Cơ sở hạ tầng:** Secrets Manager đảm bảo thông tin đăng nhập nhạy cảm không bao giờ được lưu trữ dưới dạng văn bản thuần túy.  
- **Kiểm toán:** CloudTrail ghi lại mọi lời gọi API để tuân thủ và truy xuất nguồn gốc.  

---

### **3.5 Khả Năng Mở Rộng và Khả Năng Quan Sát**

- Khả năng mở rộng toàn cầu thông qua bộ nhớ cache và phân phối CloudFront.  
- Tăng trưởng lưu trữ không giới hạn trên S3 cho các tài sản media.  
- Giám sát tài nguyên thông qua các chỉ số CloudWatch, cho phép các quyết định mở rộng chủ động.  

---

## **4. Kế Hoạch Triển Khai Kỹ Thuật**

| **Giai đoạn** | **Thời gian** | **Mục tiêu** | **Sản phẩm bàn giao** | **Tiêu chí thành công** |
|------------|---------------|-----------|------------------|----------------------|
| 1. Thiết lập Cơ sở hạ tầng | Tuần 1–2 | Cấu hình môi trường AWS | S3, CloudFront, Cognito, Route 53, SSL | Môi trường ổn định |
| 2. Phát triển Backend | Tuần 3–5 | Xây dựng API .NET & schema MySQL | Chức năng CRUD, cơ sở dữ liệu | Backend hoạt động |
| 3. Tích hợp Frontend | Tuần 6–7 | Kết nối React SPA với API | Đăng nhập, trang giao diện | Giao diện hoạt động |
| 4. Module Tải lên Hình ảnh | Tuần 8–9 | Kích hoạt tải lên S3 | Kiểm tra tải lên thành công | Đạt |
| 5. Giám sát & Sao lưu | Tuần 10–11 | Cấu hình CloudWatch & Snapshots | Cảnh báo và sao lưu tự động | Hệ thống ổn định |
| 6. Kiểm thử & Triển khai | Tuần 12–14 | QA và phát hành cuối cùng | Demo và tài liệu | Hệ thống hoàn chỉnh ổn định |

---

## **5. Lộ Trình & Các Cột Mốc Quan Trọng**

Dự án sẽ kéo dài 14 tuần (Tháng 9–Tháng 12 năm 2025), được chia thành sáu sprint Agile–Scrum.

| **Sprint** | **Sản phẩm bàn giao** | **Tiêu chí thành công** |
|-------------|-----------------|----------------------|
| Sprint 1 – Nền tảng | Thiết lập AWS (Lightsail, S3, CloudFront, Cognito, Route53) | Trang web React được phục vụ qua HTTPS; Kiểm tra đăng nhập Cognito thành công |
| Sprint 2 – Backend & DB | API .NET và schema MySQL | Các thao tác CRUD hoạt động chính xác |
| Sprint 3 – Frontend | Các trang React tích hợp với API | Hiển thị sản phẩm và giỏ hàng hoạt động |
| Sprint 4 – Media & Email | Thiết lập tải lên S3 + email SES | Phân phối hình ảnh qua CDN; email đơn hàng được gửi thành công |
| Sprint 5 – Thanh toán & Đặt hàng | Hoàn thành luồng đơn hàng | Thanh toán và xác nhận đơn hàng hoạt động |
| Sprint 6 – Kiểm thử & Giám sát | Hệ thống hoạt động đầy đủ | Nhật ký CloudWatch và sao lưu được xác minh |

---

## **6. Dự Toán Ngân Sách**

| **Dịch vụ** | **Mô tả** | **Chi phí Ước tính Hàng tháng (USD)** | **Ghi chú** |
|--------------|----------------|----------------------------------|------------|
| Lightsail Instance (API .NET) | 2–4 vCPU, 4–8 GB RAM | $10–$40 | Khuyến nghị gói ≥$20 |
| Cơ sở dữ liệu Lightsail MySQL | 20–50 GB DB được quản lý | $15–$50 | Nên tách riêng khỏi instance |
| Amazon S3 | Lưu trữ file tĩnh và hình ảnh | $1–$5 | Bao gồm phí yêu cầu |
| Amazon CloudFront | Phân phối CDN | $1–$30 | 1TB đầu tiên miễn phí/tháng |
| Route 53 + ACM | Domain và SSL | $1–$4 | ACM miễn phí; domain ~$12/năm |
| Amazon Cognito | Quản lý người dùng | $0–$10 | 10k người dùng đầu tiên miễn phí |
| Amazon SES | Thông báo email | $0.10–$5 | 62k email miễn phí nếu lưu trữ trên Lightsail |
| CloudWatch + CloudTrail | Giám sát và ghi nhật ký | $1–$10 | Phụ thuộc vào khối lượng nhật ký |
| Sao lưu | Snapshots và versioning | $1–$10 | Khuyến nghị sao lưu tự động hàng tuần |

**Tổng ước tính:** $30–$160/tháng (≈ $90–$480 cho 3 tháng)

---

### **Mẹo Tối Ưu Hóa Chi Phí**

1. Sử dụng AWS Free Tier cho Lightsail, S3, CloudFront, SES và Cognito.  
2. Triển khai tại ap-southeast-1 (Singapore) để có độ trễ tối thiểu.  
3. Áp dụng S3 Lifecycle Policies để chuyển file cũ sang Glacier Deep Archive.  
4. Kích hoạt cảnh báo thanh toán với AWS Cost Explorer và Budgets.  
5. Lên lịch snapshot hàng tuần và kích hoạt MFA Delete trên S3.  

---

## **7. Đánh Giá Rủi Ro**

| **ID Rủi ro** | **Mô tả** | **Mức độ nghiêm trọng** | **Tác động** |
|--------------|----------------|--------------|-------------|
| R1 | Lỗi Lightsail instance | Trung bình | Ngừng hoạt động tạm thời |
| R2 | Hỏng cơ sở dữ liệu | Cao | Mất dữ liệu giao dịch |
| R3 | Rò rỉ thông tin đăng nhập | Trung bình | Rủi ro truy cập trái phép |
| R4 | Quá tải do lưu lượng tăng đột biến | Trung bình | Trang web chậm hoặc không phản hồi |

---

### **7.1 Chiến Lược Giảm Thiểu**

- R1: Snapshot Lightsail hàng ngày và quy trình khôi phục chi tiết.  
- R2: Sao lưu DB tự động được xuất sang S3 để dự phòng.  
- R3: Bắt buộc sử dụng Secrets Manager với xoay vòng khóa.  
- R4: Tối ưu hóa bộ nhớ cache CloudFront và mở rộng Lightsail khi lưu lượng tăng đột biến.  

---

### **7.2 Kế Hoạch Dự Phòng**

- Khôi phục Hệ thống: Khôi phục instance từ snapshot mới nhất trong vòng 4 giờ.  
- Khôi phục Dữ liệu: Khôi phục sao lưu MySQL được lưu trữ trong S3.  
- Tính liên tục: Phục vụ trang bảo trì qua S3 + CloudFront trong thời gian ngừng hoạt động.  
- Sự cố Bảo mật: Xoay vòng khóa và điều tra với nhật ký CloudTrail.  

---

### **7.3 Kế Hoạch Giám Sát Rủi Ro**

- Giám sát Vận hành: Cảnh báo CloudWatch cho các ngưỡng CPU/mạng.  
- Đánh giá Bảo mật: Kiểm toán CloudTrail hàng tuần cho các hoạt động API bất thường.  
- Đánh giá Rủi ro Hàng quý: Đánh giá lại ma trận rủi ro sau các cập nhật lớn.  

---

## **8. Kết Quả Kỳ Vọng**

### **8.1 Chỉ Số Thành Công (KPIs)**

**KPIs Kỹ thuật**
- Độ trễ Frontend < 200ms (qua CloudFront)  
- Phản hồi API < 350ms (qua API Gateway + Lightsail)  
- Thời gian hoạt động 99.9% với khôi phục tự động  
- 70%+ yêu cầu được phục vụ từ bộ nhớ cache CDN  
- Không có sự cố bảo mật nghiêm trọng (Cognito + WAF)  
- RTO < 30 phút, RPO = 0 cho bảo vệ dữ liệu  

**KPIs Kinh doanh**
- Tăng 20–30% tỷ lệ chuyển đổi  
- Cải thiện 15–25% tỷ lệ giữ chân khách hàng  
- Giảm 25–40% chi phí cơ sở hạ tầng  
- Chi phí giao dịch thấp hơn phù hợp với hiệu quả giá trị AWS  

---

### **8.2 Lợi Ích Ngắn Hạn (0–6 Tháng)**

- Tải trang nhanh hơn 40–70%, tỷ lệ thoát thấp hơn  
- Giảm tải backend với bộ nhớ cache CDN  
- Xác thực mạnh mẽ hơn qua Cognito  
- Cảnh báo và sao lưu tự động với CloudWatch  
- Triển khai tính năng nhanh hơn nhờ kiến trúc tách rời  

---

### **8.3 Lợi Ích Trung Hạn (6–18 Tháng)**

- Chi phí lưu trữ thấp hơn qua vòng đời S3 → Glacier  
- API ổn định dưới lưu lượng cao  
- Dự báo chi phí thông qua AWS Cost Explorer  
- Điều chỉnh hiệu suất liên tục với bảng điều khiển CloudWatch  
- Giảm khối lượng công việc bảo trì cho lập trình viên  

---

### **8.4 Giá Trị Dài Hạn (18+ Tháng)**

- Nền tảng cloud-native có khả năng mở rộng đầy đủ, sẵn sàng mở rộng mobile hoặc marketplace  
- Sẵn sàng cho AI/ML để đề xuất trang sức cá nhân hóa  
- Giảm 80–90% chi phí lưu trữ qua lưu trữ Glacier  
- Bảo mật và tuân thủ cấp doanh nghiệp (IAM, WAF, CloudTrail)  
- Phạm vi tiếp cận toàn cầu với CloudFront Edge Network  
- Hoạt động bền vững, kiên cường cho tăng trưởng dài hạn  

---

### **8.5 Cải Thiện Trải Nghiệm Người Dùng**

- Tải hình ảnh và duyệt sản phẩm nhanh hơn  
- Đăng nhập và theo dõi đơn hàng mượt mà qua Cognito  
- Giảm độ trễ và thời gian ngừng hoạt động trong giờ cao điểm  
- Tăng niềm tin của khách hàng thông qua độ tin cậy cấp AWS  

---

### **8.6 Năng Lực Chiến Lược Đạt Được**

- Kiến trúc cloud-native, sẵn sàng cho sự phát triển microservices  
- Trưởng thành FinOps với theo dõi chi phí chi tiết  
- Xuất sắc vận hành thông qua giám sát và kiểm toán tập trung  
- Cơ sở hạ tầng sẵn sàng cho tương lai có thể mở rộng sang ECS, EKS hoặc RDS  
- Tuân thủ bảo mật cấp cao sử dụng IAM, Cognito, WAF, Secrets Manager  
- Nền tảng vững chắc cho phân tích dữ liệu và tích hợp AI