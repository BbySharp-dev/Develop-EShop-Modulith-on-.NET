# Phân rã hệ thống theo Bounded Context – Kiến trúc Modular Monolith

---

## 🧠 Khái niệm cốt lõi: Bounded Context

- **Bounded Context** là một mẫu (pattern) quan trọng trong Domain-Driven Design (DDD)
- Nó định nghĩa **ranh giới logic** mà trong đó **một mô hình domain nhất định được áp dụng**
- Mỗi **module** trong kiến trúc Modular Monolith nên tương ứng với **một bounded context rõ ràng**

---

## 🧩 Mục tiêu của việc phân rã theo Bounded Context

| Mục tiêu                        | Mô tả |
|----------------------------------|------|
| ✅ Phân chia hệ thống theo domain | Mỗi module đại diện cho 1 mảng nghiệp vụ cụ thể |
| ✅ Tăng tính độc lập giữa modules | Giảm coupling, tăng maintainability |
| ✅ Dễ mở rộng, dễ kiểm thử        | Mỗi module có scope riêng, chức năng rõ ràng |
| ✅ Chuẩn bị cho Microservices     | Có thể tách từng module sau này nếu cần |

---

## 🪜 Cách xác định Bounded Context trong hệ thống ERP

Đặt các câu hỏi để định danh domain:
- Hệ thống cần phục vụ nghiệp vụ gì?
- Các thực thể (entity) và quy trình chính là gì?
- Các phần nào tương tác với nhau?
- Mỗi phần cần quyền truy cập dữ liệu nào?

---

## 🏗️ Các module chính trong hệ thống & vai trò (Bounded Context)

---

### 1. **📦 Catalog Module** – *Product Information Management*

**Chức năng chính:**
- Quản lý thông tin sản phẩm: thêm, sửa, xóa
- Quản lý danh mục (categories)
- Quản lý giá (pricing), giảm giá (discount)

**Use Cases:**
- Thêm sản phẩm mới
- Cập nhật giá sản phẩm
- Xóa sản phẩm
- Áp dụng chính sách khuyến mãi

---

### 2. **🛒 Basket Module** – *Shopping Cart Management*

**Chức năng chính:**
- Quản lý giỏ hàng người dùng
- Tính tổng tiền
- Đồng bộ thông tin sản phẩm với Catalog

**Use Cases:**
- Thêm/sửa/xóa item trong giỏ hàng
- Tính toán tổng số tiền
- Giao tiếp bất đồng bộ với Catalog (RabbitMQ + MassTransit)
- Dùng Redis để cache thông tin giỏ hàng

---

### 3. **👤 Identity Module** – *User Authentication & Authorization*

**Chức năng chính:**
- Quản lý người dùng
- Xác thực (login), phân quyền (roles)
- Kết nối với hệ thống Keycloak

**Use Cases:**
- Đăng ký người dùng mới
- Đăng nhập
- Cấp token bảo mật (OAuth2 / OpenID Connect)
- Bảo vệ API bằng bearer token

---

### 4. **📑 Ordering Module** – *Order Management*

**Chức năng chính:**
- Quản lý vòng đời đơn hàng
- Thanh toán & vận chuyển
- Giao tiếp bất đồng bộ với Basket

**Use Cases:**
- Tạo đơn hàng từ giỏ hàng
- Xác nhận thanh toán, xử lý vận chuyển
- Gửi sự kiện thông qua Outbox Pattern (đảm bảo độ tin cậy)

---

## 🧱 Tổng quan giao tiếp giữa các modules

| Module      | Giao tiếp với       | Hình thức       |
|-------------|----------------------|------------------|
| Basket      | Catalog              | In-process + Event-driven |
| Ordering    | Basket               | Event-driven (Outbox) |
| Identity    | Tất cả               | REST API + Token (Keycloak) |

---

## 📌 Tổng kết

Việc tổ chức hệ thống theo các **bounded context rõ ràng** giúp:
- Dễ phát triển theo domain
- Chuẩn hóa cấu trúc mã nguồn
- Chuẩn bị tốt cho việc tách module thành Microservices nếu cần

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Bounded Context & Module Decomposition

### 🟢 Cơ bản:
1. Bounded Context là gì? Vì sao lại quan trọng trong kiến trúc Modular Monolith?
2. Mỗi module trong hệ thống nên tương ứng với điều gì trong DDD?
3. Ví dụ về một module tương ứng với Bounded Context trong hệ thống ERP?

### 🔵 Trung cấp:
4. Làm sao để xác định ranh giới giữa các module trong một hệ thống lớn?
5. Sự khác biệt giữa chia module theo kỹ thuật (technical layer) và theo domain?
6. Vì sao module Identity nên được tách trước khi các module khác?

### 🔴 Chuyên sâu:
7. Làm sao để giữ module “loose coupling” khi chúng cần giao tiếp với nhau thường xuyên?
8. Nếu hai module chia sẻ chung dữ liệu, bạn sẽ xử lý như thế nào?
9. Làm sao để tích hợp CQRS và Event Sourcing cho từng bounded context?

