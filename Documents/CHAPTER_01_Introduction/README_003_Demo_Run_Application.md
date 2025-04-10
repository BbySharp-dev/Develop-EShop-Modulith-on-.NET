# Hướng dẫn chạy ứng dụng và kiểm thử End-to-End

## 🚀 Chạy ứng dụng với Docker Compose

### Bước 1: Clone mã nguồn
Tải mã nguồn từ GitHub về máy tính cá nhân của bạn.

### Bước 2: Mở và cấu hình trong Visual Studio
- Mở thư mục mã nguồn bằng Visual Studio
- Đảm bảo Docker Desktop đã được khởi động
- Nhấp chuột phải vào `docker-compose` trong Solution Explorer
- Chọn **Set as Startup Project**
- Chạy dự án bằng cách nhấn **Ctrl + F5** (chạy không debug)

Sau khi chạy, Docker Desktop sẽ hiển thị các container của ứng dụng bao gồm:
- API chính
- Các dịch vụ phụ trợ: PostgreSQL, Redis, RabbitMQ, v.v.

---

## 🧪 Kiểm thử API với Postman

### Cấu hình Postman
- Mở Collection mẫu được cung cấp trong khóa học
- Chọn môi trường là **docker**
- Đảm bảo các request đang trỏ đến địa chỉ `https://localhost:6060`

---

### 1️⃣ Kiểm thử module Catalog

- Gửi yêu cầu tạo sản phẩm mới bằng phương thức POST
- Kiểm tra sản phẩm đã tạo qua GET danh sách sản phẩm với phân trang
- Gửi yêu cầu GET theo ID để xem chi tiết từng sản phẩm

---

### 2️⃣ Kiểm thử module Basket

- Trước khi tương tác, bạn cần lấy **access token** từ Identity Server bằng phương thức POST
- Dán token vào phần **Authorization** dạng Bearer Token
- Gửi yêu cầu POST để tạo mới giỏ hàng với một số sản phẩm mẫu
- Dùng GET để truy xuất giỏ hàng theo tên người dùng

---

### 3️⃣ Kiểm thử module Ordering với Outbox Pattern

- Mở RabbitMQ dashboard để theo dõi hàng đợi
- Gửi yêu cầu POST để thực hiện hành động "checkout" giỏ hàng
- Sự kiện này sẽ:
  - Ghi lại dữ liệu vào bảng outbox
  - Xóa giỏ hàng đã đặt hàng
  - Gửi sự kiện `BasketCheckout` tới RabbitMQ
  - Được tiêu thụ bởi module Ordering
  - Kích hoạt luồng tạo đơn hàng và khởi động quá trình xử lý đơn hàng

---

### 4️⃣ Xác nhận kết quả

- Trong RabbitMQ: xác nhận sự kiện đã được publish từ Basket và consumed bởi Ordering
- Trong Postman: gửi yêu cầu GET để xem danh sách đơn hàng
  - Kiểm tra dữ liệu người mua, địa chỉ giao hàng, thanh toán và danh sách sản phẩm đã đặt

---

## ✅ Kết luận

Bạn đã hoàn thành quy trình kiểm thử toàn bộ hệ thống theo kiến trúc Modular Monolith:

- Chạy ứng dụng trong môi trường Docker mô phỏng production
- Tương tác với các module thông qua Postman
- Kiểm thử cả **giao tiếp đồng bộ** (REST API) và **giao tiếp bất đồng bộ** (RabbitMQ + Outbox Pattern)

Đây là nền tảng quan trọng để bạn hiểu cách các module hoạt động độc lập nhưng vẫn phối hợp chặt chẽ trong hệ thống thực tế.
