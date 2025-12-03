---
title: "Blog 6"
 
weight: 1
chapter: false
pre: " <b> 3.6. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Xây dựng các tác nhân AI có khả năng tạo ra linh hoạt

bởi Yiwen Zhang, Hechmi Khelifi và Jennifer Moran trên30 THÁNG 9 NĂM 2025 trong Nâng cao (300) , Amazon Bedrock , AWS Well-Architected , Thực tiễn tốt nhất , Trí tuệ nhân tạo , Khả năng phục hồi Liên kết cố định| Bình luận | Chia sẻ

Các tác nhân AI tạo sinh trong môi trường sản xuất đòi hỏi các chiến lược phục hồi vượt xa các mô hình phần mềm truyền thống. Các tác nhân AI đưa ra quyết định tự động, tiêu tốn đáng kể tài nguyên tính toán và tương tác với các hệ thống bên ngoài theo những cách không thể đoán trước. Những đặc điểm này tạo ra các chế độ lỗi mà các phương pháp phục hồi thông thường có thể không giải quyết được.

Bài viết này trình bày một khuôn khổ phân tích rủi ro phục hồi tác nhân AI, áp dụng cho hầu hết các kiến ​​trúc triển khai và phát triển AI. Chúng tôi cũng khám phá các chiến lược thực tế để giúp ngăn ngừa, phát hiện và giảm thiểu những thách thức phục hồi phổ biến nhất khi triển khai và mở rộng quy mô tác nhân AI.

## Các khía cạnh rủi ro phục hồi của tác nhân AI tạo ra
Để xác định rủi ro về khả năng phục hồi, chúng tôi chia nhỏ các hệ thống tác nhân AI tạo ra thành bảy chiều:

  * Mô hình nền tảng – Mô hình nền tảng (FM) cung cấp khả năng lập kế hoạch và suy luận cốt lõi. Lựa chọn triển khai của bạn quyết định trách nhiệm và chi phí phục hồi của bạn. Ba phương pháp triển khai được quản lý hoàn toàn tự động, chẳng hạn như sử dụng Amazon Elastic Compute Cloud (Amazon EC2), dịch vụ được quản lý dựa trên máy chủ như Amazon SageMaker AI , hoặc dịch vụ được quản lý không máy chủ như Amazon Bedrock .
  * Điều phối tác nhân – Thành phần này kiểm soát cách nhiều tác nhân và công cụ AI phối hợp để đạt được các mục tiêu phức tạp, bao gồm logic để lựa chọn công cụ, kích hoạt leo thang của con người và quản lý quy trình làm việc nhiều bước.
  * Cơ sở hạ tầng triển khai tác nhân – Cơ sở hạ tầng bao gồm phần cứng và hệ thống cơ bản nơi các tác nhân chạy. Các tùy chọn cơ sở hạ tầng bao gồm sử dụng các phiên bản EC2 tự quản lý hoàn toàn, các dịch vụ được quản lý như Amazon Elastic Container Services (Amazon ECS) và các dịch vụ được quản lý chuyên biệt được thiết kế riêng cho việc triển khai tác nhân, chẳng hạn như Amazon Bedrock AgentCore Runtime .
  * Cơ sở tri thức – Cơ sở tri thức bao gồm lưu trữ cơ sở dữ liệu vector, mô hình nhúng và đường ống dữ liệu tạo ra các nhúng vector, tạo thành nền tảng cho các ứng dụng Retrieval Augmented Generation (RAG). Cơ sở tri thức Amazon Bedrock hỗ trợ các quy trình làm việc RAG được quản lý hoàn toàn.
  * Công cụ tác nhân – Bao gồm các công cụ API, máy chủ Giao thức bối cảnh mô hình (MCP), quản lý bộ nhớ và các tính năng lưu trữ đệm nhanh chóng giúp mở rộng khả năng của tác nhân.
  * Bảo mật và tuân thủ – Thành phần này bao gồm các biện pháp kiểm soát bảo mật của người dùng và tác nhân cũng như giám sát tuân thủ nội dung, hỗ trợ xác thực, ủy quyền và xác thực nội dung phù hợp. Bảo mật bao gồm xác thực đến để quản lý quyền truy cập của người dùng vào tác nhân và xác thực và ủy quyền đi để quản lý quyền truy cập của tác nhân vào các tài nguyên khác. Ủy quyền đi phức tạp hơn vì các tác nhân có thể yêu cầu danh tính riêng của họ . Amazon Bedrock AgentCore Identity là dịch vụ quản lý danh tính và thông tin xác thực được thiết kế dành riêng cho tác nhân AI, cung cấp khả năng xác thực và ủy quyền đến và đi. Để giúp ngăn ngừa các hành vi vi phạm tuân thủ, các tổ chức nên thiết lập các chính sách AI có trách nhiệm toàn diện. Amazon Bedrock Guardrails cung cấp các biện pháp bảo vệ có thể cấu hình để triển khai chính sách AI có trách nhiệm.
  * Đánh giá và khả năng quan sát – Các hệ thống này theo dõi các số liệu từ thống kê cơ sở hạ tầng cơ bản đến các dấu vết chi tiết cụ thể về AI, bao gồm đánh giá hiệu suất liên tục và phát hiện các sai lệch về hành vi. Việc đánh giá và khả năng quan sát tác nhân đòi hỏi sự kết hợp giữa các số liệu hệ thống truyền thống và các tín hiệu cụ thể của tác nhân, chẳng hạn như dấu vết suy luận và kết quả gọi công cụ.

Sơ đồ sau đây minh họa các kích thước này.
![picture 1](/images/image6.png)
Cấu hình này cung cấp khả năng hiển thị vào các ứng dụng của tác nhân, cho phép các phiên tiếp theo đưa ra phân tích khả năng phục hồi có mục tiêu và các khuyến nghị giảm thiểu.

## 5 vấn đề phục hồi hàng đầu cho các tác nhân và kế hoạch giảm thiểu
Khung Phân tích Khả năng Phục hồi xác định các chế độ lỗi cơ bản mà hệ thống sản xuất nên tránh. Trong bài viết này, chúng tôi xác định năm chế độ lỗi chính của các tác nhân AI tạo sinh và cung cấp các chiến lược có thể giúp thiết lập các đặc tính phục hồi.

### Số phận chung
Chia sẻ số phận xảy ra khi lỗi trong một thành phần tác nhân lan rộng ra toàn bộ hệ thống, ảnh hưởng đến toàn bộ tác nhân. Cô lập lỗi là đặc tính mong muốn. Để đạt được điều này, bạn phải hiểu cách các thành phần tác nhân tương tác và xác định các mối phụ thuộc chung của chúng.

Mối quan hệ giữa FM, cơ sở tri thức và điều phối tác nhân đòi hỏi ranh giới cô lập rõ ràng. Ví dụ: trong các ứng dụng RAG, cơ sở tri thức có thể trả về kết quả tìm kiếm không liên quan. Việc triển khai các rào cản với kiểm tra mức độ liên quan có thể giúp ngăn chặn các lỗi truy vấn này lan rộng sang phần còn lại của quy trình làm việc của tác nhân.

Các công cụ nên được thiết kế phù hợp với ranh giới cô lập lỗi để hạn chế tác động trong trường hợp xảy ra lỗi. Khi xây dựng các công cụ tùy chỉnh, hãy thiết kế mỗi công cụ thành một miền cô lập riêng. Khi sử dụng máy chủ MCP hoặc các công cụ hiện có, hãy đảm bảo bạn sử dụng các lược đồ yêu cầu/phản hồi nghiêm ngặt, có phiên bản và xác thực chúng tại ranh giới. Thêm các xác thực ngữ nghĩa như phạm vi ngày, quy tắc liên trường và kiểm tra độ mới của dữ liệu. Các công cụ nội bộ cũng có thể được triển khai trên các Vùng Khả dụng AWS khác nhau để tăng cường khả năng phục hồi.

Ở chiều hướng phối hợp, hãy triển khai các bộ ngắt mạch giám sát tỷ lệ lỗi và độ trễ, kích hoạt khi các phụ thuộc không khả dụng. Đặt giới hạn thử lại giới hạn với độ trễ lũy thừa và độ trễ dao động (jitter) để kiểm soát chi phí và xung đột. Để tăng cường khả năng phục hồi kết nối, hãy triển khai ánh xạ lỗi JSON-RPC mạnh mẽ và thời gian chờ cho mỗi cuộc gọi, đồng thời duy trì các nhóm kết nối lành mạnh đến các công cụ, máy chủ MCP và các dịch vụ hạ nguồn. Chiều hướng phối hợp cũng nên quản lý các phương án dự phòng tương thích với hợp đồng - định tuyến từ một công cụ hoặc máy chủ MCP bị lỗi sang các phương án thay thế - đồng thời duy trì các lược đồ nhất quán và cung cấp chức năng bị suy giảm.

Khi ranh giới cô lập bị lỗi, bạn có thể triển khai phương pháp giảm cấp nhẹ nhàng (duyên dáng) để duy trì chức năng cốt lõi trong khi các tính năng nâng cao không khả dụng. Hãy tiến hành kiểm tra khả năng phục hồi bằng cách tiêm lỗi cụ thể của AI, chẳng hạn như mô phỏng lỗi suy luận mô hình hoặc sự không nhất quán của cơ sở kiến ​​thức, để kiểm tra ranh giới cô lập trước khi sự cố xảy ra trong quá trình sản xuất.

### Không đủ năng lực
Tải quá mức có thể gây quá tải ngay cả với những hệ thống được trang bị tốt, có khả năng dẫn đến suy giảm hiệu suất hoặc lỗi hệ thống. Công suất đủ đảm bảo hệ thống của bạn có đủ tài nguyên cần thiết để xử lý cả lưu lượng dự kiến ​​và nhu cầu tăng đột biến bất ngờ.

Việc lập kế hoạch năng lực cho tác nhân AI bao gồm dự báo nhu cầu, đánh giá tài nguyên và phân tích hạn ngạch. Cân nhắc chính khi lập kế hoạch năng lực là ước tính Số yêu cầu mỗi phút (RPM) và Số mã thông báo mỗi phút (TPM). Tuy nhiên, việc ước tính RPM và TPM đặt ra những thách thức riêng do bản chất ngẫu nhiên của các tác nhân. Các tác nhân AI thường sử dụng xử lý đệ quy, trong đó công cụ suy luận của tác nhân liên tục gọi các FM cho đến khi đạt được câu trả lời cuối cùng. Điều này tạo ra hai khó khăn lớn trong việc lập kế hoạch. Thứ nhất, số lượng các cuộc gọi lặp lại khó dự đoán vì nó dựa trên độ phức tạp của tác vụ và các đường dẫn suy luận. Thứ hai, độ dài mã thông báo của mỗi cuộc gọi cũng khó dự đoán vì nó bao gồm lời nhắc của người dùng, hướng dẫn hệ thống, các bước suy luận do tác nhân tạo ra và lịch sử hội thoại. Hiệu ứng gộp này khiến việc lập kế hoạch năng lực cho các tác nhân trở nên khó khăn.

Thông qua phân tích heuristic trong quá trình phát triển, các nhóm có thể đặt ra giới hạn đệ quy hợp lý để giúp ngăn ngừa các vòng lặp dư thừa và tiêu thụ tài nguyên vượt mức. Ngoài ra, vì đầu ra của tác nhân trở thành đầu vào cho các lần đệ quy tiếp theo, việc quản lý mã thông báo hoàn thành tối đa giúp kiểm soát một thành phần của mức tiêu thụ mã thông báo ngày càng tăng trong các chuỗi suy luận đệ quy.

Các phương trình sau đây giúp chuyển đổi cấu hình tác nhân thành các ước tính năng lực này:
```
RPM = Average agent level thread per minute * average FM invocation per minute in one thread 
    = Average agent level thread per minute * (1 + 60/(max_completion_tokens/TPS))
```
Token mỗi giây (TPS) khác nhau đối với từng mô hình và có thể được tìm thấy trong tài liệu phát hành mô hình và kết quả chuẩn mực nguồn mở, chẳng hạn như phân tích nhân tạo.
```
TPM = RPM * Average input token length
    = RPM * (system prompt length + user prompt length + max_completion_tokens * (recursion_limit -1)/recursion_limit)
```
Tính toán này giả định rằng không có tính năng lưu trữ tạm thời nào được triển khai.

Không giống như các công cụ bên ngoài, nơi khả năng phục hồi được quản lý bởi các nhà cung cấp bên thứ ba, các công cụ được phát triển nội bộ dựa vào cấu hình phù hợp của nhóm phát triển để mở rộng quy mô dựa trên nhu cầu. Khi nhu cầu tài nguyên tăng đột biến, chỉ những công cụ bị ảnh hưởng mới cần mở rộng quy mô.

Ví dụ: các hàm AWS Lambda có thể được chuyển đổi thành các công cụ tương thích với MCP bằng Amazon Bedrock AgentCore Gateway . Nếu các công cụ phổ biến khiến các hàm Lambda đạt đến giới hạn dung lượng, bạn có thể tăng giới hạn thực thi đồng thời ở cấp tài khoản hoặc triển khai đồng thời được cung cấp để xử lý tải tăng thêm.

Đối với các tình huống liên quan đến nhiều nhóm hành động thực thi đồng thời, các điều khiển đồng thời dành riêng của hàm Lambda cung cấp khả năng cô lập tài nguyên thiết yếu bằng cách phân bổ dung lượng chuyên dụng cho từng nhóm hành động. Điều này giúp ngăn chặn việc một công cụ duy nhất chiếm hết tài nguyên khả dụng trong các lệnh gọi được dàn dựng, tạo điều kiện thuận lợi cho việc sử dụng tài nguyên cho các hàm có mức độ ưu tiên cao.

Khi đạt đến giới hạn dung lượng, bạn có thể sử dụng hàng đợi yêu cầu thông minh với phân bổ theo mức độ ưu tiên để đảm bảo các dịch vụ thiết yếu tiếp tục hoạt động. Việc triển khai hạ cấp nhẹ nhàng trong các giai đoạn tải cao có thể hữu ích. Điều này duy trì chức năng cốt lõi trong khi tạm thời giảm các tính năng không cần thiết.

### Độ trễ quá mức
Độ trễ quá mức làm ảnh hưởng đến trải nghiệm người dùng, giảm năng suất và làm suy yếu giá trị thực tế của các tác nhân AI trong quá trình sản xuất. Việc phát triển khối lượng công việc của tác nhân đòi hỏi sự cân bằng giữa tốc độ, chi phí và độ chính xác. Độ chính xác là nền tảng để các tác nhân AI chiếm được lòng tin của người dùng. Để đạt được độ chính xác cao, cần cho phép các tác nhân thực hiện nhiều lần lặp lại suy luận, điều này chắc chắn sẽ tạo ra những thách thức về độ trễ.

Việc quản lý kỳ vọng của người dùng trở nên vô cùng quan trọng—việc thiết lập các chỉ số mục tiêu mức dịch vụ (SLO) trước khi bắt đầu dự án sẽ đặt ra các mục tiêu thực tế cho thời gian phản hồi của tác nhân. Các nhóm nên xác định ngưỡng độ trễ cụ thể cho các khả năng khác nhau của tác nhân, chẳng hạn như phản hồi dưới một giây cho các truy vấn đơn giản so với thời gian phản hồi dài hơn cho các tác vụ phân tích đòi hỏi nhiều tương tác công cụ hoặc chuỗi suy luận mở rộng. Việc truyền đạt rõ ràng về thời gian phản hồi dự kiến ​​giúp tránh gây khó chịu cho người dùng và cho phép đưa ra các quyết định thiết kế hệ thống phù hợp.

Kỹ thuật nhanh chóng mang lại cơ hội lớn nhất để cải thiện độ trễ bằng cách giảm các vòng lặp suy luận không cần thiết. Các lời nhắc mơ hồ đưa tác nhân vào các chu kỳ cân nhắc kéo dài, trong khi các hướng dẫn rõ ràng giúp đẩy nhanh quá trình ra quyết định. Việc yêu cầu tác nhân "phê duyệt nếu trường hợp sử dụng có giá trị chiến lược" tạo ra một chuỗi suy luận phức tạp. Trước tiên, tác nhân phải xác định các tiêu chí giá trị chiến lược, sau đó đánh giá các tiêu chí nào được áp dụng, và cuối cùng xác định ngưỡng ý nghĩa. Ngược lại, việc nêu rõ các tiêu chí trong lời nhắc hệ thống có thể giảm đáng kể số lần lặp lại của tác nhân. Các ví dụ sau minh họa sự khác biệt giữa các hướng dẫn mơ hồ và rõ ràng.

Sau đây là một ví dụ về lệnh tác nhân mơ hồ:
```
You are a generative AI use case approver. 
Your role is to evaluate GenAI agent build requests by carefully analyzing user-provided 
information and make approval decisions. Please follow the following instructions: 
<instructions>
1. Carefully analyze the information provided by the user, and collect use case information, 
such as use case sponsor, significance of the use case, and potential values that it can bring. 
2. Approve the use case if it has a senior sponsor and is of strategic value. 
</instructions>
```
Sau đây là một ví dụ về hướng dẫn tác nhân rõ ràng, được định nghĩa rõ ràng:
```
You are a generative AI use case approver. 
Your role is to evaluate Gen AI agent build requests by carefully analyzing user-provided 
information and make approval decisions based on specific criteria. 
Please strictly follow the following instructions: 
<instructions>
1. Carefully analyze the information provided by the user. Collect answers to the following questions:
<question_1>Does the use case have a business sponsor that is VP level and above? </question_1>
<question_2>What value is this agent expected to deliver? The answer can be in the form of 
number of hours per month saved on certain tasks, or additional revenue values.</question_2>
<question_3>If the use case is external customer facing, please provide supporting information 
on the demand. </question_3>
2. Evaluate the request against these approval criteria:
<criteria_1>The use case has business sponsor at VP level and above. This is a hard criteria. </criteria_1>
<criteria_2>The use case can bring significant $ value, calculated by productivity gain or 
revenue increase. This is a soft criteria. </criteria_2>
<criteria_3>Have strong proof that the use case/feature is demanded by customers. This is a 
soft criteria. </criteria_3>
3. Based on the evaluation, make a decision to approve or deny the use case.
- Approve: If the hard criterion is met, and at least one of the soft criteria is met. 
- Deny: The hard criterion is not met, or neither of the soft criteria is met. 
</instructions>
```
Bộ nhớ đệm nhắc nhở giúp giảm đáng kể độ trễ bằng cách lưu trữ các tiền tố nhắc nhở lặp lại giữa các yêu cầu. Bộ nhớ đệm nhắc nhở Amazon Bedrock có thể giảm độ trễ tới 85% cho các mô hình được hỗ trợ, đặc biệt hữu ích cho các tác nhân có lời nhắc hệ thống dài và thông tin ngữ cảnh ổn định qua các phiên.

Xử lý không đồng bộ cho tác nhân và công cụ giúp giảm độ trễ bằng cách cho phép thực thi song song. Quy trình làm việc đa tác nhân đạt được tốc độ tăng đáng kể khi các tác nhân độc lập thực thi song song thay vì chờ hoàn tất tuần tự. Đối với các tác nhân có công cụ, xử lý không đồng bộ cho phép tiếp tục suy luận và chuẩn bị các hành động tiếp theo trong khi các công cụ thực thi ở chế độ nền, tối ưu hóa quy trình làm việc bằng cách chồng chéo xử lý nhận thức với các thao tác I/O.

Kiểm tra bảo mật và tuân thủ phải giảm thiểu tác động của độ trễ trong khi vẫn duy trì khả năng bảo vệ trên nhiều chiều. Các tác nhân kiểm duyệt nội dung triển khai quét tuân thủ luồng, đánh giá đầu ra của tác nhân trong quá trình tạo thay vì chờ phản hồi đầy đủ, đánh dấu nội dung có khả năng gây ra sự cố theo thời gian thực, đồng thời cho phép nội dung an toàn được truyền tải ngay lập tức.

### Phản hồi của tác nhân không chính xác
Đầu ra chính xác đảm bảo tác nhân AI của bạn hoạt động đáng tin cậy trong phạm vi đã xác định, cung cấp phản hồi chính xác và nhất quán, đáp ứng kỳ vọng của người dùng và yêu cầu kinh doanh. Tuy nhiên, cấu hình sai, lỗi phần mềm và ảo giác mô hình có thể làm giảm chất lượng đầu ra, dẫn đến phản hồi không chính xác, làm suy yếu niềm tin của người dùng.

Để cải thiện độ chính xác, hãy sử dụng các luồng điều phối xác định bất cứ khi nào có thể. Việc để các tác nhân dựa vào LLM để ứng biến trong quá trình thực hiện nhiệm vụ sẽ tạo ra nguy cơ đi chệch khỏi lộ trình dự định. Thay vào đó, hãy xác định các quy trình làm việc rõ ràng, chỉ rõ cách các tác nhân nên tương tác và sắp xếp các hoạt động của mình. Cách tiếp cận có cấu trúc này giúp giảm thiểu cả lỗi gọi giữa các tác nhân và lỗi gọi công cụ. Ngoài ra, việc triển khai các rào cản đầu vào và đầu ra giúp tăng cường đáng kể độ chính xác của tác nhân. Amazon Bedrock Guardrails có thể quét dữ liệu đầu vào của người dùng để kiểm tra tính tuân thủ trước khi gọi mô hình và cung cấp xác thực đầu ra để phát hiện ảo giác , phản hồi có hại , thông tin nhạy cảm và các chủ đề bị chặn .

Khi xảy ra sự cố về chất lượng phản hồi, bạn có thể triển khai xác thực trực tiếp cho các quyết định quan trọng đòi hỏi độ chính xác cao và triển khai cơ chế thử lại tự động với lời nhắc tinh chỉnh khi phản hồi ban đầu không đáp ứng tiêu chuẩn chất lượng.

### Điểm lỗi duy nhất
Dự phòng tạo ra nhiều con đường dẫn đến thành công bằng cách giảm thiểu các điểm lỗi đơn lẻ có thể gây suy yếu toàn hệ thống. Các điểm lỗi đơn lẻ làm suy yếu dự phòng khi nhiều thành phần phụ thuộc vào một tài nguyên hoặc dịch vụ duy nhất, tạo ra các lỗ hổng vượt qua ranh giới bảo vệ. Dự phòng hiệu quả đòi hỏi cả các thành phần dự phòng và các đường dẫn dự phòng, đảm bảo rằng nếu một thành phần bị lỗi, các thành phần thay thế có thể tiếp quản, và nếu một đường dẫn không khả dụng, lưu lượng có thể lưu thông qua các tuyến đường khác nhau.

Các tác nhân yêu cầu dự phòng phối hợp cho các FM của họ. Nếu các mô hình được tự quản lý, bạn có thể triển khai mô hình đa vùng với tính năng chuyển đổi dự phòng tự động. Khi sử dụng dịch vụ được quản lý, Amazon Bedrock cung cấp tính năng suy luận liên vùng để cung cấp dự phòng tích hợp cho các mô hình được hỗ trợ, tự động định tuyến yêu cầu đến các Vùng AWS thay thế khi điểm cuối chính gặp sự cố.

Chiều công cụ tác nhân phải phối hợp dự phòng công cụ để tạo điều kiện cho việc hạ cấp nhẹ nhàng khi các công cụ chính không khả dụng. Thay vì hoàn toàn thất bại, hệ thống nên tự động chuyển hướng sang các công cụ thay thế cung cấp chức năng tương tự, ngay cả khi chúng kém tinh vi hơn. Ví dụ: khi cơ sở kiến ​​thức của trợ lý trò chuyện nội bộ bị lỗi, nó có thể chuyển sang công cụ tìm kiếm để cung cấp kết quả thay thế cho người dùng.

Việc duy trì tính nhất quán của quyền trên các môi trường dự phòng là rất quan trọng. Điều này giúp ngăn ngừa các lỗ hổng bảo mật trong các tình huống chuyển đổi dự phòng. Do việc kiểm soát truy cập quá mức gây ra những rủi ro bảo mật đáng kể, việc xác thực cả quyền của người dùng cuối và quyền truy cập cấp công cụ đều giống nhau giữa các thành phần chính và thành phần chuyển đổi dự phòng là rất quan trọng. Tính nhất quán này đảm bảo các ranh giới bảo mật được duy trì bất kể môi trường nào đang chủ động phục vụ yêu cầu, giúp ngăn ngừa tình trạng leo thang đặc quyền hoặc truy cập trái phép có thể xảy ra khi hệ thống chuyển đổi giữa các mô hình cấp quyền khác nhau trong quá trình chuyển đổi vận hành.

## Sự xuất sắc trong vận hành: Tích hợp các hoạt động truyền thống và hoạt động cụ thể của AI
Sự xuất sắc trong vận hành AI agentic tích hợp các phương pháp DevOps đã được chứng minh với các yêu cầu cụ thể của AI để vận hành hệ thống agentic một cách đáng tin cậy trong môi trường sản xuất. Các quy trình tích hợp liên tục và phân phối liên tục (CI/CD) điều phối toàn bộ vòng đời của agent, và cơ sở hạ tầng dưới dạng mã (IaC) chuẩn hóa việc triển khai trên nhiều môi trường, giảm thiểu lỗi thủ công và cải thiện khả năng tái tạo.

Khả năng quan sát tác nhân đòi hỏi sự kết hợp giữa các số liệu truyền thống và các tín hiệu cụ thể của tác nhân, chẳng hạn như dấu vết suy luận và kết quả gọi công cụ. Mặc dù có thể lấy số liệu hệ thống và nhật ký truyền thống từ Amazon CloudWatch , việc theo dõi cấp độ tác nhân đòi hỏi phải xây dựng phần mềm bổ sung. Amazon Bedrock AgentCore Observability (bản xem trước) vừa được công bố gần đây hỗ trợ OpenTelemetry để tích hợp dữ liệu đo từ xa của tác nhân với các dịch vụ quan sát hiện có, bao gồm CloudWatch, Datadog , LangSmith và Langfuse . Để biết thêm chi tiết về các tính năng của Amazon Bedrock AgentCore Observability, hãy xem Ra mắt khả năng quan sát AI tạo sinh của Amazon CloudWatch (Bản xem trước) .

Ngoài việc giám sát, kiểm thử và xác thực tác nhân còn vượt ra ngoài các phương pháp phần mềm thông thường. Các bộ kiểm thử tự động như promptfoo giúp các nhóm phát triển cấu hình các bài kiểm thử để đánh giá chất lượng suy luận, hoàn thành tác vụ và tính nhất quán của hội thoại. Các kiểm tra trước khi triển khai xác nhận kết nối công cụ và khả năng truy cập kiến ​​thức, và tính năng chèn lỗi mô phỏng sự cố công cụ, lỗi API và sự không nhất quán dữ liệu để phát hiện các lỗi suy luận trước khi chúng ảnh hưởng đến người dùng.

Khi sự cố phát sinh, việc giảm thiểu dựa vào các cẩm nang bao gồm cả các vấn đề ở cấp độ cơ sở hạ tầng và từng tác nhân cụ thể. Các cẩm nang này hỗ trợ các phiên làm việc trực tiếp, cho phép chuyển giao liền mạch cho các tác nhân dự phòng hoặc người vận hành mà không làm mất ngữ cảnh.

## Bản tóm tắt
Trong bài viết này, chúng tôi đã giới thiệu một mô hình kiến ​​trúc bảy chiều để lập bản đồ các tác nhân AI của bạn và phân tích nơi xuất hiện rủi ro phục hồi. Chúng tôi cũng đã xác định năm chế độ lỗi phổ biến liên quan đến các tác nhân AI và các chiến lược giảm thiểu của chúng.

Các chiến lược này minh họa cách các nguyên tắc phục hồi áp dụng cho khối lượng công việc của các tác nhân chung, nhưng chúng không phải là tất cả. Mỗi hệ thống AI có những đặc điểm và mối phụ thuộc riêng. Bạn phải phân tích kiến ​​trúc cụ thể của mình trên bảy khía cạnh rủi ro để xác định các thách thức phục hồi trong khối lượng công việc của riêng mình, ưu tiên các lĩnh vực dựa trên tác động của người dùng và mức độ quan trọng của doanh nghiệp thay vì độ phức tạp về mặt kỹ thuật.

Khả năng phục hồi là một hành trình liên tục chứ không phải là đích đến. Khi các tác nhân AI của bạn phát triển và xử lý các trường hợp sử dụng mới, các chiến lược phục hồi của bạn cũng phải thay đổi tương ứng. Bạn có thể thiết lập các quy trình kiểm tra, giám sát và cải tiến thường xuyên để đảm bảo hệ thống AI của bạn luôn phục hồi khi mở rộng quy mô. Để biết thêm thông tin về các tác nhân AI tạo sinh và khả năng phục hồi trên AWS, vui lòng tham khảo các tài nguyên sau:

  * Kịch bản kỹ thuật hỗn loạn cho khối lượng công việc GenAI
  * Thiết kế khối lượng công việc AI tạo ra để có khả năng phục hồi
  * Giới thiệu Amazon Bedrock AgentCore: Triển khai và vận hành tác nhân AI một cách an toàn ở mọi quy mô (bản xem trước)
  * Triển khai các cơ chế ủy quyền dữ liệu hiệu quả để bảo mật dữ liệu của bạn được sử dụng trong các ứng dụng AI tạo sinh: Phần 1 và Phần 2

