# Lộ trình học và phương pháp học tập trong khóa học DotNet Modular Monolith

---

## 📌 1. Tổng quan lộ trình khóa học

Khóa học được chia thành **3 giai đoạn chính**:

---

### ✅ Giai đoạn 1: Khởi tạo giải pháp & cấu hình ban đầu

- **Tạo Solution Structure**
  - Xây dựng kiến trúc ban đầu theo Modular Monolith
  - Thiết lập các thư mục, project trong Visual Studio
  - Cấu hình Docker Compose, Serilog, Dependency Injection...

- **Wiring Dependencies**
  - Thiết lập kết nối DI giữa các module
  - Đảm bảo khả năng tương tác linh hoạt và dễ bảo trì

---

### ✅ Giai đoạn 2: Phát triển các module nghiệp vụ

> Mỗi module tuân theo Vertical Slice Architecture và áp dụng DDD.

- **1. Catalog Module**
  - Module đầu tiên, nền tảng để xây dựng các module còn lại
  - Áp dụng Vertical Slice, CQRS, MediatR
  - CRUD sản phẩm, Domain Events, EF Core Code First

- **2. Basket Module**
  - Tích hợp Redis làm cache phân tán
  - Áp dụng Proxy, Decorator, Cache-Aside pattern
  - Giao tiếp đồng bộ với Catalog module để lấy giá sản phẩm

- **3. Identity Module**
  - Tích hợp Keycloak cho xác thực người dùng
  - Cấu hình OAuth2, OpenID Connect, Docker Compose
  - Bảo vệ API bằng Bearer Token

- **4. Ordering Module**
  - Tiêu thụ sự kiện Checkout từ Basket qua RabbitMQ
  - Áp dụng Outbox Pattern để đảm bảo gửi sự kiện tin cậy
  - Quản lý đơn hàng: shipping, billing, payment...

---

### ✅ Giai đoạn 3: Giao tiếp giữa các module

- **Synchronous Communication**
  - Dùng in-process method call (gọi hàm trực tiếp)
  - Ví dụ: Basket gọi Catalog để lấy giá & tên sản phẩm

- **Asynchronous Communication**
  - Dùng RabbitMQ + MassTransit
  - Các use case:
    - Giá sản phẩm thay đổi
    - Sự kiện Checkout từ Basket → Ordering
  - Áp dụng Outbox Pattern để đảm bảo gửi sự kiện an toàn

---

## 🧠 2. Phương pháp học tập (Way of Learning)

Khóa học sử dụng mô hình học tập **4 bước**, lặp lại trong từng phần:

---

### 🔍 Bước 1: **Phân tích (Analyze)**
- Hiểu yêu cầu nghiệp vụ (domain)
- Phân tích kỹ thuật và khả năng mở rộng
- Thiết kế kiến trúc phù hợp cho module

---

### 📘 Bước 2: **Học lý thuyết (Learn)**
- Nắm vững mẫu kiến trúc, nguyên lý, pattern liên quan:
  - DDD, Vertical Slice, CQRS, Outbox, DI, SOLID...
- Đảm bảo kiến thức nền trước khi code

---

### 🧑‍💻 Bước 3: **Phát triển & Kiểm thử (Develop & Test)**
- Viết mã thực tế cho module
- Viết test, chạy thử nghiệm local
- Sửa lỗi và cải tiến theo phản hồi

---

### 🚀 Bước 4: **Triển khai (Deploy)**
- Container hóa bằng Docker
- Orchestrate bằng Docker Compose
- Mô phỏng môi trường production

---

## ✅ Kết luận

Kết hợp lộ trình thực hành theo module + phương pháp học 4 bước, bạn sẽ:
- Nắm rõ từng phần của hệ thống Modular Monolith
- Thành thạo từ thiết kế đến triển khai thực tế
- Tự tin xây dựng ứng dụng doanh nghiệp với .NET hiện đại
