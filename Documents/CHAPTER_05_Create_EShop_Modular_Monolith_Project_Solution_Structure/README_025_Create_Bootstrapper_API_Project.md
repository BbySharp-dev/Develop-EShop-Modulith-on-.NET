# Tạo Bootstrapper API Project – Entrypoint cho Modular Monolith

---

## 🎯 Mục tiêu

Tạo một dự án ASP.NET Core Web API rỗng (Empty Template) trong thư mục `Bootstrapper/`, đóng vai trò làm **entry point** cho toàn bộ ứng dụng Modular Monolith.

---

## 🪜 Các bước thực hiện

---

### 1. Mở Visual Studio → Chọn thư mục `Bootstrapper`

> Lưu ý: thư mục này hiện mới tồn tại **trong Solution**, chưa tồn tại **trên ổ đĩa**.

---

### 2. Tạo project ASP.NET Core Empty

1. Click chuột phải vào thư mục `Bootstrapper` trong Solution
2. Chọn `Add → New Project`
3. Trong cửa sổ chọn template, tìm và chọn **ASP.NET Core Empty**
4. Click **Next**

---

### 3. Cấu hình project

- **Project name**: `API`
- **Location**: trỏ tới đường dẫn: [repo-root]/src/Bootstrapper

> Do thư mục `Bootstrapper` chưa tồn tại vật lý, hãy gõ tên thư mục vào path như sau: [repo-root]/src/Bootstrapper


➡️ Visual Studio sẽ tự tạo thư mục `Bootstrapper` vật lý và đặt project `API` bên trong

---

### 4. Chọn thông số tạo project

- **Framework**: `.NET 8`
- ✅ `Configure for HTTPS`: **Bật**
- ❌ `Enable Docker`: **Tắt**
- Click **Create**

---

### 5. Xác minh kết quả

Cấu trúc thư mục sau khi tạo:

modular-monoliths/ 
└── src/ 
└── Bootstrapper/ 
└── API/ 
└── API.csproj 
└── Program.cs

---

### 6. Chạy thử project

1. Click phải vào project `API` → `Set as Startup Project`
2. Nhấn `Ctrl + F5` (chạy không debug)
3. Trình duyệt mở ra và hiện dòng `"Hello World"` → ✅ thành công

---

## 🔍 Vai trò của project `API`

| Thành phần | Vai trò |
|------------|--------|
| `Bootstrapper/API` | Entry point của toàn bộ hệ thống |
| `Program.cs`       | Cấu hình host, DI, middleware, route |
| Future             | Đăng ký & gọi các module: Catalog, Basket... |

> Đây là nơi tập trung cấu hình toàn bộ hệ thống:  
> - Expose các endpoint từ module  
> - Đăng ký Swagger, Authentication, Exception Handling, Logging, Routing...

---

## 📌 Ghi chú

- Nên sử dụng **template Empty** để tối ưu cho kiến trúc module hóa (Vertical Slice)
- Các thư mục logic `Modules/`, `Shared/` sẽ được thêm sau
- Đây là bước đầu tiên để xây dựng lớp API tập trung

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Entrypoint & Bootstrapper

---

### 🟢 Cơ bản:
1. Dự án `API` trong Bootstrapper có vai trò gì?
2. Vì sao nên chọn ASP.NET Core Empty thay vì Web API template?
3. Tại sao phải tạo thư mục `Bootstrapper` vật lý?

---

### 🔵 Trung cấp:
4. Trong kiến trúc Modular Monolith, các module được "kết nối" vào API như thế nào?
5. Làm sao để đăng ký middleware và DI cho nhiều module trong `Program.cs`?
6. Có thể chạy nhiều `API` project cùng lúc không? Tại sao?

---

### 🔴 Chuyên sâu:
7. Làm sao để tổ chức `Program.cs` thành các extension methods nhằm hỗ trợ module hóa tốt hơn?
8. Nếu bạn cần tạo một API Gateway tách riêng (chạy ngoài monolith), bạn sẽ refactor Bootstrapper như thế nào?
9. Làm sao để tích hợp OpenTelemetry hoặc distributed tracing từ điểm entrypoint (`API`) xuyên suốt qua các module?
10. Trong một hệ thống lớn, bạn sẽ xử lý cấu hình đa môi trường (dev/staging/prod) cho Bootstrapper API ra sao?

---

