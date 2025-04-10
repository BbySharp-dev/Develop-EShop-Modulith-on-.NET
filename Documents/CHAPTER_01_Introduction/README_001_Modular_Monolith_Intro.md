# Khóa học DotNet Backend Bootcamp - Kiến trúc Modular Monolith

## 👋 Giới thiệu
Chào mừng đến với khóa học **DotNet Backend Bootcamp** – một kiến trúc sư phần mềm chuyên sâu vào kiến trúc **Modular Monolith** trên nền tảng .NET.

### 📚 Nội dung chính của khóa học:
- **Mẫu kiến trúc**: Modular Monolith, Vertical Slice Architecture, Domain-Driven Design (DDD), Outbox Pattern
- **Công nghệ sử dụng**: ASP.NET 8, PostgreSQL, Redis, RabbitMQ, Keycloak, Docker, MassTransit, Entity Framework Core, MediatR, Carter

---

## 🧱 Tại sao chọn Modular Monolith?

### ❗ Từ Monolith đến Microservices
- **Monolith truyền thống**: triển khai đơn giản ban đầu, nhưng khó mở rộng và bảo trì khi hệ thống lớn.
- **Microservices**: linh hoạt, mở rộng tốt, nhưng rất phức tạp (giao tiếp mạng, đảm bảo dữ liệu, logging, bảo mật…)
- **Modular Monolith** = kết hợp ưu điểm của cả hai:
  - Phân chia module theo miền nghiệp vụ như Microservices
  - Chạy cùng một tiến trình => không cần quản lý giao tiếp mạng
  - Dễ dàng chuyển hóa dần từng module thành Microservice sau này

---

## 🔍 Tổng quan kiến trúc khóa học

### 📦 Các module chính
- **Catalogue**
- **Basket**
- **Ordering**
- **Identity**

Mỗi module:
- Có **schema riêng** trong cùng PostgreSQL
- Giao tiếp nội bộ qua **method call trong cùng tiến trình**
- Giao tiếp bất đồng bộ sử dụng **RabbitMQ + MassTransit**

---

## 🔐 Bảo mật
- Dùng **Keycloak** làm nhà cung cấp xác thực (OpenID Connect)
- Tích hợp qua **Docker Compose**

---

## 🧪 Chi tiết module Catalogue
- Dùng **Minimal APIs** với .NET 8 & C# 12
- Áp dụng **Vertical Slice Architecture** với folder theo chức năng
- Kết hợp **DDD + MediatR**
- Xử lý Domain Events + Integration Events
- Dùng **EF Core Code First** với PostgreSQL
- Dùng **Carter** để khai báo endpoints
- Xử lý cross-cutting concerns: Logging (Serilog), Validation (MediatR Pipeline), Pagination, Exception Handling

---

## 🧪 Module Basket
- Tương tự Catalogue (Vertical Slice + DDD)
- Sử dụng **Redis** làm cache phân tán
- Áp dụng:
  - Proxy & Decorator Pattern
  - Cache-aside Pattern
- Giao tiếp đồng bộ: method call qua **MediatR**
- Giao tiếp bất đồng bộ: RabbitMQ + Integration Events

---

## 🧪 Module Ordering
- Cùng nền tảng kiến trúc (Vertical Slice + DDD)
- Áp dụng **Outbox Pattern**:
  - Lưu thông tin sự kiện vào bảng outbox cùng lúc với dữ liệu chính
  - Một process riêng sẽ xuất sự kiện ra RabbitMQ (MassTransit)
- Ordering module sẽ tiêu thụ sự kiện và tiến hành đặt hàng

---

## 🧪 Module Identity
- Xây dựng chức năng xác thực người dùng với **Keycloak**
- Thực hiện các flow xác thực OAuth2/OpenID
- Bảo vệ các API bằng **Bearer Token**

---

## 🔁 Lộ trình tiến hóa: từ Monolith đến Microservices
- Bắt đầu từ Modular Monolith
- Di chuyển dần từng module thành Microservice bằng **Strangler Fig Pattern**
- Thực hành:
  - Cô lập dữ liệu & logic theo module
  - Xác định public API
  - Dùng sự kiện để giao tiếp
  - Chuẩn bị cho triển khai độc lập

---

## 🎯 Mục tiêu cuối cùng
Sau khóa học, bạn sẽ:
- Nắm vững phát triển backend với .NET
- Áp dụng thành thạo các mẫu kiến trúc hiện đại
- Sẵn sàng xây dựng ứng dụng doanh nghiệp theo chuẩn **modular, cloud-native**

> ⚒️ 95% khóa học là thực hành: bạn sẽ tự tay phát triển từng module, áp dụng các pattern và đóng gói bằng Docker để triển khai.

---

## 🛠 Công cụ và kỹ thuật sử dụng
- CQRS, MediatR
- DDD với Aggregates & Value Objects
- EF Core Code First
- RabbitMQ + MassTransit
- Docker Compose
- Keycloak cho xác thực
- Carter cho endpoint ngắn gọn
- Serilog cho logging có cấu trúc
