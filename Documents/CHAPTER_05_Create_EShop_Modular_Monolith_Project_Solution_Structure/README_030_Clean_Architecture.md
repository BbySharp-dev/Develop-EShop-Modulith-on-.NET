# Clean Architecture – Kiến trúc sạch theo Uncle Bob

---

## 🎯 Mục tiêu

Giới thiệu kiến trúc **Clean Architecture** được đề xuất bởi **Robert C. Martin (Uncle Bob)** – một mô hình kiến trúc phần mềm tập trung vào **separation of concerns**, giúp hệ thống **độc lập với UI, Database và Framework**, dễ mở rộng, dễ test và dễ bảo trì.

---

## 🧱 Các nguyên tắc cốt lõi của Clean Architecture

| Nguyên tắc                        | Giải thích |
|----------------------------------|------------|
| ✅ **Independence of Frameworks** | Không phụ thuộc framework cụ thể (ASP.NET, EF Core...) |
| ✅ **Testability**               | Logic nghiệp vụ có thể test độc lập, không cần UI/DB |
| ✅ **UI Agnostic**               | Có thể thay đổi UI mà không ảnh hưởng business logic |
| ✅ **Database Agnostic**         | Không gắn chặt với một loại DB cụ thể |
| ✅ **External System Agnostic** | Không phụ thuộc vào bên ngoài (REST, Message Queue...) |

---

## 🧩 Cấu trúc tầng trong Clean Architecture

[Entities / Domain Layer] 
            ↑
[Use Cases / Application Layer] 
            ↑ 
[Interface Adapters / Infrastructure Layer] 
            ↑ 
[Frameworks & Drivers]


### 1. 🔹 **Entities Layer (Domain)**

- Chứa: Entities, Value Objects, Business Rules
- Không phụ thuộc bất kỳ tầng nào khác
- Ví dụ: `Order`, `OrderItem`

### 2. 🔹 **Use Case Layer (Application)**

- Chứa các logic nghiệp vụ cụ thể cho từng chức năng
- Ví dụ: `CreateOrder`, `CancelOrder`, `UpdateStatus`

### 3. 🔹 **Interface Adapters (Infrastructure)**

- Là nơi kết nối giữa use case và thế giới bên ngoài
- Gồm: Repositories, Mapping, DTO, Controllers

### 4. 🔹 **Frameworks & Drivers**

- Giao diện ngoài cùng: ASP.NET Controllers, EF Core, Redis, RabbitMQ, v.v.
- Có thể thay đổi mà không ảnh hưởng tầng trên

---

## 📦 Ví dụ: Clean Architecture trong Ordering Module

| Tầng                  | Ví dụ cụ thể |
|-----------------------|--------------|
| Entities (Domain)     | `Order`, `OrderItem`, `OrderStatus` |
| Use Cases (App)       | `CreateOrderHandler`, `CancelOrderHandler` |
| Adapters (Infra)      | `OrderRepository`, `EFCoreDbContext`, `Mappers` |
| Frameworks & Drivers  | ASP.NET Controllers, EF Core, MassTransit |

---

## 📈 Ưu điểm của Clean Architecture

| Ưu điểm       | Lý do |
|---------------|-------|
| ✅ **Modular**     | Thay đổi 1 module không ảnh hưởng các phần khác |
| ✅ **Adaptable**   | Có thể thay DB, framework... dễ dàng |
| ✅ **Testable**    | Core logic test độc lập không cần DB, UI |
| ✅ **Maintainable**| Tách biệt rõ trách nhiệm, dễ đọc, dễ bảo trì |

---

## ⚠️ Nhược điểm cần cân nhắc

- Yêu cầu tổ chức code phức tạp hơn
- Cần hiểu rõ DDD, Dependency Inversion, Layered Dependency
- Có thể over-engineering nếu áp dụng vào module quá đơn giản

---

## 🧠 Khi nào nên dùng Clean Architecture?

- Các module có **nghiệp vụ phức tạp**: nhiều trạng thái, nhiều bước xử lý
- Cần dễ test, dễ thay đổi công nghệ
- Có khả năng scale lớn hoặc migrate thành microservice trong tương lai

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Clean Architecture

### 🟢 Cơ bản:
1. Clean Architecture là gì? Ai là người đề xuất?
2. Tầng Use Case dùng để làm gì?
3. Entities Layer có được phép gọi Repository không?

### 🔵 Trung cấp:
4. Làm sao để clean architecture không bị phụ thuộc vào EF Core?
5. Mối quan hệ giữa Application Layer và Infrastructure Layer nên một chiều hay hai chiều?
6. So sánh Clean Architecture với Layered Architecture truyền thống?

### 🔴 Chuyên sâu:
7. Làm sao để kết hợp Clean Architecture với DDD và Event-Driven?
8. Nếu một module quá đơn giản (VD: chỉ có 2 CRUD), có nên áp dụng full Clean Architecture?
9. Làm sao để triển khai DI (Dependency Injection) đúng trong Clean Architecture?

