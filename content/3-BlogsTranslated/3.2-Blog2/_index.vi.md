---
title: "Blog 2"
 
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Các tác nhân như thang cuốn: Giám sát video AI thời gian với Amazon Bedrock và luồng video 

Bởi Kiowa Jackson và Piotr | Chotkowski 07 tháng 7 năm 2025 | trong Amazon Bedrock , Amazon Bedrock Agents , Amazon Kinesis , Amazon Machine Learning , Analytics , Artificial Intelligence , Intermediate (200) , Kinesis Video Streams, Permalink,  Comment, Share

Các tổ chức triển khai hệ thống giám sát video phải đối mặt với một thách thức quan trọng: xử lý các luồng video liên tục trong khi vẫn duy trì nhận thức tình huống chính xác. Các phương pháp giám sát truyền thống sử dụng phát hiện dựa trên quy tắc hoặc thị giác máy tính cơ bản thường bỏ sót các sự kiện quan trọng hoặc tạo ra quá nhiều báo động giả, dẫn đến hoạt động kém hiệu quả và gây mệt mỏi cho hệ thống cảnh báo.

Trong bài viết này, chúng tôi sẽ trình bày cách xây dựng một giải pháp triển khai hoàn chỉnh, xử lý luồng video bằng OpenCV , Amazon Bedrock để hiểu ngữ cảnh và phản hồi tự động thông qua Amazon Bedrock Agents . Giải pháp này mở rộng các khả năng đã được chứng minh trong bài viết Tự động hóa chatbot để truy xuất tài liệu và dữ liệu bằng Amazon Bedrock Agents và Cơ sở tri thức , trong đó thảo luận về việc sử dụng Amazon Bedrock Agents để truy xuất tài liệu và dữ liệu. Trong bài viết này, chúng tôi áp dụng Amazon Bedrock Agents vào phân tích video thời gian thực và giám sát sự kiện.


## Lợi ích của việc sử dụng Amazon Bedrock Agents để giám sát video

Hình sau đây minh họa các luồng video đầu vào từ các tình huống giám sát khác nhau. Với khả năng hiểu bối cảnh, người dùng có thể tìm kiếm các sự kiện cụ thể.
![picture 1](/images/image3.2.1.png)
Camera cửa trước có thể ghi lại nhiều sự kiện trong ngày, nhưng có một số sự kiện thú vị hơn những sự kiện khác—việc có bối cảnh khi một gói hàng được giao hoặc lấy đi (như trong ví dụ về gói hàng sau đây) sẽ giới hạn cảnh báo đối với các sự kiện khẩn cấp.
![picture 2](/images/image3.2.2.png)
Amazon Bedrock là một dịch vụ được quản lý hoàn toàn, cung cấp quyền truy cập vào các mô hình nền tảng (FM) hiệu suất cao từ các công ty AI hàng đầu thông qua một API duy nhất. Sử dụng Amazon Bedrock, bạn có thể xây dựng các ứng dụng AI tạo sinh an toàn và có trách nhiệm. Amazon Bedrock Agents mở rộng các khả năng này bằng cách cho phép các ứng dụng thực hiện các tác vụ nhiều bước trên các hệ thống và nguồn dữ liệu, lý tưởng cho các tình huống giám sát phức tạp. Giải pháp xử lý luồng video thông qua các bước chính sau:

1.	Trích xuất khung hình khi phát hiện chuyển động từ luồng video trực tiếp hoặc tệp cục bộ.
2.	Phân tích bối cảnh bằng FM đa phương thức
3.	Đưa ra quyết định bằng logic dựa trên tác nhân với các phản hồi có thể cấu hình được.
4.	Duy trì bộ nhớ ngữ nghĩa có thể tìm kiếm được của các sự kiện.
Bạn có thể xây dựng hệ thống giám sát video thông minh này bằng cách sử dụng Amazon Bedrock Agents và Amazon Bedrock Knowledge Bases trong một giải pháp tự động. Mã nguồn đầy đủ có sẵn trong GitHub repo.

## Những hạn chế của hệ thống giám sát video hiện tại

Các tổ chức triển khai hệ thống giám sát video đang đối mặt với một tình thế tiến thoái lưỡng nan. Bất chấp những tiến bộ trong công nghệ camera và khả năng lưu trữ, lớp thông minh (intelligent layer) xử lý dữ liệu video thường vẫn còn thô sơ. Điều này tạo ra một tình huống khó khăn, đòi hỏi các đội ngũ an ninh phải đánh đổi đáng kể trong phương pháp giám sát của mình. Các giải pháp giám sát video hiện tại thường buộc các tổ chức phải lựa chọn giữa những điều sau:

  * Các quy tắc đơn giản có thể mở rộng nhưng tạo ra quá nhiều kết quả dương tính giả
  * Các quy tắc phức tạp đòi hỏi phải bảo trì và tùy chỉnh liên tục
  * Giám sát thủ công dựa vào sự chú ý của con người và không mở rộng quy mô
  * Các giải pháp điểm chỉ xử lý các tình huống cụ thể nhưng thiếu tính linh hoạt

Những đánh đổi này tạo ra những rào cản cơ bản cho việc giám sát video hiệu quả, ảnh hưởng đến an ninh, an toàn và hiệu quả hoạt động trong nhiều ngành. Dựa trên kinh nghiệm làm việc với khách hàng, chúng tôi đã xác định ba thách thức quan trọng phát sinh từ những hạn chế này:

  * Mệt mỏi vì cảnh báo – Các hệ thống phát hiện chuyển động và nhận dạng vật thể truyền thống sẽ tạo ra cảnh báo cho bất kỳ thay đổi hoặc vật thể nào được phát hiện. Các nhóm an ninh nhanh chóng bị quá tải bởi khối lượng thông báo cho các hoạt động thông thường. Điều này dẫn đến việc giảm sự chú ý khi xảy ra các sự kiện thực sự quan trọng, làm giảm hiệu quả an ninh và tăng chi phí vận hành do phải liên tục xác minh báo động giả.
  * Hiểu biết ngữ cảnh hạn chế – Các hệ thống dựa trên quy tắc về cơ bản gặp khó khăn trong việc diễn giải ngữ cảnh một cách tinh tế. Ngay cả các hệ thống truyền thống phức tạp cũng hoạt động với hiểu biết hạn chế về môi trường mà chúng giám sát do thiếu nhận thức ngữ cảnh, bởi vì chúng không thể dễ dàng thực hiện những điều sau:
    * Phân biệt hành vi bình thường với hành vi đáng ngờ
    * Hiểu các mô hình thời gian như các sự kiện lặp lại hàng tuần
    * Xem xét bối cảnh môi trường như thời gian trong ngày hoặc địa điểm
    * Liên hệ nhiều sự kiện có thể chỉ ra một mô hình
  * Thiếu bộ nhớ ngữ nghĩa – Các hệ thống thông thường không có khả năng xây dựng và sử dụng kiến thức theo thời gian. Chúng không thể thực hiện những điều sau:
    * Thiết lập các đường cơ sở của các sự kiện thường lệ so với các sự kiện bất thường
    * Cung cấp khả năng tìm kiếm ngôn ngữ tự nhiên trên dữ liệu lịch sử
    * Hỗ trợ lý luận về các mô hình mới nổi

Nếu không có những khả năng này, bạn sẽ không thể tận dụng tối đa lợi ích từ cơ sở hạ tầng giám sát hoặc thực hiện phân tích hồi cứu phức tạp. Để giải quyết những thách thức này một cách hiệu quả, bạn cần một phương pháp tiếp cận hoàn toàn khác. Bằng cách kết hợp khả năng hiểu ngữ cảnh của FM với một khuôn khổ có cấu trúc để phân loại và phản hồi sự kiện, bạn có thể xây dựng các hệ thống giám sát thông minh hơn. Amazon Bedrock Agents cung cấp nền tảng lý tưởng cho phương pháp tiếp cận thế hệ tiếp theo này.

## Tổng quan về giải pháp
Bạn có thể giải quyết những thách thức giám sát này bằng cách xây dựng giải pháp giám sát video với Amazon Bedrock Agents. Hệ thống sẽ sàng lọc thông minh các sự kiện, lọc các hoạt động thường ngày và nâng cấp các tình huống cần sự chú ý của con người, giúp giảm thiểu tình trạng quá tải cảnh báo đồng thời cải thiện độ chính xác phát hiện. Giải pháp sử dụng Amazon Bedrock Agents để phân tích chuyển động được phát hiện từ video và cảnh báo người dùng khi có sự kiện quan trọng xảy ra theo hướng dẫn được cung cấp. Điều này cho phép hệ thống lọc thông minh các sự kiện nhỏ có thể kích hoạt phát hiện chuyển động, chẳng hạn như gió hoặc chim, và chỉ hướng sự chú ý của người dùng vào các sự kiện quan trọng. Sơ đồ sau minh họa kiến trúc giải pháp.

![picture 3](/images/image3.2.3.png)
Giải pháp sử dụng ba thành phần chính để giải quyết các thách thức cốt lõi: các tác nhân như thang cuốn, quy trình xử lý video và Amazon Bedrock Agent. Chúng tôi sẽ thảo luận chi tiết hơn về các thành phần này trong các phần sau.
Giải pháp sử dụng AWS Cloud Development Kit (AWS CDK) để triển khai các thành phần giải pháp. AWS CDK là một khung phát triển phần mềm nguồn mở dùng để định nghĩa cơ sở hạ tầng đám mây dưới dạng mã và cung cấp thông qua AWS CloudFormation .

## Agent as escalators
Thành phần đầu tiên sử dụng Amazon Bedrock Agents để kiểm tra các sự kiện chuyển động được phát hiện với các khả năng sau:
  * Cung cấp khả năng hiểu ngôn ngữ tự nhiên của các cảnh và hoạt động để diễn giải theo ngữ cảnh
  * Duy trì nhận thức về thời gian trên các chuỗi khung hình để hiểu tiến trình sự kiện
  * Tham khảo các mô hình lịch sử để phân biệt các sự kiện bất thường với các sự kiện thường lệ
  * Áp dụng lý luận theo ngữ cảnh về hành vi, xem xét các yếu tố như thời gian trong ngày, địa điểm và chuỗi hành động

Chúng tôi triển khai một khuôn khổ phản hồi theo cấp độ phân loại các sự kiện theo mức độ nghiêm trọng và hành động cần thiết:

  * Cấp độ 0: Chỉ ghi nhật ký – Hệ thống ghi lại các hoạt động bình thường hoặc dự kiến. Ví dụ: khi người giao hàng đến trong giờ làm việc hoặc một phương tiện được nhận dạng đi vào lối vào, những sự kiện này sẽ được ghi lại để phân tích mẫu và tham khảo trong tương lai nhưng không yêu cầu hành động ngay lập tức. Chúng vẫn có thể được tìm kiếm trong lịch sử sự kiện.
  * Cấp độ 1: Thông báo của con người – Cấp độ này xử lý các sự kiện bất thường nhưng không nghiêm trọng cần sự chú ý của con người. Một chiếc xe lạ đỗ gần đó, một vị khách bất ngờ, hoặc các kiểu di chuyển bất thường sẽ kích hoạt thông báo cho nhân viên an ninh. Những sự kiện này cần được xác minh và đánh giá bởi con người.
  * Cấp độ 2: Phản hồi tức thì – Dành riêng cho các sự kiện bảo mật quan trọng. Các nỗ lực truy cập trái phép, phát hiện khói hoặc lửa, hoặc hành vi đáng ngờ sẽ kích hoạt hành động phản hồi tự động thông qua các lệnh gọi API. Hệ thống sẽ thông báo cho nhân viên qua tin nhắn SMS hoặc email với thông tin sự kiện và bối cảnh.

Giải pháp cung cấp giao diện xử lý và giám sát tương tác thông qua ứng dụng Streamlit. Với giao diện người dùng Streamlit , người dùng có thể cung cấp hướng dẫn và tương tác với tác nhân.
![picture 4](/images/image3.2.4.png)
Ứng dụng này bao gồm các tính năng chính sau:
  * Phát trực tiếp hoặc nhập tệp video – Ứng dụng chấp nhận URL luồng M3U8 từ webcam hoặc nguồn cấp dữ liệu bảo mật, hoặc tệp video cục bộ ở các định dạng phổ biến (MP4, AVI). Cả hai đều được xử lý bằng cùng một quy trình phát hiện chuyển động, lưu các sự kiện được kích hoạt vào Amazon Simple Storage Service (Amazon S3) để phân tích tác nhân.
  * Hướng dẫn tùy chỉnh – Người dùng có thể cung cấp hướng dẫn giám sát cụ thể, chẳng hạn như “Cảnh báo tôi về những cá nhân không xác định gần bến tàu sau giờ làm việc” hoặc “Tập trung vào hoạt động của phương tiện trong khu vực đỗ xe”. Những hướng dẫn này điều chỉnh cách tác nhân diễn giải các sự kiện chuyển động được phát hiện.
  * Cấu hình thông báo – Người dùng có thể chỉ định thông tin liên hệ cho các mức cảnh báo khác nhau. Hệ thống sử dụng Amazon Simple Notification Service (Amazon SNS) để gửi email hoặc tin nhắn văn bản dựa trên mức độ nghiêm trọng của sự kiện, do đó có thể thông báo cho các nhân viên khác nhau về các sự cố tiềm ẩn so với các tình huống nghiêm trọng.
  * Truy vấn ngôn ngữ tự nhiên về các sự kiện trong quá khứ – Giao diện bao gồm một thành phần trò chuyện để truy xuất các sự kiện lịch sử. Người dùng có thể hỏi "Những phương tiện nào đã vào đường lái xe trong tuần này?" hoặc "Cho tôi biết bất kỳ hoạt động đáng ngờ nào từ tối qua", và nhận được phản hồi dựa trên bộ nhớ sự kiện của hệ thống.

## Đường ống xử lý video
Giải pháp sử dụng một số dịch vụ AWS để thu thập và chuẩn bị dữ liệu video để phân tích thông qua một quy trình xử lý mô-đun. Giải pháp hỗ trợ nhiều loại nguồn video:

  * Phát trực tiếp video (định dạng M3U8)
  * Tệp video cục bộ (mp4, avi, v.v.)
  * Amazon Kinesis Video Streams (Kinesis video URL)
  * Local camera

Khi sử dụng luồng, thành phần VideoCapture của OpenCV sẽ xử lý kết nối và trích xuất khung hình. Để thử nghiệm, chúng tôi đã đưa vào các video sự kiện mẫu minh họa các tình huống khác nhau. Cốt lõi của quá trình xử lý video là một pipeline mô-đun được triển khai bằng Python. Các thành phần chính bao gồm:
  * SimpleMotionDetection – Xác định chuyển động trong nguồn cấp dữ liệu video
  * FrameSampling – Ghi lại chuỗi khung hình theo thời gian khi phát hiện chuyển động
  * GridAggregator – Tổ chức nhiều khung hình thành một lưới trực quan để tạo bối cảnh
  * S3Storage – Lưu trữ chuỗi khung hình đã chụp trong Amazon S3

Khung đa quy trình này tối ưu hóa hiệu suất bằng cách chạy các thành phần đồng thời và duy trì một hàng đợi các khung hình cần xử lý. Đường ống xử lý video sẽ sắp xếp dữ liệu khung hình đã ghi lại theo một cấu trúc nhất định trước khi chuyển đến tác nhân Amazon Bedrock để phân tích:

  * Frame sequence storage – Khi phát hiện chuyển động, hệ thống sẽ ghi lại chuỗi khung hình dài hơn 10 giây. Các khung hình này được lưu trữ trên Amazon S3 bằng cấu trúc đường dẫn dựa trên dấu thời gian (YYYYMMDD-HHMMSS) cho phép truy xuất hiệu quả theo ngày và giờ. Trong trường hợp chuyển động vượt quá 10 giây, nhiều sự kiện sẽ được tạo.
  * Image grid format– Thay vì xử lý từng khung hình riêng biệt, hệ thống sắp xếp nhiều khung hình liên tiếp thành một định dạng lưới (thường là 3×4 hoặc 4×5). Bản trình bày này cung cấp bối cảnh thời gian và được gửi đến tác nhân Amazon Bedrock để phân tích. Định dạng lưới cho phép hiểu cách chuyển động tiến triển theo thời gian, điều này rất quan trọng để diễn giải chính xác bối cảnh.

Hình dưới đây là ví dụ về lưới hình ảnh được gửi đến tác nhân. Việc đánh cắp gói tin rất khó xác định bằng các mô hình hình ảnh cổ điển. Khả năng suy luận trên một chuỗi hình ảnh của mô hình ngôn ngữ lớn (LLM) cho phép nó đưa ra các quan sát về ý định.

![picture 5](/images/image3.2.5.png)
Đầu ra của quy trình xử lý video—lưới khung có dấu thời gian được lưu trữ trong Amazon S3—đóng vai trò là đầu vào cho các thành phần tác nhân Amazon Bedrock, mà chúng ta sẽ thảo luận trong phần tiếp theo.

## Các thành phần của tác nhân Amazon Bedrock
Giải pháp tích hợp nhiều dịch vụ Amazon Bedrock để tạo ra một hệ thống phân tích thông minh:
  * Kiến trúc tác nhân cốt lõi – Tác nhân điều phối các quy trình công việc chính sau:
    * Nhận lưới khung hình từ Amazon S3 khi phát hiện chuyển động
    * Điều phối các quy trình phân tích nhiều bước
    * Đưa ra quyết định phân loại
    * Kích hoạt các hành động phản hồi thích hợp
    * Duy trì bối cảnh và trạng thái sự kiện
  * Quản lý kiến thức – Giải pháp sử dụng Cơ sở kiến thức Amazon Bedrock với Amazon OpenSearch Serverless để:
    * Lưu trữ và lập chỉ mục các sự kiện lịch sử
    * Xây dựng các mô hình hoạt động cơ bản
    * Cho phép truy vấn ngôn ngữ tự nhiên
    * Theo dõi các mẫu thời gian
    * Hỗ trợ phân tích theo ngữ cảnh

  * Nhóm hành động – Tác nhân có quyền truy cập vào một số hành động được xác định thông qua lược đồ API:
    * Phân tích lưới – Xử lý lưới khung hình đến từ Amazon S3
    * Cảnh báo – Gửi thông báo qua Amazon SNS dựa trên mức độ nghiêm trọng
    * Nhật ký – Ghi lại chi tiết sự kiện để tham khảo trong tương lai
    * Tìm kiếm sự kiện theo ngày – Truy xuất các sự kiện trong quá khứ dựa trên phạm vi ngày
    * Tra cứu phương tiện (Text-to-SQL) – Truy vấn cơ sở dữ liệu phương tiện để biết thông tin
Đối với các truy vấn dữ liệu có cấu trúc, hệ thống sử dụng khả năng chuyển đổi ngôn ngữ tự nhiên sang SQL của FM. Điều này cho phép:
  * Truy vấn các bảng Amazon Athena chứa bản ghi sự kiện
  * Truy xuất thông tin về xe đã đăng ký
  * Tạo báo cáo từ dữ liệu sự kiện có cấu trúc

Các thành phần này hoạt động cùng nhau để tạo ra một hệ thống toàn diện có thể phân tích nội dung video, duy trì lịch sử sự kiện và hỗ trợ cả cảnh báo theo thời gian thực và phân tích hồi cứu thông qua tương tác ngôn ngữ tự nhiên.

## Khung xử lý video
Khung xử lý video triển khai kiến trúc đa quy trình để xử lý luồng video thông qua chuỗi xử lý có thể cấu hình.
## Kiến trúc đường ống mô-đun
Khung này sử dụng phương pháp tiếp cận dựa trên thành phần được xây dựng xung quanh FrameProcessorlớp cơ sở trừu tượng.
Các thành phần xử lý triển khai một giao diện nhất quán với process(frame)phương thức lấy một Khung và trả về một Khung có khả năng được sửa đổi:
```
class FrameProcessor (ABC):
    @abstractmethod
    def process(self, frame: Frame) -> Optional[Frame]: ...
```
Lớp này Frame óng gói dữ liệu hình ảnh cùng với dấu thời gian, chỉ mục và siêu dữ liệu có thể mở rộng:
```
@dataclass
class Frame:
    buffer: ndarray  # OpenCV image array
    timestamp: float
    index: float
    fps: float
    metadata: dict = field(default_factory=dict)
```
## Chuỗi xử lý có thể tùy chỉnh
Kiến trúc này hỗ trợ cấu hình nhiều chuỗi xử lý có thể được kết nối theo trình tự. Giải pháp sử dụng hai chuỗi chính. Chuỗi phát hiện và phân tích xử lý các khung hình video đầu vào để xác định các sự kiện quan tâm:
```
chain = FrameProcessorChain([
    SimpleMotionDetection(motion_threshold=10_000, frame_skip_size=1),
    FrameSampling(timedelta(milliseconds=250), threshold_time=timedelta(seconds=2)),
    GridAggregator(shape=(13, 3))
])
```
Chuỗi lưu trữ và thông báo xử lý việc lưu trữ các sự kiện đã xác định và gọi tác nhân:
```
storage_chain = FrameProcessorChain([
    S3Storage(bucket_name=TARGET_S3_BUCKET, prefix=S3_PREFIX, s3_client_provider=s3_client_provider),
    LambdaProcessor(get_response=get_response, monitoring_instructions=config.monitoring_instructions)
])
```
Bạn có thể sửa đổi những thay đổi này một cách độc lập để thêm hoặc thay thế các thành phần dựa trên các yêu cầu giám sát cụ thể.
## Triển khai thành phần
Giải pháp bao gồm một số thành phần xử lý thể hiện khả năng của khung. Bạn có thể sửa đổi từng bước xử lý hoặc thêm bước mới. Ví dụ: đối với phát hiện chuyển động đơn giản, chúng tôi sử dụng một điểm ảnh đơn giản, nhưng bạn có thể tinh chỉnh chức năng phát hiện chuyển động khi cần, hoặc làm theo định dạng để triển khai các thuật toán phát hiện khác, chẳng hạn như phát hiện đối tượng hoặc phân đoạn cảnh.

Các thành phần bổ sung bao gồm Frame Sampling bộ xử lý để kiểm soát thời gian chụp, Grid Aggregator tạo lưới khung hình trực quan và bộ xử lý lưu trữ lưu dữ liệu sự kiện và kích hoạt phân tích tác nhân. Các bộ xử lý này có thể được tùy chỉnh và thay thế khi cần thiết. Ví dụ:
  * Sửa đổi các thành phần hiện có – Điều chỉnh ngưỡng hoặc tham số để phù hợp với các môi trường cụ thể
  * Tạo các backend lưu trữ thay thế – Đầu ra trực tiếp tới các dịch vụ lưu trữ hoặc cơ sở dữ liệu khác nhau
  * Triển khai các bước tiền xử lý và hậu xử lý – Thêm tính năng nâng cao hình ảnh, lọc dữ liệu hoặc tạo ngữ cảnh bổ sung

Cuối cùng, nó Lambda Processor đóng vai trò là cầu nối đến tác nhân Amazon Bedrock bằng cách gọi một hàm AWS Lambda để gửi thông tin trong một yêu cầu đến tác nhân đã triển khai. Từ đó, tác nhân Amazon Bedrock sẽ tiếp quản, phân tích sự kiện và thực hiện hành động tương ứng.

## Triển khai tác nhân
Sau khi triển khai giải pháp, một biệt danh tác nhân Amazon Bedrock sẽ khả dụng. Tác nhân này hoạt động như một lớp phân tích thông minh, xử lý các sự kiện video đã ghi lại và thực hiện các hành động phù hợp dựa trên kết quả phân tích. Bạn có thể kiểm tra tác nhân và xem dấu vết suy luận của nó trực tiếp trên bảng điều khiển Amazon Bedrock, như được hiển thị trong ảnh chụp màn hình sau.
![picture 6](/images/image3.2.6.png)
Tác nhân này sẽ thiếu một số siêu dữ liệu do ứng dụng Streamlit cung cấp (chẳng hạn như thời gian hiện tại) và có thể không đưa ra cùng câu trả lời như ứng dụng đầy đủ.

## Luồng gọi
Tác nhân được gọi thông qua một hàm Lambda xử lý chu trình yêu cầu-phản hồi và quản lý trạng thái phiên. Hàm này tìm ID phiên bản đã xuất bản cao nhất và sử dụng nó để gọi tác nhân và phân tích phản hồi.

## Nhóm hành động
Khả năng của tác nhân được xác định thông qua các nhóm hành động được triển khai bằng cách sử dụng Bedrock Agent Resolver khuôn khổ. Phương pháp này tự động tạo ra lược đồ OpenAPI theo yêu cầu của tác nhân.

Khi tác nhân được gọi, nó sẽ nhận được một đối tượng sự kiện bao gồm đường dẫn API và các tham số khác thông báo cho khung tác nhân cách định tuyến yêu cầu đến trình xử lý phù hợp. Bạn có thể thêm các hành động mới bằng cách định nghĩa các trình xử lý điểm cuối bổ sung theo cùng một mẫu và tạo một lược đồ OpenAPI mới:
```
if __name__ == "__main__":
    print(app.get_openapi_json_schema())
```
## Tích hợp văn bản sang SQL
Thông qua nhóm hành động của mình, tác nhân có thể dịch các truy vấn ngôn ngữ tự nhiên sang SQL để phân tích dữ liệu có cấu trúc. Hệ thống đọc dữ liệu từ assets/data_query_data_source, có thể bao gồm nhiều định dạng khác nhau như CSV, JSON, ORC hoặc Parquet.

Khả năng này cho phép người dùng truy vấn dữ liệu có cấu trúc bằng ngôn ngữ tự nhiên. Như minh họa trong ví dụ sau, hệ thống dịch các truy vấn ngôn ngữ tự nhiên về xe cộ sang SQL, trả về thông tin có cấu trúc từ cơ sở dữ liệu.
![picture 7](/images/image3.2.7.png)
Kết nối cơ sở dữ liệu được cấu hình thông qua công cụ SQL Alchemy. Người dùng có thể kết nối với cơ sở dữ liệu hiện có bằng cách cập nhật create_sql_engine()hàm để sử dụng các tham số kết nối của chúng.

## Bộ nhớ sự kiện và tìm kiếm ngữ nghĩa
Tác nhân này duy trì bộ nhớ chi tiết về các sự kiện trong quá khứ, lưu trữ nhật ký sự kiện với mô tả phong phú trên Amazon S3. Các sự kiện này có thể được tìm kiếm thông qua cả tìm kiếm ngữ nghĩa dựa trên vectơ và lọc theo ngày. Như được minh họa trong ví dụ sau, truy vấn thời gian cho phép truy xuất thông tin về các sự kiện trong khoảng thời gian cụ thể, chẳng hạn như số lượng phương tiện được quan sát trong 72 giờ qua.

Khả năng bộ nhớ ngữ nghĩa của hệ thống cho phép thực hiện các truy vấn dựa trên các khái niệm trừu tượng và mô tả bằng ngôn ngữ tự nhiên. Như được minh họa trong ví dụ sau, tác nhân có thể hiểu các khái niệm trừu tượng như "buồn cười" và truy xuất các sự kiện liên quan, chẳng hạn như một người làm rơi bánh sinh nhật.

Tác nhân có thể liên kết các sự kiện với nhau để xác định các mẫu hoặc sự cố liên quan. Ví dụ: hệ thống có thể liên hệ các lần nhìn thấy riêng biệt của những cá nhân có đặc điểm tương tự. Trong ảnh chụp màn hình sau, tác nhân kết nối các sự cố liên quan bằng cách xác định các thuộc tính chung như quần áo trong các sự kiện khác nhau.

Kho lưu trữ sự kiện này cho phép hệ thống tích lũy kiến thức theo thời gian, cung cấp những thông tin chi tiết ngày càng có giá trị khi dữ liệu được tích lũy. Sự kết hợp giữa truy vấn cơ sở dữ liệu có cấu trúc và tìm kiếm ngữ nghĩa trên các mô tả sự kiện tạo ra một tác nhân có bộ nhớ có thể tìm kiếm được về tất cả các sự kiện trong quá khứ.

## Điều kiện tiên quyết
Trước khi triển khai giải pháp, hãy hoàn tất các điều kiện tiên quyết sau:

  1. Cấu hình thông tin xác thực AWS bằng cách sử dụng aws configure. Sử dụng hoặc us-west-2Vùng us-east-1AWS.
  2. Cho phép truy cập vào các mô hình Claude 3.x của Anthropic hoặc một mô hình Amazon Bedrock Agents được hỗ trợ khác mà bạn muốn sử dụng.
  3. Hãy đảm bảo bạn có các phụ thuộc sau:
    * Python
    * AWS CDK
    * AWS Command Line Interface (AWS CLI)
    * Git
    * Node.js
    * Docker
## Triển khai giải pháp
Việc triển khai AWS CDK tạo ra các tài nguyên sau:

  * Lưu trữ – Thùng S3 cho tài sản và kết quả truy vấn
  * Tài nguyên Amazon Bedrock – Đại lý và cơ sở kiến thức
  * Tính toán – Các hàm Lambda cho các hành động, lệnh gọi và cập nhật
  * Cơ sở dữ liệu – Cơ sở dữ liệu Athena dành cho các truy vấn có cấu trúc và trình thu thập dữ liệu AWS Glue để khám phá dữ liệu
Triển khai giải pháp bằng các lệnh sau:

```
#1. Clone the repository and navigate to folder
git clone https://github.com/aws-samples/sample-video-monitoring-agent.git && cd sample-video-monitoring-agent
#2. Set up environment and install dependencies
python3 -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt
#3. Deploy AWS resources
cdk bootstrap && cdk deploy
#4. Run the streamlit app
cd code/streamlit_app && streamlit run app.py
```
Trên Windows, hãy thay thế dòng thứ hai bằng mã sau:

```
python3 -m venv .venv && % .venv\Scripts\activate.bat && pip install -r requirements.txt
```
## Dọn dẹp
Để hủy các tài nguyên bạn đã tạo và ngừng phát sinh chi phí, hãy chạy lệnh sau:
```
cdk destroy
```
## Những cải tiến trong tương lai
Việc triển khai hiện tại chứng minh tiềm năng của việc giám sát video dựa trên tác nhân trong bối cảnh an ninh tại nhà, nhưng vẫn còn nhiều ứng dụng tiềm năng khác.
## Các trường hợp sử dụng mẫu
Sau đây là phần trình bày về ứng dụng của giải pháp này trong nhiều tình huống khác nhau.
### Doanh nghiệp nhỏ
{ “alert_level”: 0, “timestamp”: “2024-11-20T15:24:15Z”, “reason”: “Xe đến lối vào nhà”, “description”: “Trình tự xe đến và đỗ theo tiêu chuẩn. Xe hiện diện: Xe bán tải Nissan Frontier màu đen (đang đỗ), Honda CR-V màu bạc (đang đến), và một phần xe màu xanh ở phía trước. Đặc điểm khu vực: Mặt đường trải sỏi, hai thùng rác (Rác thải Quận và tái chế), cây xanh ở phía sau. Trình tự cho thấy Honda CR-V đang thực hiện thao tác đỗ xe thông thường: tiếp cận từ phía đông, thực hiện vòng quay ba điểm theo tiêu chuẩn, đến vị trí cuối cùng bên cạnh xe bán tải. Điều kiện ban ngày, tầm nhìn rõ ràng. Tình trạng xe: Xe CR-V sạch sẽ, được bảo dưỡng tốt, có vẻ là đời 2012-2016, không có hư hỏng rõ ràng hoặc thay đổi bất thường. Mẫu di chuyển cho thấy tài xế quen thuộc đang thực hiện thao tác đỗ xe thông thường. Không quan sát thấy hành vi đáng ngờ hoặc lo ngại về an toàn. Dấu thời gian cho biết thời gian đến theo tiêu chuẩn vào buổi chiều. Thùng rác được đặt đúng vị trí và không bị xáo trộn trong quá trình đỗ xe.” }
### Công nghiệp
{ “alert_level”: 2, “timestamp”: “2024-11-20T15:24:15Z”, “reason”: “Rò rỉ sản phẩm/nguy cơ an toàn trong kho”,”description”: “Sự cố tràn sản phẩm đáng kể trong lối đi lưu trữ trong kho. Địa điểm: Lối đi chính trong kho giữa các hệ thống kệ cao chứa hàng tồn kho đóng hộp. Trình tự cho thấy những gì có vẻ là chất lỏng hoặc tràn container, có thể là sản phẩm nước/đồ uống dựa trên các container màu xanh lam có thể nhìn thấy. Cơ sở hạ tầng: Kho được thiết lập chuyên nghiệp với kệ kim loại màu xanh lam nhiều tầng, sàn bê tông, đèn chiếu sáng trên cao. Tiến trình sự cố: Khung hình ban đầu cho thấy lối đi sạch sẽ, sau đó là sản phẩm rơi/lộn, dẫn đến việc các mặt hàng phân tán rộng rãi trên sàn lối đi. Đánh giá mối nguy hiểm: Tạo ra nguy cơ trượt ngã ngay lập tức, chặn lối thoát hiểm khẩn cấp, có khả năng gây thiệt hại cho hàng tồn kho. Tác động đến khu vực: Khoảng 15-20 feet không gian lối đi bị ảnh hưởng. Loại cơ sở dường như là trung tâm phân phối hoặc kho lưu trữ. Nhiều hộp các tông nhìn thấy trên các kệ xung quanh có nguy cơ bị hư hỏng do chất lỏng.” }

### Sân sau
{ “alert_level”: 1, “timestamp”: “2024-11-20T15:24:15Z”, “reason”: “Phát hiện động vật hoang dã trong khu vực”, “description”: “Quan sát thấy gấu mèo trưởng thành đang thăm dò khu vực hiên/sàn có lan can màu trắng. Camera hồng ngoại/nhìn đêm cung cấp hình ảnh rõ nét về con vật. Đặc điểm của đối tượng: gấu mèo trưởng thành cỡ trung bình, các dấu hiệu đặc trưng trên mặt dễ thấy, bộ lông khỏe mạnh, kiểu di chuyển bình thường. Chuỗi hình ảnh cho thấy con vật đang tiến lại gần camera (15:42 chiều), đang thăm dò khu vực gần lan can (15:43-15:44 chiều), với sự kiểm tra kỹ lưỡng khuôn mặt (15:45 chiều). Khung hình cuối cùng cho thấy một phần góc nhìn khi con vật di chuyển ra xa. Môi trường: Vị trí dường như là sàn/sàn cao với lan can và trụ gỗ sơn trắng. Điều kiện ánh sáng: Ban đêm, camera hoạt động ở chế độ hồng ngoại/nhìn đêm cung cấp hình ảnh đen trắng rõ nét. Hành vi của con vật dường như là hoạt động khám phá ban đêm bình thường, không có dấu hiệu hung dữ hoặc bệnh tật.” }

### Các phần mở rộng tiếp theo
Ngoài ra, bạn có thể mở rộng khả năng FM bằng các phương pháp sau:
  * Tinh chỉnh cho các bối cảnh giám sát cụ thể – Điều chỉnh các mô hình để nhận dạng các đối tượng, hành vi và tình huống cụ thể theo miền
  * Lời nhắc được tinh chỉnh cho các trường hợp sử dụng cụ thể – Tạo các hướng dẫn chuyên biệt giúp tối ưu hóa hiệu suất của tác nhân cho các môi trường cụ thể như cơ sở công nghiệp, không gian bán lẻ hoặc khu dân cư

Bạn có thể mở rộng khả năng hành động của tác nhân, ví dụ:
  * Kiểm soát trực tiếp hệ thống nhà thông minh và tòa nhà thông minh – Tích hợp với API thiết bị Internet vạn vật (IoT) để điều khiển đèn, khóa hoặc hệ thống báo động
  * Tích hợp với các giao thức bảo mật và an toàn – Kết nối với cơ sở hạ tầng bảo mật hiện có để tuân theo các quy trình đã thiết lập
  * Quy trình phản hồi tự động – Tạo chuỗi hành động nhiều bước có thể được kích hoạt bởi các sự kiện cụ thể

Bạn cũng có thể cân nhắc việc nâng cao hệ thống bộ nhớ sự kiện:
  * Nhận dạng mẫu dài hạn – Xác định các mẫu lặp lại trong khoảng thời gian dài
  * Tương quan giữa các camera – Liên kết các quan sát từ nhiều camera để theo dõi chuyển động qua một không gian
  * Phát hiện bất thường dựa trên các mẫu lịch sử – Tự động xác định độ lệch so với các đường cơ sở đã thiết lập

Cuối cùng, hãy cân nhắc mở rộng khả năng giám sát ngoài các camera cố định:
  * Giám sát cho hệ thống thị giác robot – Áp dụng trí thông minh tương tự cho robot di động tuần tra hoặc kiểm tra khu vực
  * Giám sát bằng máy bay không người lái – Xử lý cảnh quay trên không để giám sát toàn diện địa điểm
  * Ứng dụng bảo mật di động – Mở rộng nền tảng để xử lý dữ liệu từ camera gắn trên người nhân viên an ninh hoặc thiết bị di động

Những cải tiến này có thể chuyển đổi hệ thống từ một công cụ giám sát thụ động thành một bên tham gia tích cực vào các hoạt động bảo mật, với khả năng hiểu biết ngày càng tinh vi về các mô hình bình thường và các sự kiện bất thường.

## Phần kết luận
Phương pháp sử dụng tác nhân như thang cuốn thể hiện một bước tiến đáng kể trong giám sát video, sử dụng khả năng hiểu ngữ cảnh của FM với khuôn khổ hướng hành động của Amazon Bedrock Agents. Bằng cách lọc tín hiệu khỏi nhiễu, giải pháp này giải quyết vấn đề quan trọng về tình trạng quá tải cảnh báo, đồng thời nâng cao khả năng giám sát an ninh và an toàn. Với giải pháp này, bạn có thể:

  * Giảm các kết quả dương tính giả trong khi vẫn duy trì độ nhạy phát hiện cao
  * Cung cấp các mô tả và phân loại sự kiện dễ đọc đối với con người
  * Duy trì hồ sơ có thể tìm kiếm của tất cả các hoạt động
  * Khả năng giám sát quy mô mà không cần nguồn nhân lực tương xứng

Sự kết hợp giữa sàng lọc thông minh, phản hồi phân cấp và bộ nhớ ngữ nghĩa cho phép một hệ thống giám sát hiệu quả và năng suất hơn, nâng cao năng lực của con người thay vì thay thế chúng. Hãy dùng thử giải pháp ngay hôm nay và trải nghiệm cách Amazon Bedrock Agents có thể chuyển đổi khả năng giám sát video của bạn từ phát hiện chuyển động đơn giản sang khả năng hiểu cảnh thông minh.

## Về các tác giả
![picture 8](/images/image3.2.8.png)
Kiowa Jackson là Kỹ sư Học máy Cấp cao tại AWS ProServe, chuyên về thị giác máy tính và hệ thống agentic cho các ứng dụng công nghiệp. Công việc của ông kết nối các phương pháp học máy cổ điển với AI tạo sinh để nâng cao khả năng tự động hóa công nghiệp. Các công trình trước đây của ông bao gồm hợp tác với Amazon Robotics, NFL và Koch Georgia Pacific.

![picture 9](/images/image3.2.9.png)
Piotr Chotkowski là Kiến trúc sư Ứng dụng Đám mây Cấp cao tại Trung tâm Đổi mới Trí tuệ Nhân tạo AWS (AWS Generative AI Innovation Center). Ông có kinh nghiệm thực tế về kỹ thuật phần mềm cũng như thiết kế kiến trúc phần mềm. Trong vai trò tại AWS, ông hỗ trợ khách hàng thiết kế và xây dựng các ứng dụng AI nhân tạo cấp độ sản xuất trên nền tảng đám mây.







