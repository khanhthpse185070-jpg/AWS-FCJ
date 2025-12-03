---
title: "Blog 3"
 
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Giao hàng nhanh hơn bằng cách giới hạn công việc đang được tiến hành 

Bởi Matthias Patzak | vào 04 tháng 3 năm 2025 | in Best Practices, DevOps, Enterprise Strategy | Permalink |  Comments |  Share

Các nhóm phát triển phần mềm luôn gặp khó khăn trong việc cung cấp các tính năng trong khung thời gian mà doanh nghiệp và khách hàng mong đợi. Một  nghiên cứu gần đây của BCG study cho thấy hơn một phần ba số dự án phát triển phần mềm nội bộ của người được hỏi bị trì hoãn. Việc giao hàng trễ làm chậm trễ lợi tức đầu tư (ROI) và gây khó chịu cho tất cả những người liên quan.

Các tổ chức phải đối mặt với nhiều thách thức khi đẩy nhanh việc cung cấp phần mềm, nhưng có một thách thức nổi bật vì tác động to lớn và cách khắc phục tương đối đơn giản: làm quá nhiều việc cùng một lúc.

## Bẫy đa nhiễm 
Một nhóm có ba dự án kéo dài sáu tuần:
  * Dự án A: cập nhật ứng dụng di động hướng tới khách hàng
  * Dự án B: cải tiến bảo mật quan trọng
  * Dự án C: API mới để tích hợp đối tác

Nếu bối cảnh nhóm thay đổi liên tục giữa các dự án, họ sẽ bị sa lầy. Có lẽ bạn cũng đã từng trải qua tình huống này, tham dự các cuộc họp liên tục và quản lý các kỳ vọng khác nhau của các bên liên quan. Cuối cùng, nhóm hoàn thành cả ba dự án cùng một lúc:

  * Dự án A: 16 tuần
  * Dự án B: 17 tuần
  * Dự án C: 18 tuần
Tác động thật thảm khốc. Ứng dụng di động ra mắt rất lâu sau mùa mua sắm cao điểm. Bản cập nhật bảo mật bị trì hoãn gây lo lắng cho các bên liên quan, và API bị trì hoãn khiến cơ hội tích hợp đối tác bị trì hoãn.
![picture 1](/images/image3.3.1.png)
Nhưng nếu nhóm tập trung vào một dự án cho đến khi hoàn thành, họ có thể cung cấp ứng dụng di động chỉ trong 6 tuần. Họ hoàn thành bản cập nhật bảo mật vào tuần thứ 12 và API vào tuần thứ 18. Họ vẫn hoàn thành tất cả công việc trong 18 tuần, nhưng họ cung cấp cho khách hàng một bản cập nhật giá trị sớm hơn 10 tuần so với việc chuyển đổi ngữ cảnh giữa các dự án. Họ khắc phục các vấn đề bảo mật sớm hơn 5 tuần, và toàn bộ quy trình hiệu quả hơn.

## Giải pháp đơn giản: Giới hạn công việc đang tiến hành (WIP)
Bạn có thể rút ngắn thời gian đưa sản phẩm ra thị trường bằng cách giới hạn công việc đang tiến hành (WIP), tức là giới hạn số lượng mục mà nhóm của bạn làm việc cùng một lúc.

Khi các nhóm phát triển tại Siemens Health Systems  bắt đầu áp dụng giới hạn WIP, họ đã giảm thời gian chu kỳ giao hàng từ 71 ngày xuống còn 43 ngày—cải thiện 42%. Các nhóm không cần bổ sung nguồn lực hay tăng giờ làm việc. Cùng một nhóm, hoàn thành cùng khối lượng công việc, đã mang lại giá trị cho khách hàng sớm hơn gần một tháng. Chất lượng cũng được cải thiện đáng kể—tỷ lệ thành công trong lần kiểm tra đầu tiên tăng từ 75% lên 95%. Việc tập trung vào ít hạng mục cùng lúc giúp giao hàng nhanh hơn và kết quả tốt hơn.

Little’s Law, mô tả số lượng mặt hàng trung bình trong một hệ thống tĩnh theo thời gian, chứng minh bằng toán học rằng thời gian giao hàng tăng lên khi WIP tăng:
![picture 2](/images/image3.3.2.png)
Where:
  * L= số lượng mục trung bình trong hệ thống (WIP)
  * λ = số lượng trung bình các mặt hàng đến trong một đơn vị thời gian (thông lượng); và
  * W = thời gian trung bình một mục tồn tại trong hệ thống (thời gian chu kỳ).

Nếu có 10 mục đang được tiến hành (L) và có 2 mục hoàn thành mỗi tuần (λ), thì mỗi mục sẽ mất 5 tuần (W):
![picture 3](/images/image3.3.3.png)
Nhân đôi WIP lên 20 mục và thời gian giao hàng tăng gấp đôi lên 10 tuần—ngay cả khi tỷ lệ hoàn thành vẫn như vậy:
![picture 4](/images/image3.3.4.png)
Nếu bạn muốn giao hàng nhanh hơn, bạn có hai lựa chọn: tăng thông lượng (cần nhiều tài nguyên hơn) hoặc giảm WIP (cần tập trung hơn). Bạn không cần đầu tư lớn hay chuyển đổi phức tạp để bắt đầu sử dụng giới hạn WIP; đây là một trong những công cụ cải tiến tiết kiệm chi phí nhất hiện có.

## Sử dụng giới hạn WIP ở nơi quan trọng nhất
Giới hạn WIP hiệu quả nhất khi gặp tình trạng tắc nghẽn. Theo lý thuyết ràng buộc, thông lượng của bất kỳ quy trình nào cũng bị giới hạn bởi bước chậm nhất của quy trình đó.

Value stream mapping giúp bạn xác định những hạn chế này. Nó trực quan hóa toàn bộ quy trình phát triển của bạn — từ ý tưởng đến sản xuất — giúp bạn thấy rõ khối lượng công việc tích tụ và các điểm nghẽn hình thành. Bạn có thể phát hiện ra một lượng lớn mã hoặc tính năng chưa được kiểm thử đang chờ phê duyệt triển khai. Những điểm nghẽn này hoạt động như những hạn chế làm hạn chế tốc độ phân phối tổng thể của bạn.

Bằng cách đặt giới hạn WIP một cách chiến lược tại các giai đoạn nút thắt này, bạn tạo ra hiệu ứng "kéo" điều chỉnh toàn bộ hệ thống. Khi giai đoạn nút thắt chạm đến giới hạn WIP, các giai đoạn thượng nguồn sẽ tự động chậm lại vì chúng không thể đẩy thêm công việc về phía trước. Điều này ngăn chặn công việc bị dồn ứ tại điểm giới hạn và giảm tổng lượng WIP trong hệ thống của bạn. Trong khi đó, các giai đoạn hạ nguồn chỉ có thể xử lý công việc nhanh như tốc độ nó chảy qua nút thắt.

Trong một quy trình phát triển thông thường, kiểm thử là nút thắt cổ chai. Nếu không có giới hạn WIP, bạn có thể thấy 10 tính năng đang được phát triển đồng thời, 6 tính năng đang chờ duyệt mã, 8 tính năng bị kẹt trong quá trình kiểm thử và 3 tính năng đang chờ triển khai—tức là 27 mục đang được tiến hành. Bằng cách đặt giới hạn WIP là 4 mục đang kiểm thử, bạn sẽ tạo ra hiệu ứng lan tỏa: quá trình duyệt mã không thể đẩy quá 4 mục về phía trước, do đó quá trình phát triển tập trung vào ít tính năng hơn cùng một lúc. Giờ đây, bạn có thể có 4 tính năng đang phát triển, 4 tính năng đang được duyệt, 4 tính năng đang được kiểm thử và 2 tính năng đang được triển khai—tổng cộng chỉ có 14 mục. Với cùng tốc độ hoàn thành 3 tính năng mỗi tuần, bạn đã rút ngắn thời gian chu kỳ gần một nửa, từ 9 tuần xuống còn chưa đầy 5 tuần.

## Bắt đầu: 12 tuần đầu tiên của bạn với giới hạn WIP
Để bắt đầu áp dụng giới hạn WIP trong tổ chức của bạn, hãy chọn một nhóm thí điểm. Hãy tìm một nhóm sẵn sàng thay đổi và đang gặp khó khăn với khối lượng công việc hiện tại—họ sẽ là đối tác tốt nhất của bạn trong nỗ lực này. Tập hợp nhóm và các bên liên quan để phác thảo từng bước từ ý tưởng đến triển khai sản xuất trong sơ đồ luồng giá trị. Đặc biệt chú ý đến các giai đoạn công việc thường bị dồn ứ—những khu vực này sẽ được hưởng lợi nhiều nhất từ giới hạn WIP ban đầu của bạn.

Tìm điểm nghẽn. Sau đó, đặt giới hạn WIP ban đầu ở mức 70% đến 80% khối lượng công việc hiện tại để tạo ra sự căng thẳng hiệu quả mà không làm gián đoạn việc giao hàng. Trong ví dụ trên về quy trình phát triển điển hình, bạn sẽ đặt giới hạn ban đầu là sáu mục trong quá trình kiểm thử.

Đo thời gian chu kỳ của nhóm thí điểm trong bốn tuần. Đếm số ngày hoàn thành mỗi hạng mục công việc. Theo dõi số lượng hạng mục nhóm hoàn thành mỗi tháng (thông lượng). Tính thời gian cho từng bước, chẳng hạn như phát triển và thử nghiệm, sau đó giảm giới hạn WIP tại điểm nghẽn khi các nhóm thích nghi.

Sau 4 tuần đầu tiên, hãy giảm giới hạn từ 10% đến 20%. Khoảng này cân bằng giữa tiến độ và tính thực tiễn—giới hạn cứng gây ra sự phản kháng, nhưng giới hạn mềm không đủ để thúc đẩy thay đổi hành vi. Hãy cân nhắc nhu cầu của nhóm bạn. Một nhóm phát triển 10 người có thể bắt đầu với 8 mục đồng thời và giảm xuống còn 6 khi tỷ lệ hoàn thành được cải thiện.

Tiếp tục đo lường những thứ tương tự trong 8-12 tuần. Hãy xem sự khác biệt. Các nhóm sẽ hoàn thành công việc nhanh hơn với ít hạng mục đang thực hiện hơn nhưng vẫn hoàn thành cùng số lượng hạng mục mỗi tháng. Một nhóm hoàn thành ba hạng mục mỗi tuần sẽ hiển thị kết quả như trong hình 2.
![picture 5](/images/image3.3.5.png)
Hình 2. Tác động của giới hạn WIP trong khoảng thời gian 8 tuần

Khi các nhóm đạt đến giới hạn WIP, họ nên hỗ trợ các công việc chủ động (sửa lỗi, cải thiện mã, cập nhật công cụ hoặc chia sẻ kiến thức) thay vì bắt đầu các nhiệm vụ mới. Các cá nhân đóng góp có thể cảm thấy họ làm việc chậm hơn, nhưng các nhóm hoàn thành công việc nhanh hơn và đẩy nhanh tiến độ giao hàng tổng thể.

## Mở rộng thành công vượt ra ngoài nhóm thí điểm
Triển khai và mở rộng giới hạn WIP trên toàn tổ chức của bạn. Sau giai đoạn thử nghiệm thành công, hãy mở rộng giới hạn WIP, bắt đầu với các nhóm thường xuyên tương tác với nhóm thử nghiệm. Họ sẽ thấy được lợi ích thông qua quá trình cộng tác hàng ngày. Các nhóm này phải đối mặt với những thách thức tương tự và làm việc theo các yêu cầu tương đương, khiến họ trở thành ứng cử viên lý tưởng cho việc áp dụng.

Tăng dần giới hạn WIP. Các nhóm làm việc ở cấp độ câu chuyện, nhưng các sáng kiến lớn hơn thường liên quan đến nhiều nhóm. Hãy áp dụng giới hạn WIP ở các cấp độ cao hơn này. Trưởng phòng nên giới hạn các sáng kiến đang hoạt động. Khi các nhóm hoàn thành công việc một cách nhất quán với giới hạn WIP, các trưởng phòng sẽ áp dụng chúng ở cấp độ danh mục đầu tư.

Mở rộng giới hạn WIP trong toàn bộ quy trình phân phối. Lập bản đồ hành trình từ ý tưởng ban đầu đến triển khai sản xuất. Nhiều tổ chức nhận thấy quy trình của họ bắt đầu từ rất lâu trước khi bất kỳ nhóm nào viết mã. Áp dụng giới hạn WIP ở mỗi giai đoạn để duy trì sự liền mạch trong toàn bộ quy trình phân phối.

## Ngừng bắt đầu và bắt đầu kết thúc
Giới hạn WIP không chỉ giúp phần mềm nhanh hơn hiện tại mà còn giúp tổ chức của bạn sẵn sàng cho những thách thức trong tương lai. Các tổ chức sử dụng giới hạn WIP để cung cấp phần mềm nhanh chóng có thể duy trì tốc độ khi mở rộng quy mô.

Nhóm phát triển của bạn đã có khả năng giao hàng nhanh hơn. Giới hạn WIP sẽ giải phóng tiềm năng đó.

## Về tác giả
![picture 6](/images/image3.3.6.png)
Matthias Patzak gia nhập đội ngũ Chiến lược gia  Doanh nghiệp vào đầu năm 2023 sau một thời gian làm Cố vấn Chính về Kiến trúc Giải pháp AWS. Trong vai trò này, Matthias làm việc với các đội ngũ điều hành về cách thức đám mây có thể giúp tăng tốc độ đổi mới, hiệu quả CNTT và giá trị kinh doanh mà công nghệ của họ tạo ra từ góc độ con người, quy trình và công nghệ. Trước khi gia nhập AWS, Matthias là Phó Chủ tịch CNTT tại AutoScout24 và Tổng Giám đốc tại Home Shopping Europe. Tại cả hai công ty, ông đã giới thiệu các mô hình vận hành tinh gọn - linh hoạt trên quy mô lớn và dẫn dắt các cuộc chuyển đổi đám mây thành công, rút ngắn thời gian triển khai, tăng giá trị kinh doanh và nâng cao định giá công ty.





