---
title : "Trực quan hóa Analytics với Trang tổng quan sáng bóng"

weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

## 5.5.1 Cách tiếp cận Trực quan hóa Thực dụng

Với phạm vi dự án hiện tại, hãy bắt đầu với những gì đã có sẵn:

- **CloudWatch Log Insights**: Sử dụng các truy vấn đã lưu để xem nhanh độ trễ, tỷ lệ lỗi 5xx/4xx, lỗi xác thực và số lượng sự kiện sản phẩm (product_view, add_to_cart, checkout_*).

- **Athena** (Tùy chọn, nếu kích hoạt xuất dữ liệu): Chạy SQL trên nhật ký JSON đã xuất để xây dựng các biểu đồ phễu (funnels) đơn giản và xem mức độ phổ biến của sản phẩm.

- **QuickSight (Tùy chọn)**: Sử dụng các dashboard nhẹ trên Athena; giữ kích thước SPICE (Công cụ tính toán siêu tốc) nhỏ.

## 5.5.2 Các Truy vấn CloudWatch Đề xuất

- **Độ tin cậy (Reliability)**: Tỷ lệ lỗi, độ trễ p95 theo tuyến đường; các endpoint lỗi nhiều nhất; lỗi xác thực.

- **Hành vi (Behavior)**: Số lượng theo eventName; mức độ phổ biến của sản phẩm (productId, category); tỷ lệ hoàn thành thanh toán.

- **Tải lên (Uploads)**: Thành công so với thất bại cho presigned PUT (lọc theo statusCode và path).

Lưu các truy vấn và ghim vào một CloudWatch dashboard để có khả năng hiển thị hoạt động nhanh chóng.

## 5.5.3 Nếu sử dụng Athena/QuickSight

1. Xuất nhật ký CloudWatch sang S3 hàng ngày.

2. Tạo một bảng ngoài (external table) trên dữ liệu JSON; phân vùng theo ngày.

3. Các số liệu ví dụ:

  - Các sự kiện theo thời gian, sự kiện được kết hợp theo userLoginState.
  
  - Số lượt xem sản phẩm so với thêm vào giỏ hàng so với hoàn thành thanh toán.
  
  - Tỷ lệ lỗi và độ trễ p95 theo tuyến đường.
  
4. Trong QuickSight, xây dựng 3 hình ảnh trực quan:

  - Các ô KPI (Tổng số sự kiện, tỷ lệ lỗi, độ trễ p95).
  
  - Biểu đồ Phễu (product_view → add_to_cart →checkout_start → checkout_complete).
  
  - Các sản phẩm hàng đầu (lượt xem và thêm vào giỏ hàng).
  
## 5.5.4 Quyền truy cập và Bảo mật

- Giữ bucket xuất dữ liệu riêng tư; giới hạn quyền truy cập Athena/QuickSight cho quản trị viên dự án.

- Sử dụng ranh giới quyền IAM (IAM permission boundaries): chỉ cấp quyền đọc cho nhà phân tích, quyền ghi cho đội vận hành (ops) khi cần.

- Không có endpoint dashboard công khai; chia sẻ thông qua truy cập console AWS hoặc PDF đã xuất nếu được yêu cầu.