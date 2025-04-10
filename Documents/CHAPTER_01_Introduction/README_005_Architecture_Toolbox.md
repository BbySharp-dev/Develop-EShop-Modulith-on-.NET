# Tổng quan kiến trúc, mẫu thiết kế và công cụ sử dụng trong khóa học

## 🎯 Mục tiêu
Khóa học sử dụng **kiến trúc Modular Monolith** với tư duy thiết kế **theo module**, giúp phát triển dễ bảo trì, dễ kiểm thử và mở rộng thành Microservices nếu cần.

---

## 🧱 1. External vs. Internal Architecture

### 📌 External Architecture – Kiến trúc bên ngoài
- Bao gồm: Client Apps, API Gateway, các Microservice hoặc Modules
- Các thành phần giao tiếp qua API Gateway
- Mỗi service có thể dùng công nghệ hoặc kiến trúc khác nhau

### 📌 Internal Architecture – Kiến trúc bên trong mỗi Module
- Mỗi module có thể chọn kiến trúc phù hợp:
  - **N-Layer Architecture**
  - **Vertical Slice Architecture** ✅ (chúng ta sẽ sử dụng)
  - **Clean Architecture**
- Tư duy **polyglot architecture**: chọn đúng công cụ cho từng nghiệp vụ

---

## 🧩 2. Kiến trúc sẽ sử dụng trong khóa học

### ✅ Vertical Slice Architecture
- Chia hệ thống thành các **slices** (từng tính năng riêng biệt)
- Mỗi slice tự xử lý: route, validation, handler, response
- Dễ kiểm thử, dễ bảo trì, dễ mở rộng

### ✅ Domain-Driven Design (DDD)
- Mô hình hóa logic nghiệp vụ theo domain
- Đảm bảo tính rõ ràng, đúng nghiệp vụ, dễ tách module

### ✅ Modular Monolith
- Mỗi module giống như 1 service riêng biệt (có dữ liệu và logic riêng)
- Có thể chuyển đổi sang microservices dễ dàng về sau

---

## 🔧 3. Design Patterns & Nguyên lý áp dụng

| Pattern / Principle             | Vai trò chính |
|---------------------------------|----------------|
| **SOLID**                       | Cốt lõi thiết kế hướng đối tượng tốt |
| **Dependency Injection**        | Giảm phụ thuộc giữa các lớp |
| **CQRS (Command Query Split)**  | Tách đọc và ghi |
| **Mediator**                    | Tách lệnh – giúp module giao tiếp qua trung gian |
| **Proxy / Decorator**           | Thêm hành vi mà không thay đổi lớp gốc |
| **Publish-Subscribe**           | Giao tiếp bất đồng bộ qua sự kiện |
| **Outbox Pattern**              | Đảm bảo gửi message tin cậy qua RabbitMQ |

---

## 🗃️ 4. Quản lý dữ liệu và caching

- **PostgreSQL**: cơ sở dữ liệu chính – hỗ trợ transaction tốt
- **Redis**: cache phân tán – tăng tốc độ truy vấn
- **RabbitMQ + MassTransit**: giao tiếp module bất đồng bộ
- **Outbox Pattern**: chống mất sự kiện khi gửi qua RabbitMQ

---

## 🔐 5. Authentication & Authorization

- Sử dụng **Keycloak**
- Giao thức **OpenID Connect**
- Gửi token theo chuẩn **Bearer Token**
- Tích hợp trong Docker Compose

---

## 🧰 6. Bộ thư viện sử dụng trong dự án .NET

| Thư viện | Mục đích |
|----------|----------|
| **Carter** | Định nghĩa endpoint nhẹ nhàng |
| **MediatR** | Điều phối request/command/event |
| **FluentValidation** | Kiểm tra dữ liệu đầu vào |
| **Mapster** | Mapping đối tượng |
| **MassTransit** | Trừu tượng hóa RabbitMQ |
| **EF Core** | ORM – thao tác với DB |
| **Serilog** | Structured Logging |

---

## 🔁 7. Kiểu giao tiếp giữa các module

### Giao tiếp đồng bộ (synchronous)
- Gọi trực tiếp trong tiến trình (In-process)
- Dùng cho các thao tác như lấy giá sản phẩm khi thêm vào giỏ

### Giao tiếp bất đồng bộ (asynchronous)
- Dùng RabbitMQ + MassTransit
- Các use case:
  - Giá sản phẩm thay đổi
  - Checkout giỏ hàng

---

## 🐳 8. Triển khai và container hóa

- Dùng **Docker** để đóng gói ứng dụng
- Dùng **Docker Compose** để orchestration toàn bộ:
  - Các module
  - PostgreSQL
  - Redis
  - RabbitMQ
  - Keycloak

---

## 📌 Hình minh họa kiến trúc tổng quan

![External vs Internal Architecture](../image.png)

### 💡 Giải thích luồng đi của hình ảnh

1. **Client Apps** (góc trái):
   - Gồm các ứng dụng như mobile app, website, desktop app…
   - Người dùng thực hiện các thao tác như thêm sản phẩm vào giỏ, xem đơn hàng...

2. **API Gateway**:
   - Là cổng duy nhất mà tất cả client gọi tới.
   - Nhận request từ client, định tuyến đến đúng microservice/module phía sau.
   - Có thể xử lý xác thực, logging, caching, hoặc chịu trách nhiệm cho rate limiting, load balancing...

3. **Các Microservices (hoặc Modules)**:
   - Gồm nhiều service/module nhỏ như: Catalog, Basket, Ordering...
   - Mỗi service là một backend nhỏ gọn, độc lập về logic và dữ liệu.
   - Triển khai bằng ASP.NET Core, có thể dùng công nghệ khác nhau nếu cần.

4. **Internal Architecture per Microservice**:
   - Mỗi microservice/module có thể chọn kiến trúc riêng biệt phù hợp với độ phức tạp của nghiệp vụ:
     - **N-Layer Architecture**: tách riêng tầng UI, Business, DataAccess – dễ hiểu nhưng cồng kềnh với tính năng nhỏ.
     - **Vertical Slice Architecture**: chia theo tính năng (use case), dễ quản lý, phù hợp cho tốc độ và bảo trì – **sẽ được dùng trong khóa học**.
     - **Clean Architecture**: hướng đến testability, tách biệt domain với hạ tầng, phù hợp dự án lớn và lâu dài.

➡️ Tổng kết lại, **luồng chính**:
- Client → API Gateway → Microservice → Kiến trúc nội bộ phù hợp → Trả kết quả về client.

---

## ✅ Kết luận

Toàn bộ khóa học sử dụng tư duy:
- Modular → tách module rõ ràng
- DDD → mô hình hóa đúng nghiệp vụ
- Vertical Slice → code gọn, dễ quản lý
- Giao tiếp module hiện đại → sync + async

Bạn sẽ nắm được cách xây dựng backend **hiện đại, mạnh mẽ, sẵn sàng mở rộng** và áp dụng được trong doanh nghiệp thực tế.
