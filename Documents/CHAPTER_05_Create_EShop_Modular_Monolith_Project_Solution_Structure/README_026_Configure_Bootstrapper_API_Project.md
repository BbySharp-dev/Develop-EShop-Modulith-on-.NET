# Cấu hình dự án API để trở thành Bootstrapper cho Modular Monolith

---

## 🎯 Mục tiêu

Cấu hình lại ASP.NET Core Empty Project để trở thành **Bootstrapper API**, đóng vai trò entrypoint chính cho toàn bộ hệ thống Modular Monolith.

Gồm 3 bước:

1. Cấu hình `Program.cs`
2. Tùy chỉnh `launchSettings.json`
3. Kiểm tra và chạy thử API

---

## 🪜 Bước 1: Cấu hình lại `Program.cs`

### ✅ Mục tiêu:
- Định nghĩa rõ ràng 2 pha:
  - Trước khi build: cấu hình DI, logging, middleware
  - Sau khi build: cấu hình HTTP request pipeline

### 📄 Ví dụ `Program.cs` cơ bản:

```csharp
var builder = WebApplication.CreateBuilder(args);

// --- Before build: cấu hình services ---
builder.Services.AddControllers(); // sẽ mở rộng sau
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// --- After build: cấu hình HTTP pipeline ---
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

- Cấu trúc này giúp dễ dàng mở rộng để đăng ký các module và service injection theo từng module sau này.

## 🪜 Bước 2: Cập nhật launchSettings.json
### ✅ Vị trí:
Bootstrapper/API/Properties/launchSettings.json

### ✅ Mục tiêu:
- Cấu hình cổng mặc định cho môi trường dev
- Tắt tự động mở trình duyệt khi chạy project

### 📄 Gợi ý nội dung launchSettings.json:
```json
{
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": false,
      "applicationUrl": "http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "https": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": false,
      "applicationUrl": "https://localhost:5050",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```
- Sau này khi triển khai với Docker Compose, bạn có thể dùng port 6060, 6061, v.v. cho môi trường production.

## 🪜 Bước 3: Chạy và xác minh API
1. Click phải vào project API → Set as Startup Project
2. Chọn chạy profile HTTPS (port 5050)
3. Nhấn Ctrl + F5 để chạy thử

### ✅ Nếu cấu hình đúng:
- Trình duyệt không mở (vì "launchBrowser": false)
- Terminal báo đang chạy tại https://localhost:5050
- Có thể truy cập thủ công bằng Postman hoặc trình duyệt

## 📌 Kết quả đạt được
### ✅ Cấu trúc thư mục đúng chuẩn
modular-monoliths/
└── src/
    └── Bootstrapper/
        └── API/
            ├── API.csproj
            ├── Program.cs
            └── Properties/
                └── launchSettings.json

### ✅ API hoạt động đúng ở chế độ phát triển
- Chạy tại https://localhost:5050
- Không mở trình duyệt khi chạy (launchBrowser: false)
- Sẵn sàng test qua Postman
### ✅ Program.cs có cấu trúc rõ ràng, chuẩn mở rộng
- Phân tách rõ ràng trước và sau builder.Build()
- Có thể mở rộng đăng ký module, middleware, service
### ✅ launchSettings.json được cấu hình đúng
- Cổng cố định cho dev: 5000 / 5050
- Môi trường: Development
- Sẵn sàng chuyển sang Docker Compose sau này
### ✅ Tóm lại: bạn đã cấu hình xong API khởi đầu, sẵn sàng tích hợp các module vào hệ thống Modular Monolith.

## 🎯 Bộ câu hỏi phỏng vấn – Cấu hình Bootstrapper API
### 🟢 Cơ bản:
1. Tại sao cần chia cấu hình trước và sau builder.Build()?
2. Tác dụng của "launchBrowser": false trong launchSettings.json?
3. Vì sao nên chọn port cố định như 5050?

### 🔵 Trung cấp:
1. Làm sao để mở rộng Program.cs cho phép đăng ký module động?
2. Nếu dùng nhiều profile chạy cùng lúc, bạn quản lý như thế nào?
3. Tại sao nên dùng Empty template thay vì Web API?

### 🔴 Chuyên sâu:
1. Làm sao tổ chức Program.cs theo mô hình extension methods để dễ bảo trì?
2. Làm sao chuyển cấu hình từ launchSettings.json sang môi trường Docker Compose?
3. Làm sao để trace request từ API qua các module khi triển khai distributed tracing?