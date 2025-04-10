# Cấu trúc mã nguồn của hệ thống Modular Monolith

## 🎯 Mục tiêu

Tài liệu này giúp bạn hiểu cách tổ chức mã nguồn trong giải pháp **Modular Monolith** sử dụng .NET. Việc nắm vững cấu trúc này sẽ giúp bạn:

- Làm chủ khả năng mở rộng và bảo trì hệ thống
- Tách biệt rõ ràng từng module nghiệp vụ
- Sẵn sàng chuyển đổi sang Microservices khi cần thiết

---

## 🧭 Cấu trúc tổng thể của Solution

/SolutionRoot 
├── Bootstrapper // Điểm khởi đầu ứng dụng 
├── Modules // Các module nghiệp vụ độc lập 
├── Shared // Các thành phần chia sẻ dùng chung 
├── docker-compose.yml // Tập tin cấu hình môi trường chạy

---

## 1️⃣ Bootstrapper – Điểm khởi động API

**Vai trò:**  
- Là nơi chứa dự án Web API chính (ASP.NET Core)
- Chịu trách nhiệm khởi tạo ứng dụng, routing request đến các module
- Tích hợp các thư viện như: Carter (đăng ký endpoints), Serilog, cấu hình Swagger

**Thành phần chính:**
- Khởi tạo `WebApplication`
- Gọi `MapCarter()` để tự động đăng ký tất cả endpoint từ các module
- Cấu hình các Middleware toàn cục: xác thực, logging, exception handler...

---

## 2️⃣ Modules – Trái tim của ứng dụng

**Vai trò:**  
- Mỗi module đại diện cho một **miền nghiệp vụ độc lập**: Catalog, Basket, Ordering...
- Tự quản lý logic, dữ liệu, validation, API riêng
- Dựa theo **Vertical Slice Architecture** & **Domain-Driven Design (DDD)**

### Cấu trúc bên trong mỗi module

#### 📁 Data/
- Chứa lớp DbContext, định nghĩa schema cho module đó
- Dùng **EF Core - Code First**
- Có thư mục Migrations để quản lý thay đổi cơ sở dữ liệu

#### 📁 Features/
- Chứa các Use Case – ví dụ: Tạo sản phẩm, Lấy danh sách sản phẩm...
- Mỗi use case là một thư mục riêng, gồm:
  - Endpoint: định nghĩa route và HTTP method
  - Request: input dữ liệu từ client
  - Handler: xử lý chính của use case (dùng MediatR)
  - Response (tuỳ chọn): dữ liệu trả về cho client

#### 📁 Domain/
- Chứa các thực thể nghiệp vụ (Entities), giá trị (ValueObjects), quy tắc nghiệp vụ
- Thiết kế theo nguyên tắc **Aggregate Root** và **Domain Integrity**
- Tách biệt logic nghiệp vụ khỏi tầng giao tiếp và lưu trữ

#### 📁 Events/
- Chứa Domain Events và Integration Events
- Sử dụng để phát tán sự kiện trong hệ thống, đồng bộ hoặc bất đồng bộ

---

## 3️⃣ Shared – Thư viện dùng chung

**Vai trò:**  
- Tập trung các phần tái sử dụng giữa các module
- Đảm bảo nguyên lý **Don't Repeat Yourself (DRY)**

**Thành phần điển hình:**
- Logging (Serilog)
- Validation (FluentValidation, MediatR Pipeline)
- Middleware xử lý lỗi
- Pagination helpers
- Abstractions dùng cho bảo mật, sự kiện, cấu hình chung
- Các lớp cơ sở dùng cho các Event, Command, Query...

---

## 4️⃣ Docker Compose – Môi trường chạy

**Vai trò:**
- Khởi động toàn bộ ứng dụng và các dịch vụ nền trong môi trường Docker

**Bao gồm:**
- Các module ứng dụng chạy nền ASP.NET Core
- PostgreSQL (CSDL chính)
- Redis (Cache phân tán)
- RabbitMQ (Giao tiếp bất đồng bộ)
- Keycloak (Xác thực người dùng)

**Tập tin cấu hình:**
- `docker-compose.yml`
- `docker-compose.override.yml`

> Cho phép chạy toàn bộ hệ thống như trong môi trường production giả lập

---

## 🔁 Giao tiếp giữa các module

- **Đồng bộ (Synchronous):**
  - Gọi trực tiếp qua method trong cùng tiến trình
  - Dùng MediatR để gọi lẫn nhau giữa các module

- **Bất đồng bộ (Asynchronous):**
  - Gửi sự kiện qua RabbitMQ
  - Kết hợp với **Outbox Pattern** để đảm bảo độ tin cậy (Reliable Messaging)

---

## 📌 Tổng kết

| Thành phần     | Mô tả                                                                 |
|----------------|----------------------------------------------------------------------|
| Bootstrapper   | Điểm khởi động Web API, định tuyến và cấu hình toàn hệ thống        |
| Modules        | Chứa nghiệp vụ từng phần, áp dụng DDD và Vertical Slice              |
| Shared         | Thành phần dùng chung, tái sử dụng giữa các module                   |
| Docker Compose | Khởi chạy tất cả module và dịch vụ nền trong môi trường nhất quán   |

---

## 🧠 Ghi nhớ

- Mỗi module như một ứng dụng thu nhỏ: độc lập về dữ liệu, logic và giao tiếp
- Code dễ hiểu nhờ tổ chức theo tính năng thay vì kiểu truyền thống (Controller/Service/Repo)
- Kiến trúc giúp hệ thống **dễ mở rộng**, **dễ bảo trì**, sẵn sàng cho Microservice nếu cần

