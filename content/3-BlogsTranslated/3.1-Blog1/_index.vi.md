---
title: "Blog 1"
 
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Xây dựng trợ lý AI có khả năng mở rộng để giúp đỡ người tị nạn bằng AWS

của Taras Tsarenko , Anton Garvanko và Vitalii Bozadzhy, Vladyslav Horbatenko | 03 tháng 6 năm 2025 | in Amazon Bedrock, Amazon Machine Learning, Amazon Rekognition, Amazon Translate, Architecture, Artificial Intelligence, Customer Solutions| Permalink |  Comments |  Share
Bài đăng này được đồng viết với Taras Tsarenko, Vitalil Bozadzhy và Vladyslav Horbatenko. 
Trong bối cảnh các tổ chức trên toàn thế giới đang tìm cách ứng dụng AI để tạo ra tác động xã hội, tổ chức nhân đạo Đan Mạch Bevar Ukraine đã phát triển một trợ lý ảo toàn diện, được hỗ trợ bởi AI, có tên là Victor, nhằm giải quyết những nhu cầu cấp thiết của người tị nạn Ukraine đang hòa nhập vào xã hội Đan Mạch. Bài viết này trình bày chi tiết về việc triển khai kỹ thuật của chúng tôi bằng cách sử dụng các dịch vụ AWS để tạo ra một hệ thống trợ lý AI đa ngôn ngữ, có khả năng mở rộng, cung cấp hỗ trợ tự động trong khi vẫn đảm bảo bảo mật dữ liệu và tuân thủ GDPR.
Bevar Ukraine được thành lập năm 2014 và đã đi đầu trong việc hỗ trợ người tị nạn Ukraine tại Đan Mạch kể từ cuộc chiến tranh toàn diện năm 2022, cung cấp hỗ trợ cho hơn 30.000 người Ukraine về nhà ở, tìm kiếm việc làm và các dịch vụ hội nhập. Tổ chức này cũng đã chuyển hơn 200 tấn hàng viện trợ nhân đạo cho Ukraine, bao gồm vật tư y tế, máy phát điện và các mặt hàng thiết yếu cho thường dân bị ảnh hưởng bởi chiến tranh.


## Bối cảnh và thách thức

Việc hòa nhập người tị nạn vào các quốc gia tiếp nhận đặt ra nhiều thách thức, đặc biệt là trong việc tiếp cận các dịch vụ công và xử lý các thủ tục pháp lý phức tạp. Các hệ thống hỗ trợ truyền thống, vốn phụ thuộc nhiều vào nhân viên xã hội, thường gặp phải những hạn chế về khả năng mở rộng và rào cản ngôn ngữ. Giải pháp của Bevar Ukraine giải quyết những thách thức này thông qua một hệ thống được hỗ trợ bởi AI, hoạt động liên tục trong khi vẫn duy trì tiêu chuẩn chất lượng dịch vụ cao.

## Tổng quan về giải pháp

Nền tảng của giải pháp bao gồm một số dịch vụ AWS nhằm cung cấp trợ lý generative AI đáng tin cậy, an toàn và hiệu quả cho người tị nạn Ukraine. Nhóm gồm ba nhà phát triển phần mềm tình nguyện đã phát triển giải pháp này chỉ trong vài tuần.
Sơ đồ sau đây minh họa kiến trúc giải pháp.

![picture 1](/images/image3.1.1.png)

Amazon Elastic Compute Cloud (Amazon EC2) đóng vai trò là lớp điện toán chính, sử dụng Spot Instance để tối ưu hóa chi phí. Amazon Simple Storage Service (Amazon S3) cung cấp dịch vụ lưu trữ an toàn cho nhật ký hội thoại và tài liệu hỗ trợ, trong khi Amazon Bedrock hỗ trợ các chức năng xử lý ngôn ngữ tự nhiên cốt lõi. Bevar Ukraine sử dụng Amazon DynamoDB để truy cập dữ liệu theo thời gian thực và quản lý phiên, mang lại phản hồi độ trễ thấp ngay cả khi tải cao.
Trong quá trình triển khai, chúng tôi nhận thấy mô hình ngôn ngữ lớn (LLM) Claude 3.5 của Anthropic là lựa chọn phù hợp nhất nhờ logic hội thoại tiên tiến và khả năng duy trì giọng điệu giống con người. Mô hình này phù hợp nhất cho những phản hồi sâu sắc, hợp lý và tạo ra nội dung sáng tạo hơn, giúp câu trả lời của Victor tự nhiên và hấp dẫn hơn.
Amazon Titan Embeddings G1 – Text v1.2 vượt trội trong việc tạo ra các biểu diễn vector chất lượng cao cho văn bản đa ngôn ngữ, cho phép tìm kiếm ngữ nghĩa và so sánh độ tương đồng hiệu quả. Điều này đặc biệt hữu ích khi Victor cần truy xuất thông tin liên quan từ một cơ sở kiến thức lớn hoặc so sánh truy vấn của người dùng với các dữ liệu đầu vào đã xem trước đó. Amazon Titan Embeddings cũng tích hợp mượt mà với AWS, giúp đơn giản hóa các tác vụ như lập chỉ mục, tìm kiếm và truy xuất.
Trong các tương tác thực tế với Victor, một số truy vấn yêu cầu câu trả lời ngắn gọn, cụ thể, trong khi những truy vấn khác cần sự sáng tạo hoặc hiểu biết về ngữ cảnh. Bằng cách kết hợp Claude 3.5 của Anthropic để tạo và Amazon Titan Embeddings G1 để truy xuất ngữ nghĩa, Victor có thể định tuyến từng truy vấn qua đường dẫn phù hợp nhất, truy xuất ngữ cảnh liên quan thông qua các nhúng và tạo ra phản hồi, mang lại câu trả lời chính xác và phù hợp với ngữ cảnh hơn.
Amazon Bedrock cung cấp giao diện đáng chú ý để gọi Claude 3.5 của Anthropic và Amazon Titan Embeddings G1 (cùng với các mô hình khác) mà không cần tạo tích hợp riêng cho từng nhà cung cấp, giúp đơn giản hóa quá trình phát triển và bảo trì.
Để hỗ trợ đa ngôn ngữ, chúng tôi đã sử dụng các trình nhúng hỗ trợ nhúng đa ngôn ngữ và dịch tài liệu bằng Amazon Translate . Điều này giúp tăng cường khả năng phục hồi của hệ thống Retrieval Augmented Generation (RAG) của chúng tôi. Ứng dụng được xây dựng an toàn và sử dụng các dịch vụ AWS để thực hiện việc này. AWS Key Management Service (AWS KMS) đơn giản hóa quy trình mã hóa dữ liệu trong ứng dụng, và Amazon API Gateway hỗ trợ các điểm cuối REST của ứng dụng. Khả năng xác thực và ủy quyền người dùng được hỗ trợ bởi Amazon Cognito , cung cấp các tính năng quản lý danh tính và truy cập khách hàng (CIAM) an toàn và có khả năng mở rộng.
Ứng dụng chạy trên cơ sở hạ tầng AWS bằng các dịch vụ được thiết kế để bảo mật và có khả năng mở rộng như Amazon S3, AWS Lambda và DynamoDB

## Mẹo và khuyến nghị

Việc xây dựng giải pháp trợ lý AI cho người tị nạn bằng Amazon Bedrock và các dịch vụ AWS khác đã mang lại những hiểu biết quý giá về việc tạo ra các giải pháp nhân đạo hiệu quả dựa trên AI. Thông qua việc triển khai này, chúng tôi đã khám phá ra những cân nhắc quan trọng mà các tổ chức nên lưu ý khi phát triển các giải pháp tương tự. Trải nghiệm này đã nhấn mạnh tầm quan trọng của việc cân bằng năng lực kỹ thuật với thiết kế lấy con người làm trung tâm, cung cấp hỗ trợ đa ngôn ngữ, duy trì quyền riêng tư dữ liệu và tạo ra các giải pháp có khả năng mở rộng nhưng vẫn tiết kiệm chi phí. Những bài học kinh nghiệm này có thể đóng vai trò là nền tảng cho các tổ chức muốn sử dụng AI và công nghệ đám mây để hỗ trợ các hoạt động nhân đạo, đặc biệt là trong việc tạo ra hỗ trợ kỹ thuật số dễ tiếp cận và hữu ích cho những người dân di cư. Sau đây là những điểm chính
  * Sử dụng sân chơi Amazon Bedrock để kiểm tra nhiều LLM cạnh nhau bằng cùng một lời nhắc. Điều này giúp bạn tìm ra mô hình mang lại chất lượng, phong cách và giọng điệu phản hồi tốt nhất cho trường hợp sử dụng cụ thể của bạn (ví dụ: độ chính xác về mặt thực tế so với giọng điệu đàm thoại).
  * Thử nghiệm với các lời nhắc và cài đặt để cải thiện phản hồi.
  * Ghi nhớ chi phí; thiết lập giám sát và ngân sách trong AWS.
  * Đối với các tác vụ liên quan đến truy xuất thông tin hoặc tìm kiếm ngữ nghĩa, hãy chọn mô hình nhúng và đảm bảo chọn đúng cài đặt. Hãy chú ý đến kích thước của các nhúng, vì các vectơ lớn hơn có thể nắm bắt được nhiều ý nghĩa hơn nhưng có thể làm tăng chi phí. Ngoài ra, hãy kiểm tra xem mô hình có hỗ trợ các ngôn ngữ mà ứng dụng của bạn yêu cầu hay không.
  * Nếu bạn đang sử dụng cơ sở kiến thức, hãy sử dụng sân chơi cơ sở kiến thức Amazon Bedrock để thử nghiệm cách phân đoạn nội dung và số lượng đoạn văn được truy xuất cho mỗi truy vấn. Việc tìm đúng số lượng đoạn văn được truy xuất có thể tạo ra sự khác biệt lớn về độ rõ ràng và tập trung của câu trả lời cuối cùng—đôi khi, ít đoạn văn chất lượng cao hơn sẽ hiệu quả hơn là gửi quá nhiều ngữ cảnh.
  * Để đảm bảo an toàn và quyền riêng tư, hãy sử dụng Amazon Bedrock Guardrails . Guardrails có thể giúp ngăn chặn mô hình rò rỉ thông tin nhạy cảm, chẳng hạn như dữ liệu cá nhân hoặc nội dung doanh nghiệp nội bộ, và bạn có thể chặn các phản hồi có hại hoặc áp dụng một giọng điệu và phong cách định dạng cụ thể.
  * Bắt đầu với một nguyên mẫu đơn giản, kiểm tra chất lượng nhúng trong miền của bạn và mở rộng theo từng bước.


## Lớp tích hợp và nâng cao

Bevar Ukraine đã mở rộng cơ sở hạ tầng cốt lõi của AWS bằng một số công nghệ bổ sung:
  * Pinecone  – Để lưu trữ và truy xuất hiệu quả các nhúng ngữ nghĩa
  * DSPy framework – Để thiết kế lời nhắc có cấu trúc và tối ưu hóa các phản hồi Claude 3.5 Sonnet của Anthropic
  * EasyWeek– Để lên lịch hẹn và quản lý tài nguyên
  * Telegram API – Để cung cấp giao diện người dùng
  * Amazon Bedrock Guardrails – Để thực thi chính sách bảo mật
  * Amazon Rekognition – Để xác minh tài liệu
  * Quy trình tích hợp và phân phối liên tục (CI/CD) dựa trên GitHub – Để triển khai tính năng nhanh chóng

## Những hiểu biết kỹ thuật quan trọng

Việc triển khai đã bộc lộ một số cân nhắc kỹ thuật quan trọng. Khung DSPy đóng vai trò then chốt trong việc tối ưu hóa và nâng cao các gợi ý mô hình ngôn ngữ của chúng tôi. Bằng cách tích hợp thêm các lớp công cụ lập luận và nhận thức ngữ cảnh, DSPy đã cải thiện đáng kể độ chính xác, tính nhất quán và chiều sâu của phản hồi. Nhóm nghiên cứu nhận thấy rằng việc thiết kế một cơ sở tri thức mạnh mẽ với siêu dữ liệu toàn diện là nền tảng cho hiệu quả của hệ thống.
Việc tuân thủ GDPR đòi hỏi các quyết định kiến trúc cẩn thận, bao gồm giảm thiểu dữ liệu, lưu trữ an toàn và cơ chế đồng ý rõ ràng của người dùng. Việc tối ưu hóa chi phí đã đạt được thông qua việc sử dụng EC2 Spot Instance một cách chiến lược và triển khai điều tiết yêu cầu API, mang lại khoản tiết kiệm vận hành đáng kể mà không ảnh hưởng đến hiệu suất.


## Những cải tiến trong tương lai

Lộ trình của chúng tôi bao gồm một số cải tiến kỹ thuật nhằm nâng cao khả năng của hệ thống:
  * Triển khai phân phối ngữ cảnh nâng cao bằng thuật toán học máy để cải thiện sự phối hợp dịch vụ trên nhiều miền
  * Phát triển một hệ thống xác thực vòng lặp con người tinh vi cho các trường hợp phức tạp đòi hỏi sự giám sát của chuyên gia
  * Di chuyển các thành phần phù hợp sang kiến trúc không máy chủ bằng Lambda để tối ưu hóa việc sử dụng tài nguyên và chi phí
  * Nâng cao cơ sở kiến thức với khả năng tìm kiếm ngữ nghĩa nâng cao và cập nhật nội dung tự động

## Kết quả

Giải pháp này, phục vụ hàng trăm người tị nạn Ukraine tại Đan Mạch mỗi ngày, chứng minh tiềm năng của các dịch vụ AWS trong việc tạo ra các hệ thống AI có khả năng mở rộng, bảo mật và hiệu quả, hướng đến tác động xã hội. Nhờ đó, các tình nguyện viên và nhân viên của Bevar Ukraine đã tiết kiệm được hàng nghìn giờ làm việc, và thay vì phải trả lời những câu hỏi lặp đi lặp lại từ người tị nạn, họ có thể hỗ trợ họ trong những tình huống phức tạp hơn của cuộc sống. Đối với người tị nạn, trợ lý ảo Victor là một trợ thủ đắc lực, cho phép người dùng nhận được câu trả lời cho những câu hỏi cấp bách nhất về các dịch vụ công tại Đan Mạch và nhiều câu hỏi khác chỉ trong vài giây thay vì phải chờ đợi tình nguyện viên hỗ trợ. Với nền tảng kiến thức rộng lớn mà Victor đang sử dụng để tạo ra phản hồi, chất lượng hỗ trợ cũng đã được cải thiện.

## Phần kết luận

Thông qua thiết kế kiến trúc cẩn thận và tích hợp các công nghệ bổ sung, chúng tôi đã tạo ra một nền tảng giải quyết hiệu quả những thách thức mà người tị nạn phải đối mặt trong khi vẫn duy trì các tiêu chuẩn cao về bảo mật và bảo vệ dữ liệu.
Sự thành công của việc triển khai này cung cấp một bản thiết kế cho các giải pháp tương tự trong các lĩnh vực dịch vụ xã hội khác, có khả năng hỗ trợ người tị nạn và những người khác đang gặp khó khăn trên toàn thế giới, nhấn mạnh tầm quan trọng của việc kết hợp cơ sở hạ tầng đám mây mạnh mẽ với thiết kế hệ thống chu đáo để tạo ra tác động xã hội có ý nghĩa.

## Giới thiệu về các tác giả

![picture 2](/images/image3.1.2.png)

Taras Tsarenko là Quản lý Chương trình tại Bevar Ukraine. Trong hơn một thập kỷ hoạt động trong lĩnh vực công nghệ, Taras đã dẫn dắt mọi thứ, từ các nhóm Agile gắn kết chặt chẽ gồm 5 người trở lên cho đến một công ty 90 người, công ty đã trở thành công ty CNTT nhỏ tốt nhất tại Ukraine dưới 100 người vào năm 2015. Taras là một nhà xây dựng luôn phát triển mạnh mẽ ở giao điểm giữa chiến lược và thực thi, nơi chuyên môn kỹ thuật kết hợp với tác động của con người, dù là tinh giản quy trình làm việc, giải quyết các vấn đề phức tạp hay trao quyền cho các nhóm tạo ra các sản phẩm có ý nghĩa. Taras chuyên về các giải pháp dựa trên AI và kỹ thuật dữ liệu, tận dụng các công nghệ như học máy và AI tạo sinh bằng cách sử dụng Amazon SageMaker AI, Amazon Bedrock, Amazon OpenSearch Service, v.v. Taras là Cộng tác viên Kỹ sư ML được Chứng nhận AWS.

![picture 3](/images/image3.1.3.png)

Anton Garvanko là Chuyên gia Phân tích Kinh doanh Cấp cao khu vực Bắc Âu tại AWS. Xuất thân từ chuyên gia tài chính chuyển sang làm nhân viên kinh doanh, Anton đã có 15 năm kinh nghiệm đảm nhiệm nhiều vị trí lãnh đạo tài chính khác nhau trong các ngành chuỗi cung ứng, hậu cần và dịch vụ tài chính. Anton gia nhập Amazon hơn 5 năm trước và là thành viên của các nhóm bán hàng chuyên biệt tập trung vào trí tuệ kinh doanh, phân tích và trí tuệ nhân tạo (AI) trong hơn 3 năm. Anh tâm huyết với việc kết nối thế giới tài chính và CNTT bằng cách đảm bảo rằng trí tuệ kinh doanh và phân tích được hỗ trợ bởi AI hỗ trợ việc ra quyết định hàng ngày trong nhiều ngành và nhiều trường hợp sử dụng.

![picture 4](/images/image3.1.4.png)

Vitalii Bozadzhy là một Lập trình viên Cao cấp với kinh nghiệm dày dặn trong việc xây dựng các giải pháp đám mây tải cao, chuyên về Java, Golang, SWIFT và Python. Anh chuyên về các hệ thống backend có khả năng mở rộng, kiến trúc microservice được thiết kế để tự động hóa quy trình kinh doanh, cũng như xây dựng cơ sở hạ tầng đám mây đáng tin cậy và an toàn. Hơn nữa, anh có kinh nghiệm trong việc tối ưu hóa tài nguyên tính toán và xây dựng các giải pháp tiên tiến được tích hợp vào sản phẩm. Chuyên môn của anh bao quát toàn bộ chu trình phát triển - từ thiết kế và kiến trúc đến triển khai và bảo trì - với trọng tâm là hiệu suất, khả năng chịu lỗi và đổi mới.

![picture 5](/images/image3.1.5.png)

Vladyslav Horbatenko là sinh viên khoa học máy tính, Trợ lý Giáo sư và Nhà khoa học Dữ liệu, chuyên sâu về trí tuệ nhân tạo. Vladyslav bắt đầu hành trình của mình với học máy, học tăng cường và học sâu, và dần dần quan tâm hơn đến các mô hình ngôn ngữ lớn (LLM) và tác động tiềm năng của chúng. Điều này đã giúp anh hiểu sâu hơn về LLM, và hiện đang làm việc để phát triển, duy trì và cải tiến các giải pháp dựa trên LLM. Anh đóng góp vào các dự án sáng tạo đồng thời luôn cập nhật những tiến bộ mới nhất trong lĩnh vực AI.