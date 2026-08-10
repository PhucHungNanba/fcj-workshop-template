---
title: "Week 4: EDMS Project - Database & Storage Setup"
date: 2026-08-11
weight: 14
chapter: false
---

# Week 4: EDMS Project - Database & Storage Setup
*Tuần 4: Dự án EDMS - Thiết lập Cơ sở dữ liệu và Lưu trữ*

### Objectives | Mục tiêu tuần 4

* Design and implement a Polyglot Persistence database architecture using Amazon Aurora and DynamoDB.
  *Thiết kế và triển khai kiến trúc cơ sở dữ liệu đa mô hình (Polyglot Persistence) sử dụng Amazon Aurora và DynamoDB.*
* Configure secure object storage for physical files and set up centralized user authentication.
  *Cấu hình kho lưu trữ đối tượng an toàn cho tệp vật lý và thiết lập hệ thống xác thực người dùng tập trung.*

---

### Tasks Completed | Công việc đã thực hiện

| Day | Task Details | Date |
| :---: | :--- | :---: |
| **1** | **Database Schema Design**<br>- Designed the Polyglot Persistence schema: Aurora Serverless v2 (MySQL) for relational data (Documents, Versions, Tags) and DynamoDB for AuditLogs.<br><br>*Thiết kế Lược đồ CSDL*<br>*- Thiết kế lược đồ đa mô hình: Aurora Serverless v2 (MySQL) cho dữ liệu quan hệ (Tài liệu, Phiên bản, Nhãn) và DynamoDB cho Nhật ký hệ thống (AuditLogs).* | 23/06/2025 |
| **2** | **DynamoDB & TTL Configuration**<br>- Configured the DynamoDB AuditLogs table with Partition Key (`DOC#<documentId>`) and Sort Key (`LOG#<timestamp>`).<br>- Enabled Time-To-Live (TTL) to automatically delete expired logs and save costs.<br><br>*Cấu hình DynamoDB & TTL*<br>*- Cấu hình bảng AuditLogs trên DynamoDB với Khóa phân vùng và Khóa sắp xếp.*<br>*- Bật tính năng Time-To-Live (TTL) để tự động xóa log cũ nhằm tiết kiệm chi phí.* | 24/06/2025 |
| **3** | **Identity Management with Cognito**<br>- Integrated Amazon Cognito User Pool to handle login and password verification.<br>- Created user groups (e.g., HR, SALES) to support enterprise-level role-based access control.<br><br>*Quản lý Danh tính với Cognito*<br>*- Tích hợp Amazon Cognito User Pool để xử lý đăng nhập và xác thực mật khẩu.*<br>*- Tạo các nhóm người dùng (VD: HR, SALES) để hỗ trợ phân quyền cấp doanh nghiệp.* | 25/06/2025 |
| **4** | **Secure Storage with S3 Presigned URLs**<br>- Set up an Amazon S3 bucket for physical file storage.<br>- Engineered a secure upload mechanism using Presigned URLs with a strict 5-10 minute expiration window to prevent bandwidth abuse.<br><br>*Lưu trữ Bảo mật với S3 Presigned URLs*<br>*- Thiết lập bucket Amazon S3 để lưu trữ tệp vật lý.*<br>*- Xây dựng cơ chế tải lên an toàn bằng Presigned URLs với thời gian sống ngắn (5-10 phút) để tránh lạm dụng băng thông.* | 26/06/2025 |

---

### Results Achieved | Kết quả đạt được

* **Scalable Database Architecture:** Successfully decoupled the write-heavy AuditLog stream to DynamoDB, fully resolving potential performance bottlenecks on the main Aurora relational database.
  *Kiến trúc CSDL Mở rộng: Tách biệt thành công luồng ghi log mật độ cao sang DynamoDB, giải quyết triệt để bài toán thắt cổ chai hiệu năng trên hệ cơ sở dữ liệu quan hệ Aurora chính.*

* **Enterprise-Grade Security:** Established a robust security perimeter by combining Cognito for identity management and short-lived S3 Presigned URLs for direct, credential-free file uploads.
  *Bảo mật Cấp Doanh nghiệp: Thiết lập vành đai bảo mật vững chắc nhờ kết hợp Cognito để quản lý danh tính và S3 Presigned URLs có thời hạn ngắn để tải file trực tiếp mà không lộ thông tin xác thực.*