---
title: "Event 1"
 
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Bài thu hoạch “AWS Well-Architected Security Pillar”

### Mục Đích Của Sự Kiện

- Chia sẻ các phương pháp thực hành tốt nhất (best practices) dựa trên **AWS Well-Architected Framework (Trụ cột Bảo mật)**.

- Đi sâu vào **Mô hình Trách nhiệm chung (Shared Responsibility Model)** và các nguyên tắc cốt lõi như Zero Trust (Không tin tưởng mặc định) và **Least Privilege** (Quyền tối thiểu).

- Cung cấp hướng dẫn kỹ thuật về hiện đại hóa **Quản lý Định danh & Truy cập (IAM)**.

- Trình bày các chiến lược về Phát hiện mối đe dọa (Detection), Bảo vệ dữ liệu và Tự động hóa ứng phó sự cố (Incident Response - IR).

### Danh Sách Diễn Giả

| Tên Diễn giả | Chức danh | Tổ chức |
| :--- | :--- | :--- |
| **P.G.S.TS. Phạm Đức Long** | Thứ trưởng Bộ Khoa học và Công nghệ | Bộ Khoa học và Công nghệ |
| **H.E. Marc E. Knapper** | Đại sứ Hoa Kỳ tại Việt Nam | Đại sứ quán Hoa Kỳ tại Việt Nam |
| **Jaime Valles** | Phó Chủ tịch, Tổng Giám đốc Châu Á Thái Bình Dương & Nhật Bản | AWS |
| **Jeff Johnson** | Giám đốc Điều hành ASEAN | AWS |
| **Dr. Jens Lottner** | Tổng Giám đốc Điều hành | Techcombank |
| **Dieter Botha** | CEO | TymeX |
| **Trang Phùng** | CEO | U2U Network |
| **Vũ Văn** | Đồng sáng lập & CEO | ELSA Corp |
| **Nguyễn Hòa Bình** | Chủ tịch | Nexttech Group |
| **Gia Hiếu Đinh** | Giám đốc Công nghệ Thông tin | F88 |
| **Nguyễn Hồng Phương Huy** | Trưởng Bộ phận Hạ tầng Cloud & An ninh mạng | Masterise Group |
| **Nguyễn Vũ Hoàng** | Trưởng Bộ phận Công nghệ | VTV Digital |
| **Hà Anh Văn** | Trưởng Phòng: Giải pháp CNTT | Honda Việt Nam |

### Nội Dung Nổi Bật

#### Nền tảng Bảo mật & Nguyên tắc Cốt lõi

- **Mô hình Trách nhiệm chung**: Phân định rõ ranh giới giữa bảo mật của đám mây (do AWS lo) và bảo mật trong đám mây (do Khách hàng lo).

- **Nguyên tắc vàng**:

    * Least Privilege: Chỉ cấp những quyền thực sự cần thiết.

    * Zero Trust: "Không bao giờ tin tưởng, luôn luôn xác minh" — cả bên trong lẫn bên ngoài mạng lưới.

    * Defense in Depth: Thiết lập nhiều lớp kiểm soát bảo mật.

- **Bối cảnh**: Phân tích các mối đe dọa an ninh mạng phổ biến tại môi trường đám mây ở Việt Nam.

#### Pillar 1: Quản lý Định danh & Truy cập (IAM)
- **Kiến trúc IAM hiện đại**:

    * Chuyển dịch từ thông tin xác thực dài hạn (access keys) sang thông tin xác thực tạm thời (Roles).

    * IAM Identity Center: Triển khai SSO (Đăng nhập một lần) để quản lý truy cập tập trung.

_ **Chiến lược Đa tài khoản (Multi-Account)**: Sử dụng SCPs (Service Control Policies) và ranh giới phân quyền để quản lý quyền hạn ở cấp độ Tổ chức (Organization).

- **Vệ sinh định danh (Credential Hygiene)**: Bắt buộc dùng MFA, xoay vòng khóa định kỳ và sử dụng Access Analyzer.

#### Pillar 2: Phát hiện & Giám sát (Detection)
- **Giám sát liên tục**:

    * CloudTrail: Kiểm toán (Audit) các lời gọi API ở cấp độ tổ chức.

    * GuardDuty: Phát hiện mối đe dọa thông minh.

    * Security Hub: Quản lý tư thế bảo mật (security posture) tập trung.

- **Ghi nhật ký (Logging)**: Triển khai log tại mọi tầng (VPC Flow Logs, ALB Logs, S3 Access Logs).

- **Detection-as-Code**: Tự động hóa cảnh báo thông qua EventBridge.

#### Pillar 3 & 4: Bảo vệ Hạ tầng & Dữ liệu
- **Bảo mật Mạng**:

    * Phân đoạn VPC và phân biệt rõ giữa Security Groups (stateful - có trạng thái) và NACLs (stateless - không trạng thái).

    * Bảo vệ biên giới mạng bằng WAF, Shield và Network Firewall.

- **Mã hóa Dữ liệu**:

    * KMS (Key Management Service): Quản lý chính sách khóa và xoay vòng khóa.

    * Mã hóa dữ liệu khi lưu trữ (At-rest: S3, EBS, RDS) và khi truyền tải (In-transit: TLS).

- **Quản lý Bí mật**: Thay thế mật khẩu gán cứng (hard-coded) bằng Secrets Manager hoặc Parameter Store.

#### Pillar 5: Ứng phó Sự cố (Incident Response - IR)
- **Vòng đời IR**: Chuẩn bị, Phát hiện, Ngăn chặn, Loại bỏ, Khôi phục, Hoạt động sau sự cố.

- **Kịch bản ứng phó (Playbooks)**: Hướng dẫn cụ thể cho các tình huống như:

    * Lộ IAM key (Compromised IAM keys).

    * Dữ liệu S3 bị public ra ngoài.

    * EC2 bị nhiễm mã độc.

- **Tự động hóa**: Sử dụng Lambda và Step Functions để tự động khắc phục các mối đe dọa đơn giản (ví dụ: cô lập một máy chủ).

### Những Gì Học Được

#### Tư Duy Thiết Kế

- **Định danh là Vành đai mới**: Tập trung mạnh vào IAM như điểm kiểm soát chính, không chỉ dựa vào tường lửa mạng.

- **Tự động hóa Bảo mật**: Chuyển từ kiểm tra thủ công sang "Security as Code" sử dụng các công cụ như CloudFormation và EventBridge.

- **Giả định vi phạm (Assume Breach)**: Thiết kế hệ thống với giả định rằng cuộc tấn công sẽ xảy ra, tập trung vào việc giảm thiểu phạm vi ảnh hưởng (blast radius).

#### Kiến Trúc Kỹ Thuật

- **Log tập trung**: Log từ VPC, S3, và Ứng dụng phải được lưu trữ tập trung và bất biến (immutable) để phục vụ điều tra.

- **Mã hóa mặc định**: Bật tính năng mã hóa cho tất cả các dịch vụ lưu trữ (EBS, S3, RDS) ngay khi khởi tạo.

- **Phân tách tài khoản**: Sử dụng các tài khoản AWS riêng biệt cho Production, Development và Log Archive để hạn chế tác động khi bị tấn công.

#### Chiến Lược Hiện Đại Hóa

- **Triển khai theo giai đoạn**: Bắt đầu với những điều cơ bản (MFA, CloudTrail) trước khi chuyển sang tự động hóa nâng cao (Auto-remediation).

- **Diễn tập thường xuyên (Game Days)**: Thực hành các Playbook IR thường xuyên để đảm bảo đội ngũ biết cách phản ứng khi có sự cố thực tế.

- **Lộ trình học tập**: Hướng tới chứng chỉ AWS Certified Security – Specialty để đào sâu kiến thức.

### Ứng Dụng Vào Công Việc

- **Kiểm toán IAM Policies**: Rà soát lại người dùng/vai trò hiện tại để loại bỏ các access key dài hạn và bắt buộc dùng MFA.

- **Bật GuardDuty**: Kích hoạt GuardDuty ở tất cả các region để bắt đầu phát hiện mối đe dọa ngay lập tức.

- **Tái cấu trúc Secrets**: Quét mã nguồn để tìm các thông tin xác thực bị gán cứng (hard-coded) và chuyển chúng vào AWS Secrets Manager.

- **Xây dựng IR Playbooks**: Viết và kiểm thử quy trình cụ thể cho các kịch bản "S3 Public Bucket" và "Lộ thông tin xác thực IAM".

- **Triển khai SCPs**: Nếu đang sử dụng AWS Organizations, hãy áp dụng Service Control Policies để ngăn chặn việc sử dụng tài khoản root hoặc tắt CloudTrail trái phép.

### Trải nghiệm trong event

Tham dự buổi chia sẻ **AWS Well-Architected Security Pillar** mang lại giá trị thực tiễn cao, cung cấp một cách tiếp cận có cấu trúc về bảo mật đám mây thay vì chỉ liệt kê các công cụ rời rạc. Các trải nghiệm chính bao gồm:

#### Học hỏi từ các diễn giả có chuyên môn cao
- Việc phân tích sâu Mô hình Trách nhiệm chung giúp làm rõ chính xác những gì đội ngũ phát triển cần chịu trách nhiệm so với những gì AWS đảm nhận.

- Hiểu rõ bối cảnh các mối đe dọa cụ thể tại Việt Nam giúp ưu tiên các biện pháp kiểm soát bảo mật cần triển khai trước.

#### Trải nghiệm kỹ thuật thực tế
- Mini Demo (IAM): Phần demo về xác thực IAM Policy và giả lập truy cập (simulate access) cực kỳ hữu ích để gỡ lỗi quyền hạn mà không gây rủi ro cho môi trường production.

- Mô phỏng IR: Việc trực quan hóa quy trình phát hiện EC2 nhiễm mã độc -> tạo snapshot -> cô lập instance là một điểm nhấn ấn tượng.

#### Ứng dụng công cụ hiện đại
- Thấy được sức mạnh của Access Analyzer trong việc xác định các truy cập public ngoài ý muốn.

- Học cách EventBridge có thể biến một log thụ động thành một cảnh báo chủ động hoặc hành động khắc phục tức thì.

#### Kết nối và trao đổi
Phiên Q&A về "Các lỗi thường gặp trong doanh nghiệp Việt" đưa ra những cảnh báo thực tế về việc cấu hình sai Security Groups và quyền hạn S3.

#### Bài học rút ra
- Bảo mật không phải là rào cản mà là yếu tố thúc đẩy (enabler) khi áp dụng mô hình "Detection-as-Code".

- Ứng phó sự cố hiệu quả dựa rất nhiều vào sự chuẩn bị (Playbooks) và tự động hóa; cố gắng tìm giải pháp trong khi đang bị tấn công là quá muộn.

#### Một số hình ảnh khi tham gia sự kiện

![Your profile picture](/images/event1.png)

> Tổng thể, sự kiện không chỉ cung cấp kiến thức kỹ thuật mà còn giúp tôi thay đổi cách tư duy về thiết kế ứng dụng, hiện đại hóa hệ thống và phối hợp hiệu quả hơn giữa các team.
