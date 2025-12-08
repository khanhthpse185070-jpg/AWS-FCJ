---
title: "Event 2"
 
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Bài thu hoạch “DevOps on AWS”

### Mục Đích Của Sự Kiện

- Chia sẻ các phương pháp thực hành tốt nhất về xây dựng Văn hóa DevOps và tự động hóa quy trình phát triển phần mềm.

- Đi sâu vào bộ công cụ "native" của AWS để xây dựng CI/CD Pipeline hoàn chỉnh.

- Cung cấp hướng dẫn kỹ thuật về việc chuyển dịch từ thao tác thủ công ("ClickOps") sang Mã hóa hạ tầng (Infrastructure as Code - IaC).

- Trình diễn các chiến lược hiện đại hóa ứng dụng với Container và thiết lập khả năng quan sát toàn diện (Observability).

### Danh Sách Diễn Giả

| Tên Diễn giả | Chức danh | Tổ chức |
| :--- | :--- | :--- |
| **Nguyễn Tuấn Huy** | Giám đốc Chuyển đổi Số | Mobifone |
| **Minh Hoàng** | Giám đốc Dữ liệu | Techcom Securities |
| **Vincent Nguyễn** | Giám đốc Điều hành | Nam Long Commercial Property |
| **Seunghoon Chae** | Tổng Giám đốc | MegazoneCloud Việt Nam |
| **Uy Trần** | Đồng sáng lập & COO | Katalon |
| **Thái Huy Chương** | Trưởng Bộ phận Phát triển Ứng dụng | Bảo Việt Holdings |
| **Trần Đình Khiêm** | Giám đốc Ngân hàng Số | Techcombank |
| **Christopher Bennett** | Giám đốc Công nghệ | TymeX |
| **Selma Belhadjamor** | Nhà Khoa học Dữ liệu Chính | Onebyzero |
| **Ngô Mạnh Hà** | Đồng CEO, CTO | TechX Corp |
| **Nguyễn Thanh Bình** | Trưởng Bộ phận DevOps | Renova Cloud |

### Nội Dung Nổi Bật

#### Nền tảng Tư duy & Văn hóa DevOps

- Mindset cốt lõi: DevOps không phải là một chức danh, mà là sự kết hợp giữa Văn hóa, Công cụ và Quy trình.

- Chỉ số đo lường (DORA Metrics): Tập trung vào 4 chỉ số vàng để đánh giá hiệu quả:

    * Tần suất triển khai (Deployment Frequency).

    * Thời gian thay đổi (Lead Time for Changes).

    * Thời gian khôi phục trung bình (MTTR).

    * Tỷ lệ lỗi khi thay đổi (Change Failure Rate).

#### Pillar 1: Tự động hóa Pipeline (CI/CD)

- Quy trình chuẩn trên AWS:

    * CodeCommit: Quản lý mã nguồn tập trung (Git-based).

    * CodeBuild & CodeTest: Tự động hóa việc biên dịch và chạy Unit Test/SAST.

    * CodeDeploy: Tự động hóa việc đẩy code xuống hạ tầng.

- Chiến lược Triển khai:

    * Blue/Green: Chuyển đổi traffic tức thì giữa môi trường cũ và mới, đảm bảo Zero-downtime.

    - Canary: Phân phối traffic nhỏ giọt (10% -> 50%) để giảm thiểu rủi ro.

- Demo: Thiết lập một pipeline đầy đủ với cơ chế phê duyệt thủ công (Manual Approval) trước khi ra Production.

#### Pillar 2: Mã hóa Hạ tầng (IaC)

- Chống lại "ClickOps": Loại bỏ hoàn toàn việc cấu hình thủ công trên Console để tránh sai sót và thiếu đồng bộ.

- Công cụ IaC:

    * CloudFormation: Nền tảng cơ bản sử dụng template JSON/YAML.

    * AWS CDK (Cloud Development Kit): Xu hướng mới, cho phép viết hạ tầng bằng ngôn ngữ lập trình (TypeScript, Python) với các Constructs tái sử dụng cao.

- Drift Detection: Kỹ thuật phát hiện sự sai lệch giữa cấu hình thực tế và mã nguồn IaC.

#### Pillar 3: Hạ tầng Container & Serverless

- Lựa chọn Compute:

    * Amazon ECS: Đơn giản, tích hợp sâu, phù hợp với team muốn tập trung vào ứng dụng.

    * Amazon EKS: Dành cho các hệ thống cần chuẩn Kubernetes mở rộng và tùy biến cao.

    * AWS App Runner: Giải pháp fully-managed, không cần quản lý server hay orchestrator.

- Quản lý Image: Sử dụng Amazon ECR với tính năng quét lỗ hổng bảo mật tự động.

#### Pillar 4: Giám sát & Quan sát (Observability)

- Toàn diện hóa giám sát:

    * CloudWatch: Thu thập Metrics, Logs và thiết lập Alarms thông minh.

    * AWS X-Ray: Truy vết phân tán (Distributed Tracing) để vẽ bản đồ service map và tìm điểm nghẽn (bottleneck) trong kiến trúc Microservices.

- Dashboard: Xây dựng các bảng điều khiển tập trung cho cả Dev và Ops.

### Những Gì Học Được

#### Tư Duy Thiết Kế

- Fail Fast: Tích hợp kiểm thử tự động ngay trong giai đoạn Build để phát hiện lỗi sớm nhất có thể.

- Shift Left: Đưa bảo mật và kiểm thử lên đầu quy trình phát triển, không đợi đến khi deploy mới kiểm tra.

- Hạ tầng là Phần mềm: Quản lý phiên bản hạ tầng y hệt như quản lý mã nguồn ứng dụng (Version Control).

#### Kiến Trúc Kỹ Thuật

- Hạ tầng Bất biến (Immutable Infrastructure): Không bao giờ vá (patch) server đang chạy; thay thế nó bằng một server mới hoàn toàn.

- Chiến lược Git: Sử dụng Trunk-based Development cho các dự án cần tốc độ cao, thay vì quy trình GitFlow quá phức tạp.

#### Chiến Lược Hiện Đại Hóa

- Container First: Ưu tiên đóng gói ứng dụng vào Docker container để đảm bảo tính nhất quán giữa các môi trường (Dev/Test/Prod).

- Platform Engineering: Xây dựng nền tảng tự phục vụ (Self-service platform) để Dev có thể tự deploy mà không cần chờ đợi Ops.

### Ứng Dụng Vào Công Việc

- Triển khai CDK: Bắt đầu chuyển đổi các dự án hạ tầng mới sang dùng AWS CDK (TypeScript) để dễ bảo trì.

- Tự động Rollback: Cấu hình CloudWatch Alarm để tự động kích hoạt Rollback trong CodeDeploy nếu tỷ lệ lỗi HTTP 5xx tăng cao.

- Bật X-Ray: Kích hoạt tính năng tracing cho các Lambda functions và ECS services để debug vấn đề hiệu năng.

- Rà soát Pipeline: Thêm bước quét bảo mật tĩnh (Security Scan) vào pipeline hiện tại.

### Trải nghiệm trong event

Tham gia workshop **“DevOps on AWS”** là một trải nghiệm rất bổ ích, giúp tôi có cái nhìn toàn diện về cách hiện đại hóa ứng dụng và cơ sở dữ liệu bằng các phương pháp và công cụ hiện đại. Một số trải nghiệm nổi bật:

#### Học hỏi từ các diễn giả có chuyên môn cao
- Cuộc tranh luận về GitFlow vs Trunk-based giúp làm rõ ưu nhược điểm của từng chiến lược quản lý mã nguồn.

- Hiểu rõ cách AWS vận hành nội bộ giúp củng cố niềm tin vào văn hóa "You build it, you run it".

#### Trải nghiệm kỹ thuật thực tế
- Demo Blue/Green: Việc chứng kiến traffic chuyển đổi mượt mà giữa hai phiên bản ứng dụng mà không gây gián đoạn dịch vụ là minh chứng rõ nhất cho giá trị của DevOps.

- IaC Simulation: Thấy được sự tiện lợi của CDK khi chỉ cần vài dòng code TypeScript có thể dựng lên cả một VPC và Cluster.

#### Ứng dụng công cụ hiện đại
- Ấn tượng với App Runner vì khả năng deploy cực nhanh từ source code mà không cần viết Dockerfile phức tạp.

- Thấy được sức mạnh của X-Ray trong việc minh bạch hóa các lời gọi giữa các microservices.

#### Kết nối và trao đổi
- Phiên thảo luận giờ giải lao rất sôi nổi với chủ đề "Jenkins vs. AWS CodePipeline". Nhiều đồng nghiệp chia sẻ nỗi đau về việc phải bảo trì Jenkins server và đang cân nhắc chuyển sang dịch vụ managed như CodePipeline để giảm tải vận hành.

- Trao đổi với các kỹ sư từ một startup Fintech về câu chuyện thực tế xử lý "Alert Fatigue" (Bội thực cảnh báo) và cách họ tinh chỉnh CloudWatch để chỉ báo những lỗi quan trọng.

#### Bài học rút ra
- Tự động hóa không chỉ là công cụ, mà là cách để giải phóng con người khỏi các tác vụ lặp lại nhàm chán.

- Observability là bắt buộc đối với Microservices; nếu không có Tracing, việc debug giống như "mò kim đáy bể".

#### Một số hình ảnh khi tham gia sự kiện

![Your profile picture](/images/event2.png)

> Tổng thể, sự kiện không chỉ cung cấp kiến thức kỹ thuật mà còn giúp tôi thay đổi cách tư duy về thiết kế ứng dụng, hiện đại hóa hệ thống và phối hợp hiệu quả hơn giữa các team.
