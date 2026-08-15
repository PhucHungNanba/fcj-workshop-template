---
title: "Tuần 7"
date: 2026-08-09
weight: 17
chapter: false
---

# Tuần 7: Tự động hóa CI/CD, Bảo mật & Tích hợp AI

### Mục tiêu

* Thiết lập luồng CI/CD tự động hoàn toàn sử dụng GitHub Actions và xác thực OIDC không cần khóa (keyless).
* Triển khai các lớp bảo mật nâng cao (AWS WAF, Secrets Manager) và rà soát các chính sách IAM.
* Tích hợp khả năng OCR thông qua EventBridge để trích xuất văn bản tài liệu một cách bất đồng bộ (asynchronous).

---

### Các công việc đã hoàn thành

| Ngày | Chi tiết công việc | Ngày tháng |
| :---: | :--- | :---: |
| **1** | **Thiết lập Xác thực OIDC**<br>- Cấu hình một IAM Role với chính sách tin cậy (trust policy) cho phép GitHub Actions xác thực an toàn qua OIDC, loại bỏ việc sử dụng các khóa tĩnh (static AWS Keys). | 03/08/2026 |
| **2** | **Luồng CI/CD (GitHub Actions)**<br>- Soạn thảo workflow `deploy.yml` để tự động chạy unit tests và triển khai hạ tầng khi có mã nguồn mới được hợp nhất (merge). | 04/08/2026 |
| **3** | **Bảo mật Cơ sở dữ liệu (Secrets Manager)**<br>- Tích hợp AWS Secrets Manager để lưu trữ an toàn và tự động xoay vòng (auto-rotate) thông tin đăng nhập của cơ sở dữ liệu Aurora. | 05/08/2026 |
| **4** | **Bảo vệ biên (AWS WAF)**<br>- Cấu hình tường lửa ứng dụng web AWS (WAF) để chặn các spam bots và thực thi giới hạn tỷ lệ (rate-limiting) tại vùng mạng biên. | 06/08/2026 |
| **5** | **Rà soát Đặc quyền tối thiểu IAM**<br>- Phối hợp với cộng sự Nguyễn Như Vương để kiểm toán toàn bộ các Chính sách AWS IAM, đảm bảo nguyên tắc Quyền hạn tối thiểu (Least Privilege) được thực thi nghiêm ngặt. | 07/08/2026 |
| **6** | **Trích xuất dữ liệu AI (OCR)**<br>- Tích hợp các công cụ OCR để tự động trích xuất văn bản thô từ các hình ảnh và file PDF được tải lên, sau đó lưu vào thực thể `OCRResults`. | 08/08/2026 |
| **7** | **Xử lý Sự kiện Bất đồng bộ**<br>- Cấu hình S3 Events và Amazon EventBridge để kích hoạt các tác vụ OCR nặng một cách bất đồng bộ dưới nền, ngăn chặn tình trạng quá giờ (timeouts) của API. | 09/08/2026 |

---

### Kết quả đạt được

* **Triển khai Không cần khóa & Bảo mật Doanh nghiệp:** Đạt được một môi trường triển khai bảo mật cao sử dụng OIDC. Thông tin đăng nhập cơ sở dữ liệu được tự động xoay vòng và hệ thống được bảo vệ khỏi lưu lượng truy cập độc hại bởi AWS WAF.
* **Tự động hóa AI Hiệu suất cao:** Tách biệt thành công quá trình trích xuất AI nặng nề khỏi luồng tải lên của người dùng. Kiến trúc hướng sự kiện (event-driven architecture) đảm bảo người dùng không gặp phải độ trễ (zero lag) trong quá trình OCR chạy bất đồng bộ dưới nền.