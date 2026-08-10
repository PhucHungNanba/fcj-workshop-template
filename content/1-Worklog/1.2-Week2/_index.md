---
title: "1.2. Week 2 Worklog"
weight: 12
draft: false
---

# 1.2. Week 2: Thiết kế Cơ sở dữ liệu & Phân tích Nghiệp vụ

### Week 2 Objectives:

* Phân tích chi tiết các thực thể nghiệp vụ (Entities) của hệ thống EDMS.
* Thiết kế lược đồ cơ sở dữ liệu (Database Schema) áp dụng kiến trúc Polyglot Persistence (Aurora Serverless v2 và DynamoDB).
* Hoàn thiện kịch bản kiểm thử biên dịch cục bộ (Local Build) với Maven cho các module backend Java 17.

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

**1. Phân tích Thực thể Nghiệp vụ (Business Entities)**
Hệ thống EDMS quản lý các thực thể cốt lõi bao gồm: Users (Người dùng), Documents (Tài liệu gốc), DocumentVersions (Phiên bản nội dung), Permissions (Quyền truy cập), Tags (Nhãn phân loại), Files (Tệp vật lý đính kèm), OCRResults (Kết quả trích xuất văn bản) và AuditLogs (Nhật ký truy vết). Dựa trên phân tích này, hệ thống áp dụng mô hình phân quyền (RBAC) để kiểm soát quyền Owner, Editor và Viewer.

**2. Thiết kế Cơ sở dữ liệu đa mô hình (Polyglot Persistence)**
Thay vì sử dụng một loại database duy nhất, kiến trúc v2 được thiết kế kết hợp:
* **Aurora Serverless v2 (MySQL):** Quản lý các dữ liệu có quan hệ phức tạp (Foreign Keys) như Document, Version, Permission, Tag. Cấu trúc được chuẩn hoá 3NF để đảm bảo tính toàn vẹn dữ liệu.
* **Amazon DynamoDB:** Quản lý AuditLog, chuyên xử lý các tác vụ ghi liên tục (write-heavy) và không cần JOIN.

**3. Thiết kế bảng AuditLog trên DynamoDB**
Bảng AuditLogs được cấu hình để truy xuất lịch sử thao tác (ví dụ: UPLOAD, VIEW, DOWNLOAD, APPROVE) theo từng tài liệu. Cấu trúc khóa được thiết kế với Partition Key (PK) là `DOC#<documentId>` và Sort Key (SK) là `LOG#<timestamp>`. Đồng thời, thuộc tính `ttl` (Time-To-Live) được định nghĩa bổ sung để hệ thống tự động xóa các log quá hạn nhằm tiết kiệm dung lượng lưu trữ.

**4. Chuẩn bị công cụ Build Local**
Vì dự án bao gồm 9 Lambda function độc lập được phát triển bằng Java 17, các kịch bản biên dịch đã được thiết lập thông qua Maven. Lệnh `mvn -q clean package` được chạy vòng lặp cho từng thư mục module để đóng gói fat-jar bằng `maven-shade-plugin`, giúp phát hiện lỗi compile sớm trước khi đẩy mã nguồn lên Cloud.

---

### Khó khăn & Giải pháp

* **Khó khăn:** Việc lưu trữ khối lượng lớn nhật ký truy vết (AuditLog) vào cơ sở dữ liệu quan hệ Aurora MySQL có thể làm giảm hiệu năng hệ thống khi bảng phình to và làm tăng đáng kể chi phí lưu trữ.
* **Giải pháp:** Tách hoàn toàn tính năng lưu AuditLog sang DynamoDB (NoSQL) với thiết kế append-only. Việc truy vấn chỉ thực hiện dựa trên `documentId` để xem lịch sử truy cập, kết hợp TTL (tự động dọn rác), giúp giải quyết triệt để bài toán thắt cổ chai hiệu năng của hệ cơ sở dữ liệu chính.