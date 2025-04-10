# Tạo các thư mục chính trong Solution – Modular Monolith Structure

---

## 🎯 Mục tiêu

Thiết lập 3 thư mục logic trong solution để tổ chức các thành phần chính của kiến trúc Modular Monolith:

- `Bootstrapper/`: Entry point (Web API)
- `Modules/`: Các module nghiệp vụ
- `Shared/`: Các thành phần dùng chung (cross-cutting concerns)

---

## 🪜 Các bước thực hiện

1. Click phải vào tên Solution → `Add → New Solution Folder`
2. Tạo lần lượt 3 folder:
   - `Bootstrapper`
   - `Modules`
   - `Shared`

---

## 📁 Cấu trúc thư mục sau khi tạo

Shop.ModularMonoliths.sln 
└── Solution Items 
├── Bootstrapper/ 
├── Modules/ 
└── Shared/

---

## 🧱 Mô tả chi tiết từng thư mục

---

### 1. 📌 `Bootstrapper/` – Entry Point

- Chứa project `Escape.API` (ASP.NET Core Web API)
- Là điểm khởi động chính của toàn ứng dụng
- Cấu hình:
  - `Program.cs`: thiết lập web host, middleware, route
  - `DI`: đăng ký các module
  - `Swagger`, `Logging`, `Auth`, `ExceptionHandling`
- Chịu trách nhiệm định tuyến và expose các endpoint từ các module

---

### 2. 📦 `Modules/` – Các Bounded Context nghiệp vụ

- Chứa các **Class Library project** tương ứng với từng domain chính
- Mỗi module = 1 Bounded Context độc lập

#### Ví dụ các module:

- `Catalog`: Quản lý sản phẩm
- `Basket`: Quản lý giỏ hàng
- `Ordering`: Quản lý đơn hàng
- `Identity`: Quản lý người dùng (Auth & RBAC với Keycloak)

#### Mỗi module sẽ có cấu trúc như sau:

Modules/ 
└── Catalog/ 
        ├── Features/ # Vertical Slice – use case theo từng chức năng 
        ├── Data/ # EF Core, DbContext, Migrations 
        ├── Domain/ # Entities, ValueObjects 
        └── Events/ # Domain events & Integration events

---

### 3. 🛠 `Shared/` – Dùng chung (Cross-cutting concerns)

#### Mục đích:
- Chia sẻ các thư viện, contract, event, logic tái sử dụng giữa các module

#### Các class library con (gợi ý):

- `Shared.Common`
  - Helpers, extension methods
  - Logging config, exception middleware
- `Shared.Contracts`
  - Interface và DTO cho giao tiếp đồng bộ (in-process)
  - Chuẩn hóa API nội bộ giữa các module
- `Shared.Messaging`
  - Cấu hình RabbitMQ, MassTransit
  - Định nghĩa Integration Events và các Event Handler

---

## ✅ Lợi ích khi tổ chức theo cấu trúc này

| Lợi ích                       | Mô tả |
|-------------------------------|------|
| ✅ Separation of concerns      | Tách rõ logic domain, entrypoint, concerns dùng chung |
| ✅ Dễ mở rộng, scale module    | Mỗi module độc lập, dễ refactor, dễ tách |
| ✅ Dễ quản lý dependencies     | Module chỉ phụ thuộc vào thư viện cần thiết |
| ✅ Hướng tới clean architecture| Giảm coupling, tăng maintainability |

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Tổ chức cấu trúc Solution

### 🟢 Cơ bản:
1. Vai trò của thư mục `Bootstrapper` trong Modular Monolith là gì?
2. Tại sao cần chia `Shared` thành các class library con như `Common`, `Contracts`, `Messaging`?
3. Mỗi module nên tương ứng với điều gì trong Domain-Driven Design?

### 🔵 Trung cấp:
4. Làm sao để thiết kế folder `Features` theo Vertical Slice Architecture?
5. `Shared.Contracts` và `Shared.Messaging` khác nhau như thế nào?
6. Nếu hai module cần giao tiếp, bạn sẽ cấu trúc thư viện chia sẻ ra sao?

---

