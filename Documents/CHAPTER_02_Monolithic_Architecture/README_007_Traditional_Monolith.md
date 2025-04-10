# Monolithic Architecture – Kiến trúc nguyên khối truyền thống

---

## 🧱 Monolithic Architecture là gì?

Monolithic Architecture (kiến trúc nguyên khối) là kiểu thiết kế ứng dụng truyền thống, trong đó **toàn bộ các thành phần của ứng dụng – từ giao diện, logic xử lý, đến truy cập dữ liệu – đều được đóng gói trong một khối mã duy nhất** và được triển khai cùng nhau.

### ✅ Ví dụ:
- Một ứng dụng web ASP.NET MVC cổ điển, nơi toàn bộ Controller, Service, Repository cùng nằm chung trong một project duy nhất, deploy dưới dạng 1 file `.dll` hoặc `.exe`.

---

## 🔎 Đặc điểm chính của Monolith

| Đặc điểm               | Mô tả |
|------------------------|------|
| **Single Codebase**    | Toàn bộ mã nguồn nằm trong một codebase duy nhất. Dễ quản lý lúc đầu, nhưng càng phát triển càng phức tạp. |
| **Single Deployment**  | Toàn bộ ứng dụng được đóng gói và deploy như một đơn vị duy nhất. |
| **Tightly Coupled**    | Các thành phần phụ thuộc lẫn nhau chặt chẽ – thay đổi một phần có thể ảnh hưởng cả hệ thống. |
| **Shared Database**    | Tất cả các phần của ứng dụng dùng chung một cơ sở dữ liệu – gây khó khi cần tách biệt dữ liệu hoặc mở rộng module riêng lẻ. |

---

## ✅ Ưu điểm của Monolith

- **Dễ khởi đầu**: Phù hợp với nhóm nhỏ, timeline gấp.
- **Đơn giản trong triển khai**: Một lần build, một lần deploy.
- **Không cần xử lý giao tiếp mạng hoặc các vấn đề phân tán**.
- **Tính nhất quán dữ liệu cao**: Vì toàn bộ chạy trong cùng một tiến trình và cùng database.

---

## ⚠️ Hạn chế & vấn đề thường gặp

| Vấn đề | Hệ quả |
|--------|--------|
| **Khó mở rộng riêng lẻ** | Muốn scale một tính năng → phải scale cả hệ thống |
| **Khó bảo trì khi phức tạp** | Codebase lớn dễ rối, dễ gây lỗi khi thêm mới tính năng |
| **Mỗi lần deploy là cả hệ thống** | Chỉ thay đổi một dòng code cũng phải build + deploy toàn bộ |
| **Giới hạn trong phát triển song song** | Nhiều dev cùng sửa 1 codebase dễ gây conflict |

---

## 📌 Khi nào nên dùng Monolith?

Dù mang tính "truyền thống", monolith **không lỗi thời** nếu:
- Dự án nhỏ, MVP, PoC, startup mới cần ra sản phẩm nhanh.
- Đội phát triển nhỏ, ít người.
- Không cần khả năng mở rộng cao trong giai đoạn đầu.
- Yêu cầu **tính nhất quán dữ liệu cực cao**, ví dụ hệ thống ngân hàng nội bộ, hệ thống chấm công nội bộ.

---

## 🚧 Vì sao Monolith bị thay thế?

Khi hệ thống lớn dần:
- Mỗi thay đổi nhỏ gây build + deploy cả hệ thống
- Tính năng khó mở rộng riêng biệt
- Đội phát triển không thể làm việc song song hiệu quả
- Mọi thứ đều gắn vào nhau như “spaghetti code”

Do đó, các kiến trúc **Modular Monolith** và **Microservices** ra đời để giải quyết các vấn đề này.

---

## 🧠 Tổng kết

> Monolith là khởi đầu – nhưng không phải là kết thúc.

- Hiểu Monolith giúp bạn trân trọng sự đơn giản, nhưng cũng nhận diện được giới hạn của nó.
- Rất nhiều hệ thống thành công bắt đầu từ monolith → rồi **dần dần tách thành module** hoặc microservice (dùng Strangler Pattern).
- Không phải công nghệ nào cũng “lỗi thời”, vấn đề là dùng đúng lúc, đúng chỗ.

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Monolithic Architecture

### 🟢 Cơ bản:
1. Kiến trúc Monolithic là gì? Có những đặc điểm gì?
2. Vì sao Monolith được coi là đơn giản để bắt đầu?
3. Các thành phần nào thường nằm trong một Monolithic App?

### 🔵 Trung cấp:
4. Những thách thức lớn nhất khi duy trì hệ thống Monolith lớn là gì?
5. Tại sao shared database trong Monolith là một điểm yếu khi mở rộng?
6. So sánh Monolith và Modular Monolith về khả năng bảo trì.

### 🔴 Chuyên sâu:
7. Khi nào bạn vẫn nên chọn Monolith thay vì Modular/Microservices?
8. Làm sao để tách dần Monolith sang kiến trúc module mà không ảnh hưởng người dùng?
9. Bạn sẽ thiết kế một chiến lược rollback hiệu quả cho ứng dụng Monolith như thế nào?
