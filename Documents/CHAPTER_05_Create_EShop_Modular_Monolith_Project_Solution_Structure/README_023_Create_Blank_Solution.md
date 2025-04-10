# Tạo blank solution cho dự án Modular Monolith

---

## 🎯 Mục tiêu

Tạo một solution trống (`.sln`) dưới thư mục `src/` trong repository GitHub đã clone, làm nền tảng để thêm các project về sau (API, Modules, Shared...).

---

## 🪜 Các bước thực hiện

---

### 1. Mở Visual Studio

- Truy cập thư mục dự án GitHub đã clone về máy
- Mở thư mục `src/` trong Visual Studio

---

### 2. Tạo blank solution mới

1. **File → New → Project**
2. Chọn template **"Blank Solution"**
3. Bấm **Next**

---

### 3. Đặt tên solution

- **Solution name**: `Shop.ModularMonoliths`
- **Location**: trỏ vào thư mục `src` trong repository GitHub (ví dụ: `modular-monoliths/src`)
- Bấm **Create**

---

### 4. Cấu trúc thư mục sau khi tạo (ban đầu)

Khi tạo bằng Visual Studio, sẽ tạo thêm 1 thư mục trùng tên solution:

modular-monoliths/ 
└── src/ 
└── Shop.ModularMonoliths/ 
└── Shop.ModularMonoliths.sln

→ Không đúng vị trí mong muốn.

---

### 5. Cấu hình lại thư mục cho đúng

Thực hiện điều chỉnh lại vị trí file `.sln`:

1. Mở thư mục `src/Shop.ModularMonoliths/`
2. Cắt file `Shop.ModularMonoliths.sln`
3. Dán trực tiếp vào `src/`
4. Xoá thư mục rỗng `Shop.ModularMonoliths/`

✅ Sau thao tác, cấu trúc sẽ đúng như sau:

modular-monoliths/ 
└── src/ 
└── Shop.ModularMonoliths.sln

---

### 6. Kiểm tra lại trong Visual Studio

- Mở lại file `.sln` từ `src/`
- Vào **Solution Explorer** → `Right click → Open Folder in File Explorer`
- Xác minh rằng `.sln` đã được đặt đúng tại `src/`
- Mở **Git Changes** tab để kiểm tra trạng thái file `.sln` trong repo

---

## 📁 Kết quả

modular-monoliths/ 
├── .gitignore 
├── LICENSE 
├── README.md 
└── src/ 
    └── Shop.ModularMonoliths.sln

---

## 📌 Ghi chú

- Đặt file `.sln` trực tiếp trong `src/` giúp quản lý source code rõ ràng, tránh thư mục lồng nhau dư thừa
- Đây là bước chuẩn bị quan trọng trước khi tạo các project API và module
- Sau bước này, bạn đã sẵn sàng để bắt đầu cấu trúc các **folder chính: `Bootstrapper`, `Modules`, `Shared`**

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Solution & cấu trúc thư mục

### 🟢 Cơ bản:
1. Blank solution là gì và vai trò của nó trong dự án .NET?
2. Vì sao không nên để solution nằm trong thư mục con trùng tên?
3. Tại sao nên đặt `.sln` trong thư mục `src/`?

### 🔵 Trung cấp:
4. Nếu bạn clone repo và solution không nằm đúng vị trí, bạn xử lý ra sao?
5. Khi tạo thêm project (API, Module), bạn sẽ tổ chức ra sao dưới solution?

