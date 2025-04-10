# Những vấn đề với kiến trúc Monolithic truyền thống

---

## ❓ Monolithic dễ hiểu – vậy vấn đề nằm ở đâu?

Mặc dù Monolith có vẻ đơn giản để khởi đầu, nhưng khi ứng dụng phát triển và yêu cầu mở rộng, nó sẽ bộc lộ nhiều **vấn đề nghiêm trọng về hiệu suất, tổ chức và khả năng triển khai**.

---

## 🧱 Các vấn đề lớn thường gặp

---

### 🚧 1. Khó mở rộng (Scalability Limitations)

| Vấn đề | Mô tả |
|--------|------|
| **Không thể scale riêng từng phần** | Vì cả ứng dụng là 1 khối, nên không thể scale riêng authentication hay payment – phải scale toàn bộ. |
| **Tốn tài nguyên không cần thiết** | Dẫn đến sử dụng CPU/RAM quá mức, gây lãng phí tài nguyên |
| **Tăng chi phí vận hành** | Mỗi lần mở rộng cần tăng toàn bộ hệ thống, không tối ưu hóa được |
| **Không linh hoạt** | Nếu chỉ 1 chức năng có traffic lớn (ví dụ: login), bạn vẫn phải scale toàn hệ thống |

---

### 🐌 2. Tắc nghẽn phát triển (Development Bottlenecks)

| Vấn đề | Mô tả |
|--------|------|
| **Codebase phức tạp và cồng kềnh** | Càng thêm tính năng → code càng rối và khó hiểu |
| **Khó bảo trì** | Một thay đổi nhỏ có thể ảnh hưởng đến các phần không liên quan |
| **Nhiều developer cùng sửa 1 chỗ** | Dễ gây conflict, lỗi logic, khó debug |
| **Tăng chi phí và thời gian phát triển** | Feature nhỏ cũng có thể mất nhiều ngày vì ảnh hưởng các phần khác |

---

### 🔗 3. Tightly Coupled – Kết nối chặt chẽ giữa các thành phần

- Các component không độc lập → sửa 1 chỗ dễ “vỡ dây chuyền”
- Làm tăng độ rủi ro khi refactor
- Rất khó viết test hoặc CI/CD khi mọi thứ gắn chặt vào nhau

---

### 💣 4. Rủi ro khi triển khai (Deployment Risk)

| Rủi ro | Hệ quả |
|--------|--------|
| **Single Point of Failure** | Nếu deploy lỗi → cả hệ thống sập |
| **Không thể rollback riêng lẻ** | Phải rollback toàn bộ ứng dụng nếu gặp sự cố |
| **Downtime thường xuyên** | Triển khai cần downtime, ảnh hưởng đến người dùng |
| **Bug nhỏ → sập toàn hệ thống** | Không có cơ chế tách biệt lỗi theo module |

---

## 📌 Tổng kết

> Monolith có thể hiệu quả cho dự án nhỏ, nhưng không phù hợp cho hệ thống lớn, yêu cầu mở rộng linh hoạt.

### ❌ Khi nào **Monolith là rào cản**:
- Ứng dụng có tốc độ tăng trưởng nhanh
- Cần thêm tính năng liên tục
- Có nhiều nhóm dev làm song song
- Yêu cầu uptime cao, tránh downtime

### ✅ Khi nào **nên chuyển sang Modular/Microservices**:
- Khi muốn scale từng phần riêng lẻ
- Khi muốn giảm rủi ro triển khai
- Khi hệ thống đã quá phức tạp để duy trì

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Vấn đề với Monolith

### 🟢 Cơ bản:
1. Tại sao kiến trúc Monolith khó mở rộng trong môi trường nhiều traffic?
2. Tightly coupled nghĩa là gì? Tại sao nó gây hại trong Monolith?
3. Một thay đổi nhỏ trong Monolith có thể gây ra điều gì?

### 🔵 Trung cấp:
4. Vì sao codebase của Monolith dễ trở nên cồng kềnh?
5. So sánh chi phí vận hành giữa Monolith và hệ thống chia module?
6. Vì sao Monolith thường yêu cầu downtime khi triển khai?

### 🔴 Chuyên sâu:
7. Làm thế nào để triển khai rollback an toàn trong Monolith?
8. Đâu là rào cản lớn nhất khi tách Monolith thành Modular/Microservices?
9. Nếu bạn bắt buộc dùng Monolith cho 1 hệ thống lớn, bạn sẽ thiết kế sao cho dễ tách về sau?

