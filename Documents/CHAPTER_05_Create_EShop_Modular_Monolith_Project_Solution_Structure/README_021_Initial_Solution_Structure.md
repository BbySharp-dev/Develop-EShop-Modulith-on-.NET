# Khởi tạo cấu trúc giải pháp dự án Modular Monolith

---

## 🎯 Mục tiêu

Tạo cấu trúc chuẩn để bắt đầu phát triển một ứng dụng **Modular Monolith** bằng ASP.NET, bao gồm:
- Quản lý source code qua GitHub
- Tổ chức thư mục rõ ràng theo kiến trúc
- Khởi tạo các project cơ bản: API, module và thư viện chia sẻ

---

## 🪜 Các bước thực hiện

---

### 1. ✅ Tạo GitHub repository

Tên repo đề xuất: `escape-modular-monoliths`  
→ Dùng để lưu trữ source code và cộng tác nhóm

---

### 2. ✅ Tạo Solution mới

Tên solution: `Escape.ModularMonolith.sln`  
→ Là container chính chứa toàn bộ các project con

---

### 3. ✅ Tạo cấu trúc thư mục chính

/Escape.ModularMonolith 
├── Bootstrapper/ # Dự án API khởi động hệ thống 
├── Modules/ # Chứa các module theo domain │ 
├── Catalog/ │ 
├── Basket/ │ 
├── Identity/ │ 
└── Ordering/ 
      ├── Shared/ # Các thư viện dùng chung 
      └── Escape.ModularMonolith.sln


---

### 4. ✅ Tạo dự án API chính (Entrypoint)

- **Vị trí**: `Bootstrapper/Escape.API`
- **Loại**: ASP.NET Core Web API
- **Vai trò**:
  - Entrypoint chính của hệ thống
  - Định tuyến đến các module
  - Đăng ký middleware (auth, logging, swagger…)

---

### 5. ✅ Tạo các Module theo Bounded Context

- **Loại**: Class Library (.NET 8)
- **Vị trí**: `Modules/`
- **Tên module**:
  - `Escape.Modules.Catalog`
  - `Escape.Modules.Basket`
  - `Escape.Modules.Identity`
  - `Escape.Modules.Ordering`

> Mỗi module:
> - Có logic domain riêng
> - Sử dụng Vertical Slice Architecture (sẽ setup ở bước sau)

---

### 6. ✅ Tạo thư viện chia sẻ (Shared Libraries)

- **Vị trí**: `Shared/`
- **Vai trò**:
  - Logging
  - Middleware
  - Infrastructure chung
  - Exception, Validation, Utilities...

---

## ✅ Kết quả sau khi hoàn tất

Bạn sẽ có một kiến trúc như sau:

| Thành phần     | Mô tả |
|----------------|------|
| `Bootstrapper` | Dự án API (entrypoint) khởi động toàn hệ thống |
| `Modules`      | Chứa từng module domain độc lập |
| `Shared`       | Các thư viện dùng chung (cross-cutting concerns) |
| `Solution`     | Tập hợp tất cả các project vào cùng một .sln file |

---

## 🧠 Ghi nhớ

- Đặt **tên namespace thống nhất**, ví dụ: `Escape.Modules.Catalog.Product.AddProduct`
- Áp dụng DDD + Vertical Slice ngay từ đầu
- Mỗi module = một Bounded Context
- Không trộn logic giữa các thư mục

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Solution Structure

### 🟢 Cơ bản:
1. Tại sao cần chia solution thành các thư mục như Bootstrapper, Modules và Shared?
2. Vai trò của Bootstrapper là gì trong kiến trúc Modular Monolith?
3. Mỗi module nên tương ứng với điều gì trong Domain-Driven Design?

### 🔵 Trung cấp:
4. Làm sao để tổ chức solution giúp các module phát triển độc lập?
5. Namespace và cấu trúc thư mục nên thiết kế như thế nào cho dễ mở rộng?
6. Nếu một module cần dùng thư viện Shared, bạn sẽ thiết lập phụ thuộc ra sao?

---

