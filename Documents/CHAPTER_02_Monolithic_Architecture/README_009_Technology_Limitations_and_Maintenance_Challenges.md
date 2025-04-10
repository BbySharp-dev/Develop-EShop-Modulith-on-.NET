# Hạn chế công nghệ và thách thức bảo trì trong kiến trúc Monolith

---

## 🚫 Giới hạn trong việc đổi mới công nghệ

### 🔒 Bị khóa chặt bởi công nghệ ban đầu
- Trong kiến trúc Monolithic, các thành phần **liên kết chặt chẽ** với nhau.
- Việc thay đổi framework, ngôn ngữ lập trình, hoặc thư viện ở một phần nhỏ thường đòi hỏi **viết lại cả hệ thống**.

### 💥 Ví dụ thực tế:
> Bạn muốn chuyển sang MongoDB cho module “Feedback”, nhưng ứng dụng đang dùng PostgreSQL duy nhất → Không thể chỉ thay đổi 1 phần mà không ảnh hưởng toàn bộ.

---

## 🔄 Chu kỳ sợ hãi (The Fear Cycle)

| Triệu chứng | Hệ quả |
|-------------|--------|
| Ứng dụng tồn tại lâu năm | Rất khó thay đổi công nghệ, vì mỗi thay đổi ảnh hưởng toàn hệ thống |
| Quá phụ thuộc vào công nghệ cũ | Không dám cập nhật .NET version mới, vì sợ “vỡ” các phần liên quan |
| Sợ refactor | Tốn thời gian test toàn diện, dễ sinh bug không mong muốn |

> 👉 Kết quả: **Thay vì đổi mới**, team sẽ “vá lỗi” – dẫn đến trì trệ, mất lợi thế cạnh tranh

---

## 🧨 Khó đáp ứng yêu cầu nghiệp vụ mới

- Monolith khiến việc phản ứng với thay đổi của thị trường chậm hơn.
- Mỗi thay đổi lớn → phải test toàn hệ thống → delay release.
- **Không linh hoạt** để phát triển tính năng theo hướng module độc lập.

---

## 🛠️ Thách thức bảo trì lâu dài

### 1. Technical Debt (Nợ kỹ thuật)
- Code cũ, lạc hậu
- Thiếu tài liệu
- “Sửa nhanh cho kịp deadline” → làm giảm chất lượng hệ thống

### 2. Fix bug = sợ bug mới
- Sửa lỗi dễ tạo ra lỗi mới ở phần không liên quan
- Đòi hỏi test regression thường xuyên và toàn diện
- Feature đơn giản → chi phí duy trì cao

### 3. Quản lý đội ngũ phát triển
- Nhiều developer cùng sửa 1 codebase → dễ gây xung đột (conflict)
- Merge phức tạp, mất thời gian
- Code review trở nên nặng nề

> 👉 Làm giảm hiệu suất phát triển, mất tinh thần team, tốn kém tài nguyên dài hạn

---

## 📌 Tổng kết

| Hạn chế | Hệ quả |
|--------|--------|
| Khó đổi mới công nghệ | Không thể tận dụng công cụ mới, mất tính cạnh tranh |
| Nợ kỹ thuật tích lũy | Ảnh hưởng tốc độ phát triển |
| Khó bảo trì, fix bug | Tăng chi phí kiểm thử, vận hành |
| Team khó phối hợp | Mất thời gian, dễ xung đột |

> Monolith không chỉ giới hạn ở mặt kỹ thuật – nó còn ảnh hưởng đến **con người, tiến độ và chất lượng sản phẩm**.

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Hạn chế công nghệ & Bảo trì trong Monolith

### 🟢 Cơ bản:
1. Tại sao Monolith khó thay đổi framework hoặc ngôn ngữ?
2. Fear Cycle trong phát triển phần mềm là gì?
3. Vì sao một thay đổi nhỏ trong Monolith lại cần test toàn bộ?

### 🔵 Trung cấp:
4. Technical Debt là gì? Nó thường xuất hiện như thế nào trong hệ thống Monolithic?
5. Việc refactor trong Monolith có thể gây ra những rủi ro gì?
6. Vì sao đội phát triển lớn dễ gặp xung đột khi làm việc với Monolith?

### 🔴 Chuyên sâu:
7. Bạn sẽ xử lý việc chuyển dần công nghệ trong Monolith ra sao mà vẫn an toàn?
8. Làm thế nào để giảm thiểu technical debt trong hệ thống Monolith cũ?
9. Bạn có cách nào để tổ chức teamwork hiệu quả hơn khi phải làm việc trên một Monolithic codebase?

