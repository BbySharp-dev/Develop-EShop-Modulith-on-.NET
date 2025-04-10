# Microservices Architecture – Kiến trúc dịch vụ nhỏ độc lập

---

## 🧩 Microservices là gì?

**Microservices** là phương pháp thiết kế phần mềm, trong đó ứng dụng được chia thành **nhiều dịch vụ nhỏ (services)**, hoạt động độc lập và giao tiếp với nhau qua mạng.

### ✅ Đặc điểm chính:
- Mỗi **service là một ứng dụng nhỏ**, có codebase riêng, data riêng
- Do **nhóm nhỏ** phát triển, bảo trì độc lập
- **Giao tiếp qua API**, thường là HTTP REST, gRPC, hoặc message broker
- Dễ triển khai, mở rộng, đổi mới – không ảnh hưởng hệ thống tổng thể
- **Công nghệ độc lập**: mỗi service có thể dùng ngôn ngữ, framework, database khác nhau

---

## 🔍 Microservices Architecture là gì?

Theo định nghĩa từ [Martin Fowler](https://martinfowler.com/articles/microservices.html):

> Microservices Architecture là một phong cách thiết kế trong đó một ứng dụng được phát triển dưới dạng **tập hợp các dịch vụ nhỏ, mỗi dịch vụ chạy riêng biệt**, giao tiếp qua các giao thức nhẹ như HTTP/gRPC, được tổ chức xoay quanh **năng lực nghiệp vụ**, và có thể được **triển khai độc lập** qua các quy trình CI/CD tự động.

---

## 🧱 Kiến trúc tổng thể của Microservices

| Thành phần           | Mô tả |
|----------------------|------|
| **Service độc lập**  | Mỗi service đại diện cho một năng lực nghiệp vụ (business capability) cụ thể |
| **Cơ sở dữ liệu riêng** | Mỗi service có database riêng – không chia sẻ (Database per service) |
| **Giao tiếp qua API** | REST, gRPC, Message Queue |
| **Triển khai riêng biệt** | Có thể cập nhật, rollback từng service |
| **Team sở hữu riêng biệt** | Mỗi team chịu trách nhiệm từ A-Z cho một service (dev, deploy, monitor...) |

---

## ☁️ Microservices & Cloud-native

Microservices là xương sống của **kiến trúc cloud-native** hiện đại:
- Mỗi service là 1 unit độc lập, dễ scale, dễ failover
- Tích hợp dễ dàng với các hệ thống CI/CD và container (Docker, Kubernetes)
- Phù hợp cho phát triển phân tán toàn cầu

---

## 🔄 Giao tiếp giữa các service

| Cách giao tiếp          | Khi nào dùng |
|-------------------------|-------------|
| **REST API**            | Giao tiếp đồng bộ, dữ liệu cần phản hồi tức thời |
| **gRPC**                | Nhanh hơn REST, dùng trong nội bộ hoặc yêu cầu cao về hiệu năng |
| **Message Broker**      | Giao tiếp bất đồng bộ (Pub/Sub), decoupling service (RabbitMQ, Kafka) |
| **Event Streaming**     | Dùng khi có volume lớn, cần xử lý real-time |

---

## 🧭 Khái niệm “Bounded Context”

- Mỗi microservice thường tương ứng với một **bounded context** trong Domain-Driven Design
- Giới hạn ranh giới nghiệp vụ và dữ liệu riêng biệt
- Không chia sẻ entity, DTO giữa các service → tránh coupling

---

## ✅ Lợi ích của Microservices

| Lợi ích                         | Mô tả |
|----------------------------------|-------|
| **Triển khai độc lập**          | Triển khai, rollback từng service mà không ảnh hưởng hệ thống |
| **Tăng tốc độ phát triển**      | Nhóm nhỏ, chịu trách nhiệm riêng biệt, dễ làm song song |
| **Dễ scale**                    | Scale theo từng service → tiết kiệm tài nguyên |
| **Đa dạng công nghệ**           | Service A dùng .NET, service B dùng NodeJS, MongoDB, PostgreSQL… |
| **Thân thiện với DevOps**       | Dễ áp dụng CI/CD, auto scaling, logging, monitoring độc lập |
| **Thúc đẩy tư duy phân rã nghiệp vụ** | Áp dụng rõ ràng mô hình Bounded Context |

---

## 📌 Tổng kết

Microservices Architecture là giải pháp mạnh mẽ, hiện đại để phát triển các hệ thống lớn – tuy nhiên **không phù hợp với mọi dự án** (phần này sẽ được nói trong README tiếp theo).

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Microservices Architecture

### 🟢 Cơ bản:
1. Microservices là gì? Khác gì với Monolith?
2. Một microservice có thể giao tiếp với các service khác như thế nào?
3. Mỗi service trong microservices có dùng chung database không?

### 🔵 Trung cấp:
4. Lợi ích của việc triển khai độc lập trong microservices là gì?
5. Bounded Context là gì? Liên hệ với microservice thế nào?
6. Làm sao để mỗi nhóm dev có thể tự chịu trách nhiệm cho service của mình?

### 🔴 Chuyên sâu:
7. Bạn sẽ thiết kế 1 hệ thống Microservices như thế nào cho hệ thống e-commerce?
8. Làm sao để duy trì tính nhất quán dữ liệu giữa các service?
9. So sánh khi nào nên dùng REST, khi nào nên dùng event-based communication?

