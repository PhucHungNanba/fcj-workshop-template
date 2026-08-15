---
title: "Tuần 6"
date: 2026-08-02
weight: 16
chapter: false
---

# Tuần 6: Tự động hóa Luồng công việc, SNS & AWS SAM

### Mục tiêu

* Tự động hóa các luồng công việc phê duyệt tài liệu sử dụng AWS Step Functions.
* Tích hợp Amazon SNS để tự động hóa thông báo qua email và quản lý vòng đời tài liệu.
* Đóng gói và triển khai toàn bộ backend Serverless bằng cách sử dụng Cơ sở hạ tầng dưới dạng mã (Infrastructure as Code - AWS SAM).

---

### Các công việc đã hoàn thành

| Ngày | Chi tiết công việc | Ngày tháng |
| :---: | :--- | :---: |
| **1** | **Luồng công việc Phê duyệt (Step Functions)**<br>- Xây dựng một Máy trạng thái (State Machine - `approval.asl.json`) trên AWS Step Functions để điều phối quy trình phê duyệt tài liệu. | 27/07/2026 |
| **2** | **Thông báo Sự kiện (Amazon SNS)**<br>- Tích hợp Amazon SNS để kích hoạt các cảnh báo email tự động khi phê duyệt thành công hoặc có tài liệu mới được chia sẻ. | 28/07/2026 |
| **3** | **Chia sẻ Tài liệu An toàn**<br>- Lập trình tính năng chia sẻ có kiểm soát, tạo các Pre-signed URLs có giới hạn thời gian để cho phép truy cập từ bên ngoài/nội bộ. | 29/07/2026 |
| **4** | **Vòng đời tài liệu: Xóa tạm thời (Soft Delete)**<br>- Triển khai cơ chế Xóa tạm thời (Soft Delete), chuyển tài liệu sang trạng thái TRASH (Thùng rác) với khoảng thời gian cho phép khôi phục là 30 ngày. | 30/07/2026 |
| **5** | **Vòng đời tài liệu: Tự động hóa Xóa vĩnh viễn (Hard Delete)**<br>- Cấu hình các thuộc tính `ttl` của DynamoDB để tự động xóa vĩnh viễn các tài liệu hết hạn mà không cần can thiệp thủ công. | 31/07/2026 |
| **6** | **Cơ sở hạ tầng dưới dạng mã (IaC)**<br>- Soạn thảo tệp `template.yaml` bằng AWS SAM để định nghĩa tất cả các hàm Lambda, các endpoint của API Gateway và các bảng DynamoDB. | 01/08/2026 |
| **7** | **Triển khai Đám mây (Cloud Deployment)**<br>- Thực thi các lệnh `sam build` và `sam deploy` để cấp phát (provision) toàn bộ kiến trúc EDMS lên môi trường AWS Cloud. | 02/08/2026 |

---

### Kết quả đạt được

* **Logic Nghiệp vụ Tự động hóa:** Điều phối thành công các luồng công việc doanh nghiệp phức tạp mà không cần viết các đoạn code lồng nhau rườm rà. AWS Step Functions xử lý việc phê duyệt, trong khi SNS đảm bảo người dùng được thông báo ngay lập tức.
* **Triển khai Tối ưu:** Thay thế các cấu hình thủ công trên AWS Console bằng AWS SAM. Giờ đây, toàn bộ dự án có thể được khởi tạo (spun up) hoặc gỡ bỏ (torn down) chỉ trong vài phút bằng code, giúp giảm đáng kể gánh nặng vận hành và quản lý tài nguyên.