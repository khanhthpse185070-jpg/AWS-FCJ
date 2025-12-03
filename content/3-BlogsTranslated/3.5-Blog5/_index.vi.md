---
title: "Blog 5"
 
weight: 1
chapter: false
pre: " <b> 3.6. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Hiện đại hóa việc điều phối thanh toán theo thời gian thực trên AWS
bởi Neeraj Kaushik, Subhash Sharma  trên01 THÁNG 10 NĂM 2025 trong Amazon API Gateway , Amazon CloudFront , Amazon Elastic Container Service , Amazon Elastic Kubernetes Service , Amazon Managed Streaming for Apache Kafka (Amazon MSK) , Kiến trúc , AWS Lambda , Mạng lưới đối tác AWS , Triển khai giải pháp AWS , Dịch vụ tài chính , Giải pháp đối tác , Khu vực công , Đối tác khu vực công , Khu vực Liên kết cố định| Bình luận |Chia sẻ

Thị trường thanh toán thời gian thực toàn cầu đang có sự tăng trưởng đáng kể. Theo Fortune Business Insights , thị trường này được định giá 24,91 tỷ USD vào năm 2024 và dự kiến ​​sẽ tăng lên 284,49 tỷ USD vào năm 2032, với tốc độ tăng trưởng kép hàng năm (CAGR) là 35,4%. Tương tự, Grand View Research báo cáo rằng thị trường thanh toán di động toàn cầu, được định giá 88,50 tỷ USD vào năm 2024, dự kiến ​​sẽ tăng trưởng với tốc độ CAGR là 38,0% từ năm 2025 đến năm 2030. (Lưu ý: Nghiên cứu thị trường và số liệu thống kê của bên thứ ba chỉ nhằm mục đích cung cấp thông tin. AWS và IBM không đưa ra bất kỳ tuyên bố nào về tính chính xác của thông tin này.)

Sự mở rộng nhanh chóng này nhấn mạnh tính cấp thiết của việc các tổ chức tài chính hiện đại hóa cơ sở hạ tầng xử lý thanh toán. Các tổ chức tài chính thường cần xử lý khối lượng giao dịch lớn với độ trễ gần như bằng không để đáp ứng các thỏa thuận mức dịch vụ (SLA) nghiêm ngặt nhằm hỗ trợ khối lượng thanh toán di động đang tăng vọt.

Tuy nhiên, các hệ thống điều phối thanh toán truyền thống, thường được xây dựng trên kiến ​​trúc đơn khối, gặp khó khăn trong việc đáp ứng những yêu cầu này do độ trễ, tính khả dụng và khả năng mở rộng. Ngoài ra, việc phụ thuộc vào cơ sở hạ tầng tại chỗ dẫn đến chi phí cao hơn và cản trở sự đổi mới, làm gia tăng nhu cầu hiện đại hóa.

Khi tính bền vững trở thành ưu tiên hàng đầu, các tổ chức đang chuyển sang các giải pháp đám mây để tối ưu hóa cơ sở hạ tầng, giảm lượng khí thải carbon và nâng cao hiệu quả sử dụng năng lượng. Sự chuyển đổi này mang lại khả năng mở rộng và hiệu suất, đồng thời phù hợp với các mục tiêu phát triển bền vững toàn cầu, đảm bảo tương lai của thanh toán theo thời gian thực.

Trong bài viết này, chúng tôi thảo luận về khuôn khổ điều phối thanh toán thời gian thực. Khung này sử dụng kiến ​​trúc hướng sự kiện và các dịch vụ không máy chủ của AWS để nâng cao khả năng phục hồi, hiệu quả và khả năng mở rộng của thanh toán thời gian thực. Bằng cách phân tách quy trình thanh toán thành các năng lực kinh doanh riêng biệt, các tổ chức tài chính có thể cải thiện tính mô-đun và tính linh hoạt. Việc triển khai phân tách dựa trên đối tượng thuê giúp cô lập và bảo mật dữ liệu. Ngoài ra, việc áp dụng giao tiếp bất đồng bộ thông qua Amazon Managed Streaming for Apache Kafka (Amazon MSK) giúp tăng cường khả năng mở rộng và khả năng phục hồi.

## Điều phối thanh toán theo thời gian thực truyền thống
Hệ thống điều phối thanh toán đóng vai trò là một giải pháp phần mềm trung gian, hợp lý hóa quy trình xử lý giao dịch trên nhiều phương thức thanh toán, cổng thanh toán và tổ chức tài chính. Hệ thống này điều phối các chức năng kinh doanh chính như ủy quyền thanh toán, xử lý thanh toán, thanh toán và bù trừ, tuân thủ và quản lý rủi ro, cũng như quản lý tài khoản cho cả luồng thanh toán đến và đi.

Sơ đồ sau đây mô tả các khả năng kinh doanh cấp cao được hỗ trợ bởi các đơn vị điều phối thanh toán trên nhiều luồng thanh toán khác nhau, bao gồm thanh toán theo thời gian thực, giải ngân kỹ thuật số, thanh toán thuế, chuyển khoản, v.v.
![picture 1](/images/image2.png)


Sơ đồ luồng chi tiết mô tả hệ thống xử lý thanh toán với nhiều thành phần. Sơ đồ hiển thị các loại hình thanh toán chính ở trên cùng (bao gồm Thanh toán theo thời gian thực, Giải ngân kỹ thuật số, Chuyển khoản tín dụng và Thanh toán ngang hàng) theo thứ tự từ trên xuống dưới qua các giai đoạn xử lý cốt lõi bao gồm Chấp nhận thanh toán, Thực hiện, Bù trừ, Báo cáo, Theo dõi, Hoàn trả và Thanh toán.

Nhiều tổ chức tài chính áp dụng phương pháp tiếp cận dựa trên đối tượng thuê được tổ chức theo khu vực địa lý do quy trình thanh toán bù trừ, quy định địa phương và yêu cầu giao dịch khác nhau giữa các Vùng AWS. Tuy nhiên, do không phân tách dịch vụ hợp lý, các nhóm thường tiếp tục thêm logic riêng theo vùng vào các dịch vụ hiện có, dần dần làm tăng độ phức tạp của hệ thống và sử dụng cùng một cơ sở hạ tầng cho tất cả các luồng thanh toán.

Các hệ thống thanh toán truyền thống xử lý giao dịch theo phương pháp tuyến tính, mỗi bước chờ bước trước đó hoàn tất. Tuy nhiên, phân tích quy trình thanh toán cho thấy nhiều cơ hội thực hiện song song:

  * Kiểm tra lệnh trừng phạt và phát hiện gian lận – Kiểm tra tuân thủ và gian lận có thể chạy đồng thời với các quyết định định tuyến ban đầu, thay vì chặn tuần tự tất cả các quá trình xử lý tiếp theo
  * Yêu cầu định tuyến và ủy quyền thanh toán – Khi các xác thực cơ bản hoàn tất, định tuyến và ủy quyền có thể tiến hành song song thay vì lần lượt
  * Thực hiện thanh toán và cập nhật sổ cái – Việc thực hiện thanh toán thực tế không cần phải chờ hồ sơ sổ cái được cập nhật—những việc này có thể diễn ra đồng thời
  * Thanh toán, đối chiếu và theo dõi – Các quy trình sau giao dịch này có thể được khởi tạo độc lập ngay khi giao dịch chính hoàn tất

Phương pháp song song này có thể cải thiện đáng kể thông lượng và giảm độ trễ so với các hệ thống dựa trên hàng đợi truyền thống, trong đó các hoạt động tạo thành chuỗi tuần tự kéo dài thời gian xử lý và tạo ra tình trạng tắc nghẽn.

Hầu hết các hệ thống điều phối thanh toán cũ đều phụ thuộc rất nhiều vào máy ảo (VM) tại chỗ, dẫn đến một số thách thức:

  * Hỗ trợ đa vùng cho việc phục hồi sau thảm họa và đa thuê bao dẫn đến chi phí vốn và chi phí hoạt động đáng kể
  * Các vấn đề về độ trễ cao và SLA do xử lý tin nhắn tuần tự và sự chậm trễ giữa các trung tâm dữ liệu tách biệt trên toàn cầu
  * Khả năng tái sử dụng hạn chế của luồng thanh toán vì kiến ​​trúc đơn khối yêu cầu thay đổi theo từng khu vực đối với cơ chế và quy định thanh toán cục bộ, làm tăng tính phức tạp và chi phí
  * Thách thức về khả năng mở rộng và mức tiêu thụ bộ nhớ cao do sử dụng tài nguyên không hiệu quả và thực thi logic không liên quan trên nhiều vùng
  * Lộ trình thanh toán xuyên biên giới phức tạp do sự thay đổi trong các quy tắc thanh toán bù trừ, giới hạn giao dịch và quy định địa phương, làm tăng độ trễ và lỗi định tuyến
  * Thách thức tích hợp với nhiều định dạng dữ liệu khác nhau vì các hệ thống cũ dựa trên các tiêu chuẩn độc quyền (ví dụ: ISO 20022, SWIFT MT), làm phức tạp việc chuyển đổi và tuân thủ dữ liệu
  * Độ phức tạp triển khai cao đối với các luồng thanh toán mới do kiến ​​trúc đơn khối yêu cầu sửa đổi rộng rãi theo từng khu vực, làm chậm thời gian đưa ra thị trường
  * Tác động môi trường và lượng khí thải carbon cao từ cơ sở hạ tầng tại chỗ tiêu thụ quá nhiều năng lượng, trong khi các phương pháp dựa trên đám mây cải thiện hiệu quả
## Tổng quan về giải pháp
Để vượt qua những thách thức này, kiến ​​trúc đề xuất áp dụng các nguyên tắc thiết kế sau để xây dựng giải pháp điều phối thanh toán theo thời gian thực, sẵn sàng cho tương lai:

  * Hiệu suất theo quy mô – Xử lý hơn 1.000 giao dịch mỗi giây (TPS) với độ trễ thấp ổn định trong các điều kiện tải khác nhau.
  * Tính khả dụng cao – Đạt thời gian hoạt động 99,999% để đáp ứng các yêu cầu nghiêm ngặt của giao dịch tài chính.
  * Khả năng phục hồi về mặt địa lý – Hỗ trợ hoạt động toàn cầu tuân thủ theo từng khu vực cụ thể trong khi vẫn duy trì hiệu suất nhất quán.
  * Tối ưu hóa chi phí – Giảm tổng chi phí sở hữu thông qua việc sử dụng tài nguyên hiệu quả và công nghệ không máy chủ.
  * Bảo mật và tuân thủ – Hỗ trợ bảo vệ dữ liệu và tuân thủ quy định trên nhiều khu vực pháp lý khác nhau.
  * Đơn giản hóa hoạt động – Tinh giản việc triển khai, giám sát và bảo trì trên toàn bộ hệ sinh thái thanh toán.
  * Dịch vụ vi mô – Phân tách quy trình thanh toán thành các chức năng kinh doanh riêng biệt, giúp các tổ chức tài chính cải thiện tính mô-đun và tính linh hoạt. Phương pháp tiếp cận dựa trên dịch vụ vi mô này cho phép mở rộng quy mô và phát triển độc lập các thành phần quan trọng.

Sơ đồ sau đây mô tả kiến ​​trúc giải pháp cấp cao cho thanh toán thời gian thực. Các kênh hiện có sử dụng API đồng bộ hoặc không đồng bộ có thể được điều chỉnh để sử dụng các điểm cuối được tối ưu hóa biên nhằm giảm độ trễ.
![picture 2](/images/image3.png)

Hệ thống điều phối thanh toán theo sự kiện với các kênh pub/sub kết nối nhiều mô-đun xử lý thanh toán
Sơ đồ kiến ​​trúc mô tả chi tiết nền tảng điều phối thanh toán dựa trên AWS, sử dụng các nguyên tắc hướng sự kiện. Nền tảng này bao gồm các thành phần có thể tái sử dụng trên hai vùng, với các mô-đun chuyên dụng cho việc khởi tạo, thực hiện, đối chiếu, lập hóa đơn và quản lý rủi ro. Triển khai các mẫu tin nhắn pub/sub cho giao tiếp giữa các thành phần và kết nối với các hệ thống doanh nghiệp bao gồm kế toán, tuân thủ và phân tích.

Kiến trúc hướng sự kiện được sử dụng để điều phối thanh toán, xử lý giao tiếp thông qua mô hình pub/sub. Kiến trúc này duy trì các kết nối liên tục, cải thiện hiệu suất xử lý thanh toán theo thời gian thực từ đầu đến cuối.

Kiến trúc hướng sự kiện cho xử lý thanh toán thời gian thực cho phép nhiều hoạt động thanh toán diễn ra đồng thời bằng cách sử dụng các bộ điều hợp khác nhau, trái ngược với các hệ thống truyền thống, nơi các quy trình thanh toán diễn ra tuần tự và chạy qua một đường ống duy nhất. Các sự kiện thanh toán được phân phối đến các vi dịch vụ xử lý thanh toán chuyên biệt dựa trên chức năng của chúng (khởi tạo, thực thi, theo dõi, thanh toán), cho phép mỗi vi dịch vụ xử lý độc lập mà không cần chờ các vi dịch vụ khác hoàn tất.

Vì chúng ta đang chuyển đổi từ xử lý tuần tự sang phân tán, việc duy trì khả năng truy xuất giao dịch là rất quan trọng. Các bộ điều hợp theo dõi thanh toán được hiển thị trong sơ đồ trước kết nối với các hệ thống phân tích doanh nghiệp, tạo ra một lớp chuyên biệt để giám sát giao dịch. Mô hình pub/sub cho phép gắn ID tương quan vào các sự kiện, cho phép hệ thống theo dõi các sự kiện liên quan trên các chủ đề và giai đoạn xử lý khác nhau.

Một lược đồ sự kiện được chuẩn hóa đóng vai trò là nền tảng cho kiến ​​trúc này, đảm bảo tính nhất quán giữa các triển khai khu vực, đồng thời cho phép tùy chỉnh ở cấp bộ điều hợp. Lược đồ này xác định các cấu trúc sự kiện thống nhất chứa siêu dữ liệu dành riêng cho từng đối tượng thuê bao và hỗ trợ quản lý phiên bản để đáp ứng các yêu cầu luôn thay đổi. Bằng cách tách biệt các biến thể cụ thể theo khu vực với lớp bộ điều hợp, giải pháp duy trì chức năng cốt lõi đồng thời tương tác với các hệ thống doanh nghiệp đa dạng thông qua tùy chỉnh theo cấu hình thay vì thay đổi mã.

Đối với hầu hết các quy trình thanh toán, đặc biệt là những quy trình có các bước xử lý độc lập có thể chạy song song, kiến ​​trúc này mang lại hiệu suất ròng cao hơn mặc dù có chi phí chuyển đổi chủ đề, đặc biệt là đối với các giao dịch phức tạp yêu cầu nhiều bước xác thực hoặc xử lý độc lập.

## Triển khai trên Đám mây AWS
Giải pháp sử dụng Amazon API Gateway được tối ưu hóa theo biên cho các kênh. Điểm cuối API được tối ưu hóa theo biên sẽ định tuyến các yêu cầu đến Điểm Hiện diện (POP) Amazon CloudFront gần nhất , có thể hỗ trợ trong trường hợp khách hàng của bạn phân tán về mặt địa lý để cho phép định tuyến hiệu quả trong từng khu vực địa lý, tăng cường khả năng phản hồi toàn cầu bằng cách giảm thiểu vòng lặp mạng và đảm bảo các yêu cầu đi theo đường dẫn ngắn nhất có thể trước khi chuyển từ internet công cộng sang mạng máy khách.


Kiến trúc thanh toán AWS đa vùng với các chủ đề Kafka được quản lý kết nối các dịch vụ vi mô Lambda và lưu trữ DynamoDB
Giải pháp điều phối thanh toán AWS toàn diện, áp dụng các nguyên tắc kiến ​​trúc đám mây gốc hiện đại. Logic xử lý cốt lõi được triển khai dưới dạng các hàm Lambda, bao gồm quy trình khởi tạo, thực thi, đối chiếu, lập hóa đơn, theo dõi, quản lý rủi ro và thanh toán. Tận dụng Amazon MSK để truyền phát sự kiện đáng tin cậy giữa các thành phần, với các chủ đề Kafka chuyên dụng cho từng giai đoạn xử lý. Tính bền vững dữ liệu được xử lý bởi Amazon DynamoDB, hỗ trợ các hoạt động liên vùng. Kiến trúc thể hiện các phương pháp hay nhất của AWS dành cho dịch vụ tài chính, bao gồm dự phòng khu vực, điện toán không máy chủ, dịch vụ được quản lý và các mẫu thiết kế hướng sự kiện. Hệ thống tích hợp với cơ sở hạ tầng ngân hàng bên ngoài và các hệ thống doanh nghiệp, đồng thời duy trì việc phân tách các mối quan tâm thông qua kiến ​​trúc vi dịch vụ. Hỗ trợ tích hợp cho việc giám sát tuân thủ, quản lý rủi ro và theo dõi thanh toán thông qua các hàm Lambda chuyên biệt.

Giải pháp sử dụng Amazon MSK để triển khai kiến ​​trúc hướng sự kiện, xử lý hiệu quả cả lưu lượng kênh đến và đi thông qua các yêu cầu API và các sự kiện dựa trên tin nhắn không đồng bộ. Amazon MSK giao tiếp bằng giao thức nhị phân hiệu suất cao giữa nhà sản xuất, người tiêu dùng và nhà môi giới, mang lại độ trễ thấp và thông lượng cao. Các khoản thanh toán theo thời gian thực được phân vùng hợp lý trên nhiều đối tượng thuê bao trong các khu vực địa lý—Bắc Mỹ, EMEA, LATAM và Châu Á - Thái Bình Dương.

Mỗi đối tượng thuê thanh toán theo thời gian thực đều tuân theo chiến lược phục hồi thảm họa chủ động/chủ động bằng cách triển khai các cụm MSK trên nhiều Vùng AWS, được thiết kế để đạt được tính khả dụng và khả năng phục hồi cao. Amazon MSK cung cấp cả tùy chọn cụm không máy chủ và cụm được cung cấp. Nhóm có thể quyết định chọn một trong hai tùy chọn tùy thuộc vào yêu cầu không chức năng và chuyên môn của nhóm. Amazon MSK tự động quản lý quyền lãnh đạo phân vùng với các lãnh đạo trong các Vùng chính và các người theo dõi trong các Vùng phụ. Trong quá trình chuyển đổi dự phòng, các lãnh đạo được bầu lại trong các Vùng khỏe mạnh, được thiết kế để giúp duy trì khả năng xử lý trong các sự cố khu vực. Phân vùng cố định sử dụng hàm băm nhất quán để định tuyến xác định và cân bằng lại hợp tác cho phép chuyển đổi dự phòng hiệu quả. Triển khai nhiều Vùng sẵn sàng cung cấp dự phòng vùng và các cụm bị cô lập trên mỗi Vùng để tuân thủ chủ quyền dữ liệu thông qua các ranh giới AWS Identity and Access Management (IAM) và đám mây riêng ảo (VPC) theo chương trình.

Để hỗ trợ sao chép liên vùng liền mạch và duy trì tính liên tục của tin nhắn, Amazon MSK Replicator — một tính năng được quản lý hoàn toàn của Amazon MSK — được sử dụng để sao chép các chủ đề và đồng bộ hóa các offset nhóm người dùng trên các cụm. MSK Replicator đơn giản hóa quy trình xây dựng các ứng dụng Kafka đa vùng bằng cách không cần mã tùy chỉnh, cấu hình công cụ nguồn mở hay quản lý cơ sở hạ tầng. Nó tự động cung cấp và mở rộng các tài nguyên cần thiết, giúp các nhóm có thể tập trung vào logic kinh doanh trong khi chỉ phải trả tiền cho dữ liệu đang được sao chép. Trong trường hợp mất điện hoặc chuyển đổi dự phòng trong vùng, lưu lượng có thể được tự động chuyển hướng đến một Vùng hoạt động bình thường mà không bị mất dữ liệu hoặc gián đoạn dịch vụ, đảm bảo Mục tiêu Thời gian Phục hồi (RTO) gần như bằng không và hoạt động không bị gián đoạn cho các dịch vụ hạ nguồn như bộ xử lý thanh toán và người dùng theo dõi kiểm toán.

Ngoài tính dự phòng theo vùng, kiến ​​trúc này còn sử dụng kiến ​​trúc hướng sự kiện để cho phép xử lý song song và tách biệt các giao dịch thanh toán. Các sự kiện như khởi tạo, xác thực và thanh toán giao dịch được phát ra không đồng bộ và được xử lý độc lập bởi nhiều dịch vụ vi mô khác nhau, giúp giảm đáng kể độ trễ từ đầu đến cuối.

Để xử lý các sự kiện này ở quy mô lớn, kiến ​​trúc có thể sử dụng AWS Lambda , Amazon Elastic Container Service (Amazon ECS) hoặc Amazon Elastic Kubernetes Service (Amazon EKS) tùy thuộc vào các yêu cầu phi chức năng. Việc tự động mở rộng quy mô sẽ phản hồi các số liệu của Amazon CloudWatch , và logic thử lại theo kiểu lùi theo cấp số nhân với hàng đợi ký tự chết (DLQ) sẽ xử lý các tình huống điều tiết. Bộ ngắt mạch ngăn ngừa lỗi tầng trong trường hợp tỷ lệ lỗi cao.

Một trong những lợi ích chính của giải pháp là khả năng tái sử dụng luồng thanh toán giữa các khu vực khác nhau. Mặc dù mỗi khu vực có các yêu cầu tuân thủ và quy tắc thanh toán riêng, nhưng các chức năng cốt lõi của thanh toán thời gian thực (ủy quyền thanh toán, xử lý thanh toán, thanh toán và bù trừ) phần lớn tương tự nhau. Khả năng tái sử dụng này cho phép triển khai nhanh chóng các giải pháp thanh toán trên các khu vực mới mà không cần phải thiết kế lại toàn bộ hệ thống. Ví dụ: hệ thống thanh toán thời gian thực ở Hoa Kỳ và Vương quốc Anh có thể chia sẻ logic nghiệp vụ tương tự cho thanh toán gộp thời gian thực nhưng khác nhau về các yêu cầu bù trừ và tuân thủ. Giải pháp xử lý những điều này như các ngữ cảnh bị ràng buộc trong kiến ​​trúc vi dịch vụ, mang lại sự linh hoạt đồng thời đảm bảo mỗi khu vực có thể xử lý các quy tắc và quy định riêng của mình.

## Tính bền vững
AWS không ngừng đổi mới thiết kế, xây dựng và vận hành cơ sở hạ tầng để hướng tới mục tiêu không phát thải carbon vào năm 2040 và tiết kiệm nước vào năm 2030. Amazon MSK với các phiên bản dựa trên AWS Graviton sử dụng ít hơn tới 60% năng lượng so với các phiên bản M5 tương đương, giúp bạn đạt được các mục tiêu phát triển bền vững. Lambda vốn dĩ đã bền vững ngay từ thiết kế. Mô hình không máy chủ của nó đảm bảo tài nguyên tính toán chỉ được sử dụng khi cần thiết, giảm đáng kể cơ sở hạ tầng nhàn rỗi và năng lượng lãng phí. Thay vì duy trì máy chủ luôn hoạt động cho các tác vụ không thường xuyên, Lambda cung cấp năng lượng tính toán tức thời, đạt được khả năng nhàn rỗi gần như bằng không.

## Bảo mật và tuân thủ trong dịch vụ tài chính
Do tính chất nhạy cảm của các giao dịch thanh toán và dữ liệu tài chính, bạn nên áp dụng các biện pháp kiểm soát bảo mật cần thiết để đáp ứng các quy định về tài chính như AWS PCI DSS và AWS Federal Information Processing Standard (FIPS) 140-3 theo nhu cầu của tổ chức bạn.

Giải pháp này nên kết hợp các biện pháp kiểm soát bảo mật đa lớp, giám sát liên tục và kiểm toán tuân thủ tự động để đáp ứng các kỳ vọng khắt khe của cơ quan quản lý ngân hàng và các nhóm quản lý rủi ro nội bộ. Để biết thêm thông tin, vui lòng tham khảo Hướng dẫn Bảo mật .

## Phần kết luận
Việc hiện đại hóa các hệ thống điều phối thanh toán bằng kiến ​​trúc hướng sự kiện và công nghệ không máy chủ AWS đánh dấu một bước tiến đáng kể trong việc đáp ứng nhu cầu của bối cảnh dịch vụ tài chính đang phát triển nhanh chóng hiện nay. Giải pháp này giải quyết những thách thức chính mà các hệ thống thanh toán truyền thống phải đối mặt, đồng thời mang lại những lợi ích đáng kể về hiệu suất, khả năng mở rộng, tối ưu hóa chi phí, khả năng phục hồi toàn cầu, tính bền vững và khả năng tuân thủ. Bằng cách sử dụng công nghệ đám mây tiên tiến và các biện pháp kiểm soát bảo mật mạnh mẽ, các tổ chức tài chính giờ đây có thể xây dựng một nền tảng sẵn sàng cho tương lai, thích ứng với các nhu cầu kinh doanh đang phát triển đồng thời duy trì các tiêu chuẩn cao nhất về hiệu suất, bảo mật và độ tin cậy. Khi thị trường thanh toán thời gian thực tiếp tục tăng trưởng bùng nổ, kiến ​​trúc hiện đại này cung cấp một giải pháp đáp ứng nhu cầu hiện tại và cũng có vị thế tốt để hỗ trợ các đổi mới thanh toán trong tương lai. Các tổ chức đang tìm cách hiện đại hóa cơ sở hạ tầng thanh toán của mình có thể sử dụng bản thiết kế này để đẩy nhanh hành trình chuyển đổi số, hỗ trợ xử lý thanh toán bền vững, an toàn và hiệu quả ở quy mô lớn trong một thị trường toàn cầu ngày càng cạnh tranh.

Kiến trúc được trình bày ở đây chỉ mang tính chất tham khảo. IBM sẽ hợp tác chặt chẽ với bạn để triển khai giải pháp theo các tiêu chuẩn ngành và yêu cầu tuân thủ. Để biết thêm tài nguyên, vui lòng tham khảo:

  * IBM Consulting trên AWS
  * AWS dành cho dịch vụ tài chính
  * Chuyển đổi giao dịch: Tinh giản việc tuân thủ PCI bằng kiến ​​trúc không máy chủ AWS
  * Các phương pháp hay nhất để điều chỉnh kích thước cụm Apache Kafka của bạn sao cho tối ưu hóa hiệu suất và chi phí
  * Cách chọn loại cụm Amazon MSK phù hợp với bạn
  * Mô hình trách nhiệm chung của AWS
  * Tiêu chuẩn xử lý thông tin liên bang AWS (FIPS) 140-3
  * Tính bền vững với AWS Graviton
  * AWS PCI DSS

IBM Consulting là Đối tác Dịch vụ Cấp độ Premier của AWS, hỗ trợ khách hàng sử dụng AWS khai thác sức mạnh của đổi mới sáng tạo và thúc đẩy chuyển đổi kinh doanh. IBM Consulting được công nhận là Nhà tích hợp Hệ thống Toàn cầu (GSI) cho hơn 22 năng lực, bao gồm Tư vấn Dịch vụ Tài chính. Để biết thêm thông tin, vui lòng liên hệ với Đại diện IBM .

## Về tác giả
![picture 2](/images/image4.png)
Neeraj Kaushik là Đại sứ AWS và Trưởng nhóm Phát triển Khách hàng, làm việc tại IBM Financial Services. Ông là Kiến trúc sư Xuất sắc được Chứng nhận bởi Open Group với hai thập kỷ kinh nghiệm CNTT trong các vai trò triển khai dịch vụ khách hàng trải dài trên nhiều ngành nghề, bao gồm du lịch và vận tải, ngân hàng, bán lẻ, giáo dục, chăm sóc sức khỏe và phòng chống buôn người. Là một cố vấn đáng tin cậy, ông làm việc trực tiếp với giám đốc điều hành và kiến ​​trúc sư khách hàng về chiến lược kinh doanh để xác định lộ trình công nghệ. Là một Kiến trúc sư Chuyên nghiệp được Chứng nhận bởi AWS và Chuyên gia Xử lý Ngôn ngữ Tự nhiên, ông đã lãnh đạo nhiều chương trình hiện đại hóa đám mây phức tạp và các sáng kiến ​​AI.
![picture 2](/images/image5.png)
Subhash Sharma là Kiến trúc sư Giải pháp Đối tác Cấp cao tại AWS. Ông có hơn 25 năm kinh nghiệm trong việc cung cấp các sản phẩm phần mềm phân tán, có khả năng mở rộng, tính khả dụng cao và bảo mật, sử dụng các dịch vụ vi mô, AI/ML, Internet vạn vật (IoT) và blockchain theo phương pháp DevSecOps. Trong thời gian rảnh rỗi, Subhash thích dành thời gian cho gia đình và bạn bè, đi bộ đường dài, dạo biển và xem TV.