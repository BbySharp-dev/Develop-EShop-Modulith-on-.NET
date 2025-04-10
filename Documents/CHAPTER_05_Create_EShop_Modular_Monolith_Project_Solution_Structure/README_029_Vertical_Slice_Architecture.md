# Vertical Slice Architecture – Kiến trúc cắt dọc theo tính năng

---

## 🎯 Mục tiêu

Giới thiệu kiến trúc Vertical Slice – một cách tổ chức mã nguồn theo **tính năng (feature/use case)** thay vì theo tầng kỹ thuật (layer), được đề xuất bởi **Jimmy Bogard**.

---

## 🧭 So sánh với kiến trúc truyền thống

### 🧱 Layered Architecture (Truyền thống – chia ngang)

Presentation Layer 
        ↓ 
Application / Business Logic Layer 
        ↓ 
Data Access Layer


➡ Code được tổ chức theo tầng kỹ thuật (Controller, Services, Repository…)

---

### 🔪 Vertical Slice Architecture (Chia theo tính năng)

[AddProduct Feature] 
├── Request DTO 
├── Command / Query Handler 
├── Validator 
├── Domain Logic (nếu có) 
├── Persistence / DbContext call


➡ Mỗi tính năng được đóng gói độc lập – từ UI đến Database

---

## 🧩 Đặc điểm của Vertical Slice Architecture

| Đặc điểm                        | Mô tả |
|---------------------------------|-------|
| ✅ Tổ chức theo **tính năng**     | Mỗi slice là 1 tính năng riêng biệt |
| ✅ **Tự chứa, độc lập**           | Mỗi slice xử lý toàn bộ luồng: request → xử lý → phản hồi |
| ✅ **Giảm phụ thuộc**            | Không cần service/repo “toàn cục”, slice chỉ phụ thuộc nội bộ |
| ✅ Phù hợp **cross-functional team** | 1 team có thể build/test/deploy 1 feature độc lập |
| ✅ **Dễ mở rộng và bảo trì**     | Dễ thêm tính năng mới mà không ảnh hưởng hệ thống |
| ✅ **Tối ưu hóa cho Agile/DevOps** | Hỗ trợ triển khai nhanh, CI/CD, incremental delivery |

---

## 📈 Lợi ích khi dùng Vertical Slice

1. **Tập trung phát triển theo feature** → dễ ưu tiên và phân công
2. **Giảm xung đột merge** → mỗi team làm slice riêng
3. **Refactor dễ dàng** → không ảnh hưởng toàn hệ thống
4. **Tích hợp tốt với DDD** → mỗi slice tương ứng với use case trong bounded context
5. **Tăng tốc độ release** → có thể test & deploy theo từng slice

---

## ⚠️ Hạn chế cần lưu ý

| Hạn chế                        | Giải pháp |
|-------------------------------|-----------|
| Có thể lặp code giữa các slice| Trích xuất Shared/Helper nếu thực sự cần |
| Khó tiếp cận với người quen kiến trúc tầng | Huấn luyện lại tư duy theo use case |
| Yêu cầu xác định ranh giới slice rõ ràng | Áp dụng DDD, vẽ sơ đồ use case trước khi code |

---

## 🔧 Ứng dụng vào dự án hiện tại

| Module     | Ứng dụng Vertical Slice |
|------------|--------------------------|
| `Catalog`  | ✅ – nhiều CRUD & use case riêng biệt |
| `Basket`   | ✅ – trạng thái thay đổi liên tục, dùng event |
| `Ordering` | ✅ – kết hợp Vertical Slice + Clean Architecture |
| `Identity` | ❌ – module tích hợp Keycloak, không có use case nội bộ nhiều |

---

## 🧠 Kết luận

- Vertical Slice Architecture là **cách tổ chức mã theo tính năng**
- Giúp tăng khả năng mở rộng, bảo trì, phù hợp Agile
- Đặc biệt hiệu quả khi áp dụng trong kiến trúc:
  - Modular Monolith
  - Microservices nội bộ

> 👉 “Think in features, not in layers”

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Vertical Slice Architecture

### 🟢 Cơ bản:
1. Vertical Slice Architecture là gì?
2. Vertical Slice khác gì với Layered Architecture?
3. Lợi ích lớn nhất khi dùng Vertical Slice là gì?

### 🔵 Trung cấp:
4. Làm sao để tổ chức folder Vertical Slice trong module?
5. Một Vertical Slice thường gồm những thành phần nào?
6. Khi nào nên dùng Vertical Slice và khi nào không?

### 🔴 Chuyên sâu:
7. Làm sao để kết hợp Vertical Slice với DDD hiệu quả?
8. Làm sao viết test cho từng slice một cách độc lập?
9. Làm sao quản lý shared logic giữa nhiều slice mà không phá vỡ tính tự chứa?

