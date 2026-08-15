---
title: "Tuần 8"
weight: 18
chapter: false
---

# Tuần 8: Kiểm thử, Khả năng quan sát & Tối ưu hóa chi phí

### Mục tiêu

* Đảm bảo chất lượng mã nguồn thông qua Kiểm thử đơn vị (Unit Tests) và Kiểm thử tích hợp (Integration Tests) trên môi trường thực tế.
* Giám sát và phân tích hiệu suất hệ thống phân tán sử dụng AWS X-Ray và Amazon CloudWatch.
* Hoàn tất bàn giao dự án, hoàn thiện tài liệu và dọn dẹp tài nguyên để tối ưu chi phí về mức 0$.

---

### Các công việc đã hoàn thành

| Ngày | Chi tiết công việc | Ngày tháng |
| :---: | :--- | :---: |
| **1** | **Kiểm thử đơn vị (Unit Testing)**<br>- Viết các bài kiểm thử đơn vị cho các module backend Java 17 sử dụng framework JUnit 5 và Mockito. | 10/08/2026 |
| **2** | **Kiểm thử tích hợp (Integration Testing - E2E)**<br>- Thực thi các kịch bản kiểm thử tích hợp đầu cuối (end-to-end) bằng Bash trên môi trường Dev đã triển khai thực tế. | 11/08/2026 |
| **3** | **Theo dõi phân tán (Distributed Tracing)**<br>- Tích hợp AWS X-Ray để theo dõi các truy vấn từ API Gateway qua Lambda đến Cơ sở dữ liệu. | 12/08/2026 |
| **4** | **Giám sát hệ thống (CloudWatch)**<br>- Rà soát nhật ký hệ thống (system logs) trên Amazon CloudWatch và phân tích nguyên nhân gốc rễ của độ trễ Cold Start trên Lambda. | 13/08/2026 |
| **5** | **Tài liệu & Báo cáo**<br>- Tổng hợp báo cáo thực tập cuối kỳ và viết tài liệu cho toàn bộ kiến trúc Serverless EDMS. | 14/08/2026 |
| **6** | **Demo cuối kỳ & Bàn giao**<br>- Tiến hành buổi thuyết trình dự án (demo) cuối kỳ, trình bày các luồng công việc tự động và tính năng tích hợp AI cho các mentor. | 15/08/2026 |
| **7** | **Dọn dẹp tài nguyên (Tear Down)**<br>- Thực thi các lệnh dọn dẹp để xóa S3 Buckets, Cognito User Pools và stack SAM, giảm thành công chi phí duy trì AWS về 0$. | 16/08/2026 |

---

### Kết quả đạt được

* **Độ tin cậy & Khả năng quan sát của hệ thống:** Đảm bảo hệ thống hoạt động hoàn hảo thông qua quá trình kiểm thử nhiều cấp độ nghiêm ngặt. Việc tích hợp AWS X-Ray và CloudWatch cung cấp khả năng quan sát toàn diện vào kiến trúc phân tán, giúp việc gỡ lỗi (debugging) trở nên cực kỳ hiệu quả.
* **Làm chủ việc Tối ưu Chi phí:** Thể hiện thành công kỹ năng quản lý chi phí đám mây. Bằng cách gỡ bỏ (tearing down) có hệ thống toàn bộ các tài nguyên đã cấp phát sau buổi demo, dự án đảm bảo không phát sinh bất kỳ khoản phí ngoài ý muốn nào trong tương lai.

---

### Thách thức & Giải pháp

* **Thách thức:** Quá trình Kiểm thử Tích hợp đôi khi bị lỗi do các hàm Java Lambda mất quá nhiều thời gian để khởi động (Cold Start), dẫn đến tình trạng hết thời gian chờ (timeouts) trên API Gateway.
* **Giải pháp:** Áp dụng kỹ thuật làm nóng ("Warm Up"). Trước khi chạy các kịch bản e2e tự động hoặc bắt đầu buổi demo trực tiếp, tất cả các hàm đều được gọi (invoked) một lần để khởi tạo trước JVM, đảm bảo các yêu cầu tiếp theo được xử lý trơn tru với độ trễ tối thiểu.