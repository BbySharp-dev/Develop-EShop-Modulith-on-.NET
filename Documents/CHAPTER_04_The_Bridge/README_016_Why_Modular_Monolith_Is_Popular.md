# Vì sao Modular Monolith ngày càng phổ biến?

---

## 🔁 Sự chuyển mình của ngành phần mềm

Khi ngành phát triển phần mềm ngày càng hiểu rõ hơn về:
- Sự đơn giản của Monolith
- Sự linh hoạt của Microservices

→ Một hướng đi “trung hòa” ra đời: **Modular Monolith**.

> Modular Monolith không phải là khái niệm mới, nhưng đang **trở lại mạnh mẽ** như một giải pháp **cân bằng giữa tính đơn giản và khả năng mở rộng**.

---

## 🧭 Modular Monolith – Cầu nối giữa hai thế giới

| Kiến trúc | Đặc điểm chính |
|----------|----------------|
| **Monolith** | Đơn giản, dễ bắt đầu, nhưng khó mở rộng |
| **Microservices** | Linh hoạt, mở rộng tốt, nhưng phức tạp về vận hành |
| **Modular Monolith** | Giữ được sự đơn giản khi deploy, nhưng module hóa tốt theo domain |

Mỗi **module** trong Modular Monolith:
- Là một **Bounded Context**
- Tách biệt về logic, data (schema riêng)
- Nhưng vẫn chạy chung tiến trình (không có overhead mạng như Microservices)

---

## ✅ Tóm tắt lý do nên chọn Modular Monolith

| Mục tiêu                             | Modular Monolith cung cấp |
|--------------------------------------|----------------------------|
| Triển khai đơn giản                  | Build & deploy một khối duy nhất |
| Giao tiếp module nhanh               | Dùng method call, không cần HTTP |
| Quản lý dữ liệu đơn giản             | Schema chung, giữ được transactional integrity |
| Phát triển module độc lập            | Mỗi module là một domain riêng biệt |
| Sẵn sàng mở rộng nếu cần             | Có thể tách module thành Microservice khi thích hợp |

---

## 🌟 Ưu điểm nổi bật so với Microservices

### 1. 🧵 Giao tiếp đơn giản, không có latency mạng
- Không cần service discovery, load balancer, message broker
- Mọi thứ chạy trong cùng tiến trình → nhanh và dễ debug

### 2. 🗃️ Quản lý dữ liệu thống nhất
- Sử dụng 1 database chung (hoặc schema riêng theo module)
- Dễ dàng duy trì **ACID transactions**
- Không cần lo eventual consistency hay Saga pattern

### 3. ⚙️ Đơn giản trong phát triển và vận hành
- Không cần orchestrate hàng chục pipeline CI/CD
- Không cần thiết lập hệ thống observability phức tạp
- Dev dễ debug hơn rất nhiều so với hệ thống phân tán

### 4. 📈 Mở rộng linh hoạt
- Có thể scale theo tiến trình
- Có thể tách dần module nào cần scale nhiều hơn sang Microservice
- Dễ dùng load balancer, container, hoặc phân chia logic theo workload

---

## 💬 Kết luận

Modular Monolith không chỉ là một “giải pháp tạm thời”, mà là **một hướng đi bền vững** cho nhiều doanh nghiệp:
- Giúp tiết kiệm chi phí DevOps
- Dễ kiểm soát hệ thống
- Vẫn có khả năng mở rộng trong tương lai

**Triết lý:**
> "Start modular monolith, then extract microservices when (not if) needed."

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Vì sao chọn Modular Monolith

### 🟢 Cơ bản:
1. Modular Monolith là gì và tại sao đang phổ biến trở lại?
2. Lợi ích nào của Monolith vẫn được giữ lại trong Modular Monolith?
3. Việc giao tiếp giữa các module được thực hiện như thế nào?

### 🔵 Trung cấp:
4. So sánh tính đơn giản trong phát triển giữa Modular Monolith và Microservices?
5. Tại sao Modular Monolith dễ đảm bảo toàn vẹn dữ liệu (transaction integrity)?
6. Khi nào bạn nên scale một module trong Modular Monolith?

### 🔴 Chuyên sâu:
7. Làm sao để thiết kế Modular Monolith sao cho dễ chuyển đổi sang Microservices sau này?
8. Làm cách nào để tránh coupling ngầm giữa các module?
9. Nếu có một module tăng trưởng nhanh hơn phần còn lại, bạn sẽ xử lý ra sao trong Modular Monolith?

