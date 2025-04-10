# Modular Monolith Architecture – Kiến trúc đơn khối mô-đun hóa

---

## 🧩 Modular Monolith là gì?

**Modular Monolith** (hoặc Modular Architecture) là mô hình kiến trúc trung gian giữa **Monolithic** và **Microservices**:

> Ứng dụng được xây dựng và triển khai như **một khối thống nhất**, nhưng **bên trong được chia thành các module độc lập rõ ràng**, đại diện cho các **Bounded Context** riêng biệt.

### ✅ Mục tiêu:
- Kết hợp **sự đơn giản** của Monolith với **tính tổ chức, mở rộng** của Microservices
- Giảm độ phức tạp về triển khai và giao tiếp giữa service
- Dễ bảo trì, dễ refactor, và **có khả năng chuyển hóa dần sang microservices**

---

## 🔍 Đặc điểm chính của Modular Monolith

### 1. **Modularity & Bounded Context**
- Chia rõ domain theo từng module độc lập
- Mỗi module có logic nghiệp vụ và data riêng (ít nhất là theo schema)

### 2. **Triển khai đơn khối**
- Ứng dụng được **build & deploy dưới dạng một unit duy nhất**
- Không cần orchestrate nhiều pipeline CI/CD
- Giảm độ phức tạp về mặt vận hành

### 3. **Giao tiếp giữa module (In-process)**
- Dùng method call trực tiếp hoặc domain events trong cùng tiến trình
- Không có độ trễ mạng như Microservices
- Giao dịch có thể quản lý tập trung dễ dàng

### 4. **Quản lý dữ liệu thống nhất**
- Một database duy nhất, nhưng phân chia theo **schema riêng biệt cho mỗi module**
- Dễ quản lý tính toàn vẹn dữ liệu
- Nếu cần, vẫn có thể tách riêng database theo module

---

## 🏗️ Kiến trúc tổng quan

### Các module chính trong hệ thống ví dụ (ICAP):

| Module         | Chức năng chính |
|----------------|-----------------|
| **Catalog**    | Quản lý sản phẩm, giá, tồn kho |
| **Basket**     | Xử lý giỏ hàng: thêm, sửa, xóa item |
| **Ordering**   | Quản lý quy trình tạo đơn hàng |
| **Identity**   | Xác thực, phân quyền người dùng với Keycloak |

---

### Mỗi module gồm:
- **Class Library riêng biệt**
- Có đầy đủ các lớp:
  - Data Access (EF Core)
  - Business Logic
  - API nội bộ (exposed qua interface hoặc domain event)
- Giao tiếp qua:
  - **Public interface**
  - **Domain events**

---

## 🎯 Lợi ích của Modular Monolith

| Lợi ích                         | Mô tả |
|----------------------------------|------|
| ✅ Tổ chức theo Domain           | Áp dụng DDD rõ ràng, chia domain hợp lý |
| ✅ Dễ bảo trì, mở rộng từng phần | Mỗi module độc lập, ít ảnh hưởng nhau |
| ✅ Giao tiếp nhanh, không mạng  | Dùng method call thay vì HTTP/gRPC |
| ✅ Tối ưu chi phí vận hành       | Không cần orchestrate nhiều container |
| ✅ Dễ migrate sang Microservices | Có thể tách từng module dần dần khi cần |

---

## ⚠️ Khi nào nên dùng Modular Monolith?

- Dự án có **domain rõ ràng** nhưng chưa đủ lớn để chia thành Microservices
- Đội dev chưa có DevOps chuyên sâu
- Cần đơn giản về triển khai nhưng vẫn muốn code base tách biệt tốt
- Là bước **chuyển tiếp lý tưởng** từ Monolith lên Microservices

---

## 🧠 Tổng kết

> Modular Monolith = “Monolith thông minh”  
> Xây dựng ứng dụng có tổ chức, module hóa, dễ phát triển, dễ bảo trì, dễ tách ra Microservices nếu cần.

Đây là mô hình **rất phù hợp với các đội vừa và nhỏ**, hoặc các dự án dài hơi, nơi tính linh hoạt, tổ chức và tiết kiệm chi phí là ưu tiên hàng đầu.

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Modular Monolith Architecture

### 🟢 Cơ bản:
1. Modular Monolith là gì? Nó nằm giữa kiến trúc nào?
2. Điểm khác biệt giữa Modular Monolith và Monolith truyền thống là gì?
3. Mỗi module nên được thiết kế như thế nào trong kiến trúc này?

### 🔵 Trung cấp:
4. Vì sao Modular Monolith vẫn được triển khai dưới dạng một đơn vị duy nhất?
5. Giao tiếp giữa các module trong Modular Monolith nên được thực hiện ra sao?
6. Quản lý dữ liệu trong Modular Monolith như thế nào cho hợp lý?

### 🔴 Chuyên sâu:
7. Khi nào bạn nên tách một module trong Modular Monolith thành Microservice?
8. Làm sao để tránh Distributed Monolith trong quá trình phát triển Modular Monolith?
9. Bạn sẽ thiết kế và kiểm thử module độc lập như thế nào trong kiến trúc này?

