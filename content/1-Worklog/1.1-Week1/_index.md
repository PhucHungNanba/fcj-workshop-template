---
title: "1.1. Week 1 Worklog"
weight: 11
draft: false
---

# 1.1. Week 1: Khởi tạo Môi trường & Phân tích Kiến trúc

### Week 1 Objectives:

* Phân tích kiến trúc hệ thống EDMS (Enterprise Document Management System) theo mô hình Serverless trên AWS.
* Thiết lập tài khoản AWS an toàn tuân thủ tiêu chuẩn bảo mật doanh nghiệp.
* Chuẩn bị và đồng bộ hóa môi trường phát triển cục bộ (Local Development) cho toàn bộ nhóm.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 | - Phân tích kiến trúc Serverless v2<br>- Đánh giá các dịch vụ AWS: Cognito, S3, Lambda, API Gateway<br>- Thống nhất sử dụng Aurora Serverless v2 (MySQL) và DynamoDB | 22/06/2026 | 22/06/2026 | Tài liệu kiến trúc EDMS |
| 2 | - Khởi tạo tài khoản AWS chung<br>- Thiết lập bảo mật Root user (MFA)<br>- Tạo IAM User riêng biệt cho các thành viên<br>- Cấu hình Billing Alarm ($5/tháng) | 23/06/2026 | 23/06/2026 | AWS IAM & Billing Documentation |
| 3 | - Cài đặt môi trường lập trình: JDK 17 (Amazon Corretto), Maven 3.8+, AWS SAM CLI<br>- Cấu hình AWS CLI với Access Key cá nhân | 24/06/2026 | 24/06/2026 | AWS SAM CLI Setup Guide |
| 4 | - Khởi tạo GitHub repository và phân quyền<br>- Thiết lập các branch tiêu chuẩn (main, develop)<br>- Phân tích và chuẩn bị luồng xác thực OIDC cho GitHub Actions | 25/06/2026 | 25/06/2026 | GitHub Actions OIDC Trust Policy |
| 5 | - Báo cáo tiến độ tuần 1<br>- Lên kế hoạch chi tiết cho việc thiết kế Database ở tuần tiếp theo | 26/06/2026 | 26/06/2026 | EDMS-Master-Checklist |

---

### Chi tiết thực hiện

**1. Phân tích kiến trúc và rà soát công nghệ (Tech Stack Review)**
Hệ thống được thiết kế theo hướng polyglot persistence nhằm tối ưu hóa chi phí và hiệu năng. Kiến trúc sử dụng Aurora Serverless v2 để quản lý dữ liệu quan hệ phức tạp và DynamoDB chuyên biệt cho việc lưu vết hệ thống (AuditLog). Các dịch vụ vệ tinh bao gồm Cognito cho xác thực và S3 cho lưu trữ vật lý.

**2. Thiết lập tài nguyên và Bảo mật hạ tầng AWS**
Áp dụng nguyên tắc quyền đặc quyền tối thiểu (Least Privilege). Tài khoản Root được bảo vệ nghiêm ngặt bằng Multi-Factor Authentication (MFA). Các thành viên trong nhóm thao tác hoàn toàn thông qua IAM User độc lập. Cơ chế kiểm soát chi phí được kích hoạt thông qua AWS CloudWatch Billing Alarm.

**3. Khởi tạo môi trường phát triển (Local Development Setup)**
Đảm bảo tính đồng nhất trong môi trường phát triển của toàn đội bằng việc chuẩn hóa các phiên bản công cụ lõi: Java 17, Maven và AWS Serverless Application Model (SAM) CLI. 

**4. Quản lý mã nguồn và luồng CI/CD cơ bản**
Mã nguồn được quản lý tập trung trên GitHub. Kế hoạch triển khai CI/CD (Continuous Integration / Continuous Deployment) được định hình dựa trên giao thức OIDC (OpenID Connect), loại bỏ hoàn toàn rủi ro lộ lọt thông tin khi không cần lưu trữ static AWS keys.

---

### Khó khăn & Giải pháp

* **Khó khăn:** Quản lý chi phí cho cụm cơ sở dữ liệu Aurora Serverless v2, do dịch vụ này không tự động scale về mức 0 ACU khi hệ thống ở trạng thái nhàn rỗi (idle).
* **Giải pháp:** Thiết lập quy trình vận hành nội bộ nghiêm ngặt. Hệ thống cluster phải được chủ động dừng (stop) hoặc tự động hóa việc dọn dẹp thông qua AWS CLI sau mỗi phiên làm việc nhằm tối ưu hóa chi phí dự án.