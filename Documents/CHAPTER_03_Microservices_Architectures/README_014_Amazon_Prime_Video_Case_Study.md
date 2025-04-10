# Case Study – Amazon Prime Video: Từ Microservices sang Monolithic để tối ưu chi phí & hiệu năng

---

## 🎬 Bối cảnh

Amazon Prime Video cần giám sát hàng ngàn luồng video & âm thanh **trực tiếp (live)** cho người dùng toàn cầu.  
Yêu cầu hệ thống:
- Giám sát chất lượng âm thanh/hình ảnh theo thời gian thực
- Đảm bảo khả năng mở rộng khi số luồng tăng nhanh
- Chi phí hạ tầng phải tối ưu ở quy mô lớn

---

## ❌ Vấn đề với kiến trúc Microservices ban đầu

Hệ thống ban đầu sử dụng kiến trúc **distributed microservices**, bao gồm 3 thành phần chính:
- **Media Converter**: chuyển đổi video thành frame
- **Defect Detector**: phát hiện lỗi hình ảnh/âm thanh
- **Orchestration**: quản lý luồng xử lý qua AWS Step Functions

### ⚠️ Các vấn đề phát sinh:

| Vấn đề                        | Mô tả |
|-------------------------------|-------|
| **Chi phí quá cao**           | Sử dụng nhiều state transition + lưu trữ tạm thời trên Amazon S3 |
| **Giới hạn scale AWS Step Function** | Chuyển trạng thái liên tục → nhanh chóng chạm ngưỡng giới hạn |
| **Độ trễ cao**                | Do chia nhỏ các bước xử lý, mỗi bước lưu/đọc tạm qua S3 |
| **Quản lý phức tạp**          | Khó debug và giám sát toàn bộ flow giữa các service |

---

## ✅ Giải pháp: Chuyển sang kiến trúc Monolithic

### Kiến trúc mới:

- **Tất cả các thành phần (convert, detect, orchestrate)** được gói gọn trong **một process duy nhất**
- Triển khai trên 1 **Amazon ECS Task**
- **Không dùng S3 tạm thời** ở mỗi bước → chỉ lưu kết quả cuối
- **Chia phiên bản theo luồng/khách hàng** để xử lý song song

### 📈 Tối ưu đạt được:

| Kết quả                       | Chi tiết |
|-------------------------------|----------|
| **Giảm chi phí hạ tầng 90%+** | Không dùng intermediate S3 + tối ưu resource theo task |
| **Tăng khả năng mở rộng**     | Dễ clone ECS task theo nhu cầu |
| **Đơn giản hóa orchestration**| Không còn state transitions phức tạp |
| **Giảm độ trễ toàn hệ thống** | Xử lý trong cùng bộ nhớ (in-memory), không I/O tạm thời |

---

## 🔍 So sánh trước – sau

| Tiêu chí         | Microservices (cũ)              | Monolith (mới)                 |
|------------------|----------------------------------|--------------------------------|
| Xử lý video/audio| Phân tán nhiều service           | Tập trung trong 1 tiến trình   |
| Lưu trữ trung gian | Amazon S3 (nhiều lần đọc/ghi)  | Chỉ ghi kết quả cuối cùng      |
| Orchestration    | AWS Step Functions              | Tự quản lý trong 1 ECS Task    |
| Chi phí          | Rất cao                         | Giảm hơn 90%                   |
| Scale            | Horizontal (service)            | Clone ECS tasks (vertical + horizontal) |

---

## 💡 Bài học rút ra

- Microservices **không phải lúc nào cũng tốt hơn** – nếu dùng sai sẽ gây phức tạp & tốn chi phí
- **Đánh giá kỹ use case** trước khi chọn kiến trúc
- Monolith có thể hiệu quả hơn trong các hệ thống:
  - Có logic tightly coupled
  - Yêu cầu xử lý nhanh, thời gian thực
  - Không cần scale độc lập từng phần
- Việc **loại bỏ orchestration & lưu trữ trung gian** giúp đơn giản hóa và tiết kiệm rất nhiều

---

## 🎯 Bộ câu hỏi phỏng vấn – Chủ đề: Amazon Prime Video & Kiến trúc

### 🟢 Cơ bản:
1. Amazon Prime Video đã gặp vấn đề gì với kiến trúc microservices ban đầu?
2. Việc lưu trữ tạm trên S3 gây ảnh hưởng gì đến hiệu suất và chi phí?
3. Monolithic architecture giúp giảm chi phí bằng cách nào?

### 🔵 Trung cấp:
4. Tại sao việc dùng AWS Step Functions gây giới hạn scale?
5. Làm sao Amazon đảm bảo khả năng mở rộng khi dùng kiến trúc Monolith?
6. Vì sao việc xử lý in-memory lại hiệu quả hơn lưu/đọc qua S3?

### 🔴 Chuyên sâu:
7. Bạn có áp dụng mô hình monolith trong container như Amazon không? Cách quản lý resource?
8. Nếu refactor hệ thống microservices cũ thành monolith như case Amazon, bạn cần cân nhắc điều gì?
9. Làm sao để xác định một hệ thống đang bị “over-microserviced” và cần gom lại?

