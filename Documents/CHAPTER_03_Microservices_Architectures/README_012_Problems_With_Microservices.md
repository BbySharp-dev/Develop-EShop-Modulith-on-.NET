# Những thách thức và mặt trái của Microservices Architecture

---

## 🚨 Microservices không dành cho mọi hệ thống

Dù Microservices mang lại nhiều lợi ích (triển khai độc lập, công nghệ linh hoạt...), nhưng cũng đi kèm với **sự phức tạp gia tăng**, cả về kỹ thuật lẫn vận hành.

---

## ⚙️ 1. Hệ thống phân tán = Phức tạp

| Vấn đề                          | Mô tả |
|----------------------------------|-------|
| **Tăng số lượng dịch vụ**        | Mỗi service nhỏ hơn, nhưng tổng hệ thống lại phức tạp hơn Monolith |
| **Triển khai riêng biệt**        | Mỗi service cần cấu hình CI/CD, build, versioning riêng |
| **Quản lý logs, monitor, metrics** | Dữ liệu phân tán khắp nơi, khó tổng hợp & phân tích |

---

## 🌐 2. Vấn đề về mạng (Network Complexity)

| Rủi ro                           | Giải pháp đi kèm |
|----------------------------------|------------------|
| **Latency tăng**                 | Cần tối ưu số hop giữa services |
| **Mất kết nối (network failure)**| Retry, Timeout, Fallback (Circuit Breaker) |
| **Protocol phức tạp**            | REST/gRPC/MessageQueue → cần chọn đúng |
| **Service Discovery**            | Phải cấu hình với tools như Consul, Eureka, hoặc Kubernetes DNS |

---

## 💾 3. Quản lý dữ liệu phức tạp

| Vấn đề                          | Hệ quả |
|----------------------------------|--------|
| **Không còn giao dịch ACID truyền thống** | Khó đảm bảo tính nhất quán xuyên services |
| **Cần Eventual Consistency**    | Dùng Saga Pattern, Outbox, Event Sourcing... |
| **Trùng lặp dữ liệu (data duplication)** | Tăng chi phí lưu trữ, cần sync qua event |
| **Phức tạp hóa logic nghiệp vụ** | Mỗi service phải biết khi nào publish/subscribe dữ liệu nào |

---

## 🔧 4. Chi phí vận hành & DevOps

- Mỗi service = 1 đơn vị deploy riêng → CI/CD phải nhân lên nhiều lần
- Cần đầu tư mạnh vào:
  - **Automation pipelines**
  - **Containerization (Docker)**
  - **Orchestration (Kubernetes, Docker Swarm)**
  - **Service mesh (Istio, Linkerd)**

> ⚠️ DevOps là yếu tố then chốt nếu muốn triển khai Microservices thành công

---

## 🐞 5. Testing & Debugging phức tạp

| Thách thức                      | Mô tả |
|----------------------------------|-------|
| **End-to-end testing khó**       | Yêu cầu phối hợp nhiều service, phức tạp hơn nhiều so với Monolith |
| **Integration test chậm & nặng**| Cần môi trường staging gần giống production |
| **Debug khó xuyên service**     | Không thể debug local như monolith |
| **Cần Distributed Tracing**     | Sử dụng Zipkin, Jaeger, OpenTelemetry để trace theo flow request |

---

## 🔁 6. Quản lý giao tiếp giữa service

- Giao tiếp = hợp đồng → cần quản lý version, backward compatibility
- Call chồng call (service A → B → C → D) → dễ gây **latency chain**
- Cần thiết kế API kỹ, tránh coupling ngầm
- Để giảm call chain → dùng **event-driven architecture**

---

## 🧯 7. Fault Tolerance (Chống lỗi toàn hệ thống)

- Nếu 1 service sập → dễ ảnh hưởng chuỗi các service còn lại
- Cần:
  - Circuit Breaker (Polly, Hystrix, Resilience4J)
  - Retry with backoff
  - Graceful Fallback

---

## 📌 Tổng kết

| Lợi ích Microservices            | Cái giá phải trả                        |
|----------------------------------|-----------------------------------------|
| Triển khai độc lập               | Nhiều pipeline, nhiều tool quản lý      |
| Công nghệ linh hoạt              | Giao tiếp phải đồng bộ                  |
| Scale theo từng phần             | Phải quản lý network, resource per service |
| Đội dev tự chủ                   | Cần người dẫn kỹ thuật có kiến thức kiến trúc, DevOps |

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Thách thức của Microservices

### 🟢 Cơ bản:
1. Tại sao Microservices được gọi là hệ thống phân tán?
2. Vì sao testing microservices phức tạp hơn monolith?
3. Eventual consistency là gì? Tại sao nó cần thiết?

### 🔵 Trung cấp:
4. Bạn sẽ dùng công cụ gì để trace lỗi trong microservices?
5. So sánh Circuit Breaker và Retry logic?
6. Làm sao bạn đảm bảo dữ liệu đồng bộ giữa các service độc lập?

### 🔴 Chuyên sâu:
7. Mô hình CI/CD nào phù hợp để triển khai 50+ microservices?
8. Thiết kế API gateway và service discovery trong kiến trúc microservices ra sao?
9. Nếu một yêu cầu cần gọi 5 service liên tiếp, bạn sẽ tối ưu hiệu suất thế nào?

