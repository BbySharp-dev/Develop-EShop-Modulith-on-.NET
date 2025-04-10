# External vs Internal Architecture trong Modular Monolith

---

## 🎯 Mục tiêu

Hiểu rõ sự khác biệt giữa **kiến trúc bên ngoài (External Architecture)** và **kiến trúc bên trong (Internal Architecture)** trong hệ thống Modular Monolith.

---

## 🧩 1. External Architecture – Kiến trúc bên ngoài

### ✔ Định nghĩa:

External Architecture mô tả cách hệ thống Modular Monolith giao tiếp với các thành phần bên ngoài như:

- Người dùng (qua Web, Mobile App, Admin...)
- Các dịch vụ nền tảng (cloud-native backing services)
- Hệ thống bên thứ ba (nếu có)

### ✔ Thành phần chính:

1. **Client Applications**  
   Gửi request đến API thông qua HTTP (REST).

2. **Bootstrapper API (Entrypoint)**  
   - Là ASP.NET Core Web API chính.  
   - Nhận request, xử lý các middleware như xác thực, logging.  
   - Định tuyến đến các module nội bộ.

3. **Modules (bên trong monolith)**  
   - Mỗi module xử lý logic nghiệp vụ riêng biệt.  
   - Giao tiếp nội bộ qua method call hoặc message.

4. **Cloud-native Services**  
   - **PostgreSQL**: lưu trữ dữ liệu.  
   - **Redis**: cache dữ liệu tạm thời (Basket, Session...).  
   - **RabbitMQ**: giao tiếp bất đồng bộ giữa các module.  
   - **Keycloak**: xác thực người dùng (OAuth2 / OpenID).  
   - **Docker / Seq / Logging Services**: môi trường và giám sát.

### 👉 Tóm tắt luồng đi:

**Client → Bootstrapper API → Module xử lý → Trả kết quả → Client**  
Trong quá trình xử lý, các module có thể gọi đến database, Redis hoặc gửi sự kiện qua RabbitMQ nếu cần.

---

## 🧱 2. Internal Architecture – Kiến trúc bên trong (per module)

### ✔ Định nghĩa:

Internal Architecture mô tả cách **mỗi module được thiết kế, tổ chức và vận hành** bên trong ứng dụng Modular Monolith.

### ✔ Mỗi module có thể chọn kiến trúc riêng phù hợp với độ phức tạp:

| Module     | Kiến trúc nội bộ đề xuất                     | Lý do chọn |
|------------|----------------------------------------------|------------|
| `Catalog`  | Vertical Slice + DDD + Mediator              | Nhiều use case đơn, CRUD nhiều |
| `Basket`   | Vertical Slice + Redis Cache + Integration Events | Luôn thay đổi trạng thái giỏ hàng |
| `Ordering` | Vertical Slice + Clean Architecture + Outbox | Logic nghiệp vụ phức tạp, nhiều bước xử lý |
| `Identity` | Tương tác Keycloak qua REST API              | Chỉ giao tiếp xác thực, không xử lý logic bên trong |

### ✔ Tự do kiến trúc nội bộ – nhưng cần tuân thủ:

- Không phụ thuộc chéo (no tight coupling)
- Có khả năng test độc lập
- Có thể tách ra làm Microservice nếu cần

---

## 💡 Tổng kết

| Thành phần       | Mục tiêu                                           |
|------------------|----------------------------------------------------|
| **External Architecture** | Giao tiếp bên ngoài: API, DB, Redis, RabbitMQ... |
| **Internal Architecture** | Tổ chức logic bên trong từng module          |

- Bạn có thể dùng **kiến trúc khác nhau cho từng module** nếu cần
- Không nên “over-architecture” những module đơn giản
- Nên chuẩn hóa mẫu kiến trúc (VD: Vertical Slice) cho phần lớn module để dễ bảo trì

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề External vs Internal Architecture

### 🟢 Cơ bản:
1. External Architecture là gì? Internal Architecture là gì?
2. Mỗi module có thể dùng kiến trúc nội bộ khác nhau không?
3. Các dịch vụ nền (Redis, RabbitMQ, Keycloak...) nằm ở tầng nào?

### 🔵 Trung cấp:
4. Khi nào nên dùng Vertical Slice Architecture thay vì kiến trúc truyền thống?
5. Ordering module nên dùng kiến trúc nào? Vì sao?
6. Làm sao để module giao tiếp với nhau mà vẫn giữ tính module hóa?

### 🔴 Chuyên sâu:
7. Làm sao chọn kiến trúc nội bộ phù hợp mà không over-engineer?
8. Làm sao để test từng module một cách độc lập trong kiến trúc monolith?
9. Nếu module cần tách thành microservice sau này, kiến trúc nội bộ cần đáp ứng điều gì?

