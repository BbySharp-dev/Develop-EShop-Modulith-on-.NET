# Tạo thư mục Solution cho các Modules theo Bounded Context (DDD)

---

## 🎯 Mục tiêu

Tạo các thư mục solution con trong `Modules/`, mỗi thư mục đại diện cho **một Bounded Context** theo phân tích Domain-Driven Design.

---

## 📌 Các module cần tạo

Dựa theo phân tích nghiệp vụ, chúng ta có 4 **Bounded Context** chính, tương ứng với 4 modules:

| Module     | Mô tả |
|------------|------|
| `Catalog`  | Quản lý sản phẩm, danh mục, giá |
| `Basket`   | Giỏ hàng, tính tổng, chỉnh sửa item |
| `Ordering` | Tạo và xử lý đơn hàng |
| `Identity` | Xác thực và phân quyền người dùng |

---

## 🪜 Các bước thực hiện trong Visual Studio

### 1. Mở Visual Studio → Solution Explorer

### 2. Tìm đến thư mục `Modules/` trong Solution

### 3. Lần lượt tạo các thư mục con cho mỗi module:

- Click phải vào `Modules/` → `Add → New Solution Folder`
- Nhập tên:
  - `Catalog`
  - `Basket`
  - `Ordering`
  - `Identity` (nếu chưa tạo)

Sau khi hoàn tất, bạn sẽ có cấu trúc như sau:

Shop.ModularMonoliths.sln 
└── Modules/ 
├── Catalog/ 
├── Basket/ 
├── Ordering/ 
└── Identity/


---

## 🔍 Mỗi module là một Bounded Context

- Tách biệt về **logic**, **dữ liệu**, **API**
- Phát triển độc lập, test độc lập
- Có thể áp dụng kiến trúc nội bộ khác nhau (tùy mức độ phức tạp)
- Sau này dễ dàng tách thành Microservices nếu cần

---

## 🧱 Chuẩn bị cho kiến trúc nội bộ của từng module

| Module     | Kiến trúc đề xuất                         |
|------------|-------------------------------------------|
| `Catalog`  | Vertical Slice + DDD + EF Core            |
| `Basket`   | Vertical Slice + Caching (Redis) + Events |
| `Ordering` | Vertical Slice + Outbox Pattern           |
| `Identity` | Giao tiếp với Keycloak (REST/OIDC)        |

Chúng ta sẽ lần lượt khởi tạo các **class library project** bên trong các thư mục này để chứa mã nguồn cho từng module.

---

## 📌 Ghi chú

- Mỗi thư mục **Solution Folder** ở bước này **chỉ tạo trong solution** – **chưa tạo thư mục vật lý**
- Khi thêm project vào từng folder (Catalog, Basket...), Visual Studio sẽ tạo thư mục vật lý tương ứng

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Modules theo Bounded Context

### 🟢 Cơ bản:
1. Mỗi module trong kiến trúc Modular Monolith nên tương ứng với điều gì trong DDD?
2. Tại sao cần tách các module thành solution folder độc lập?
3. Các module có thể giao tiếp với nhau bằng cách nào?

### 🔵 Trung cấp:
4. Làm sao tổ chức folder và namespace trong mỗi module cho rõ ràng, dễ bảo trì?
5. Vì sao Catalog module nên dùng Vertical Slice thay vì MVC truyền thống?
6. Khi nào một module nên áp dụng Outbox Pattern?

### 🔴 Chuyên sâu:
7. Làm sao kiểm soát được dependencies giữa các module để không tạo ra "distributed monolith nội bộ"?
8. Nếu 2 module cần dùng chung dữ liệu, bạn xử lý thế nào để không phá vỡ Bounded Context?
9. Làm sao để thiết kế hệ thống test tự động cho từng module độc lập mà vẫn đảm bảo tích hợp chung?

