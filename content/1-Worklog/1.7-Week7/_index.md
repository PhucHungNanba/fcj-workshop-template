---
title: "Week 7: CI/CD Automation, Security & AI Integration"
date: 2026-08-11
weight: 17
chapter: false
---

# Week 7: CI/CD Automation, Security & AI Integration
*Tuần 7: Tự động hóa CI/CD, Bảo mật & Tích hợp AI (OCR)*

### Objectives | Mục tiêu tuần 7

* Establish a fully automated CI/CD pipeline using GitHub Actions and keyless OIDC authentication.
  *Thiết lập luồng triển khai CI/CD tự động hóa hoàn toàn bằng GitHub Actions và xác thực OIDC không dùng key.*
* Implement advanced security layers (AWS WAF, Secrets Manager) and review IAM policies.
  *Triển khai các lớp bảo mật nâng cao (AWS WAF, Secrets Manager) và rà soát chính sách phân quyền IAM.*
* Integrate OCR capabilities via EventBridge for asynchronous document text extraction.
  *Tích hợp khả năng OCR thông qua EventBridge để trích xuất văn bản tài liệu một cách bất đồng bộ.*

---

### Tasks Completed | Công việc đã thực hiện

| Day | Task Details | Date |
| :---: | :--- | :---: |
| **1** | **OIDC Authentication Setup**<br>- Configured an IAM Role with a trust policy allowing GitHub Actions to authenticate securely via OIDC, eliminating static AWS Keys.<br><br>*Thiết lập Xác thực OIDC*<br>*- Cấu hình IAM Role với policy cho phép GitHub Actions xác thực an toàn qua OIDC, loại bỏ hoàn toàn việc dùng Key AWS tĩnh.* | 03/08/2026 |
| **2** | **CI/CD Pipeline (GitHub Actions)**<br>- Authored the `deploy.yml` workflow to automatically run unit tests and deploy infrastructure upon new code merges.<br><br>*Luồng CI/CD (GitHub Actions)*<br>*- Viết workflow `deploy.yml` để tự động chạy kiểm thử và triển khai hạ tầng khi có mã nguồn mới được hợp nhất.* | 04/08/2026 |
| **3** | **Database Security (Secrets Manager)**<br>- Integrated AWS Secrets Manager to securely store and auto-rotate the Aurora database credentials.<br><br>*Bảo mật CSDL (Secrets Manager)*<br>*- Tích hợp AWS Secrets Manager để lưu trữ an toàn và tự động xoay vòng mật khẩu của cơ sở dữ liệu Aurora.* | 05/08/2026 |
| **4** | **Edge Protection (AWS WAF)**<br>- Configured AWS Web Application Firewall (WAF) to block spam bots and enforce rate-limiting at the network edge.<br><br>*Bảo vệ Tầng biên (AWS WAF)*<br>*- Cấu hình tường lửa AWS WAF để chặn các bot spam và áp dụng giới hạn tần suất gọi API ngay tại biên mạng.* | 06/08/2026 |
| **5** | **IAM Least Privilege Review**<br>- Collaborated with group partner Nguyễn Như Vương to audit all AWS IAM Policies, ensuring the Least Privilege principle is strictly enforced.<br><br>*Rà soát Quyền Tối thiểu IAM*<br>*- Phối hợp cùng cộng sự Nguyễn Như Vương rà soát toàn bộ AWS IAM Policies, đảm bảo nguyên tắc Quyền tối thiểu được áp dụng triệt để.* | 07/08/2026 |
| **6** | **AI Data Extraction (OCR)**<br>- Integrated OCR tools to automatically extract raw text from uploaded images and PDFs, saving it to the `OCRResults` entity.<br><br>*Trích xuất Dữ liệu AI (OCR)*<br>*- Tích hợp công cụ OCR tự động trích xuất văn bản thô từ hình ảnh và PDF tải lên, lưu vào thực thể `OCRResults`.* | 08/08/2026 |
| **7** | **Asynchronous Event Processing**<br>- Configured S3 Events and Amazon EventBridge to trigger the heavy OCR tasks asynchronously in the background, preventing API timeouts.<br><br>*Xử lý Sự kiện Bất đồng bộ*<br>*- Cấu hình S3 Events và Amazon EventBridge để kích hoạt tiến trình OCR nặng chạy ngầm, ngăn chặn lỗi quá thời gian chờ (timeout) của API.* | 09/08/2026 |

---

### Results Achieved | Kết quả đạt được

* **Zero-Key Deployment & Enterprise Security:** Achieved a highly secure deployment environment using OIDC. Database credentials are auto-rotated, and the system is shielded from malicious traffic by AWS WAF.
  *Triển khai Không Key & Bảo mật Doanh nghiệp: Đạt được môi trường triển khai bảo mật cao bằng OIDC. Mật khẩu CSDL được tự động xoay vòng và hệ thống được bảo vệ khỏi lưu lượng độc hại bởi AWS WAF.*

* **High-Performance AI Automation:** Successfully decoupled the heavy AI extraction process from the user upload flow. The event-driven architecture ensures users experience zero lag while the OCR runs asynchronously.
  *Tự động hóa AI Hiệu suất cao: Phân tách thành công tiến trình trích xuất AI nặng nề khỏi luồng tải file của người dùng. Kiến trúc hướng sự kiện đảm bảo người dùng không gặp độ trễ trong khi OCR chạy ngầm.*