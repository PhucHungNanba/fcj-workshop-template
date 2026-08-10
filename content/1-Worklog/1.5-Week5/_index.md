---
title: "Week 5: EDMS Project - Backend Logic & API Gateway"
date: 2026-08-11
weight: 15
chapter: false
---

# Week 5: EDMS Project - Backend Logic & API Gateway
*Tuần 5: Dự án EDMS - Xử lý logic Backend và API Gateway*

### Objectives | Mục tiêu tuần 5

* Develop core document management APIs (CRUD) using Java 17 and AWS Lambda.
  *Phát triển các API quản lý tài liệu cốt lõi (CRUD) bằng Java 17 và AWS Lambda.*
* Implement Versioning Control, Role-Based Access Control (RBAC), and optimize performance.
  *Triển khai kiểm soát phiên bản, phân quyền truy cập (RBAC) và tối ưu hóa hiệu năng.*

---

### Tasks Completed | Công việc đã thực hiện

| Day | Task Details | Date |
| :---: | :--- | :---: |
| **1** | **Core API Development**<br>- Programmed Lambda functions (`document_crud`, `list_documents`) using Java 17 (Amazon Corretto) to handle document creation and retrieval.<br><br>*Phát triển API Cốt lõi*<br>*- Lập trình các hàm Lambda bằng Java 17 (Amazon Corretto) để xử lý việc tạo và truy xuất tài liệu.* | 30/06/2025 |
| **2** | **Code Optimization (Lambda Layers)**<br>- Extracted shared libraries and utilities from 9 independent Lambda functions into AWS Lambda Layers to reduce deployment package size.<br><br>*Tối ưu Mã nguồn (Lambda Layers)*<br>*- Trích xuất các thư viện và mã dùng chung từ 9 hàm Lambda độc lập thành AWS Lambda Layers để giảm kích thước gói triển khai.* | 01/07/2025 |
| **3** | **Versioning Control & Rollback**<br>- Implemented version control logic to automatically generate a new `versionNumber` upon edits.<br>- Built a Rollback feature that restores previous versions while locking historical data in Read-only mode.<br><br>*Quản lý Phiên bản & Khôi phục*<br>*- Triển khai logic kiểm soát phiên bản, tự động sinh số phiên bản mới khi có chỉnh sửa.*<br>*- Xây dựng tính năng Rollback giúp khôi phục bản cũ và khóa dữ liệu lịch sử ở chế độ Chỉ xem.* | 02/07/2025 |
| **4** | **Role-Based Access Control (RBAC)**<br>- Finalized the Permissions module to enforce strict access boundaries for Owners, Editors, and Viewers at the API level.<br><br>*Phân quyền Truy cập (RBAC)*<br>*- Hoàn thiện module Phân quyền để thiết lập ranh giới truy cập nghiêm ngặt cho Chủ sở hữu, Người chỉnh sửa và Người xem ngay tại tầng API.* | 03/07/2025 |
| **5** | **Cold Start Mitigation (SnapStart)**<br>- Resolved Java 17 cold start delays (1-3s) by enabling AWS Lambda SnapStart, taking pre-initialized JVM snapshots to accelerate response times.<br><br>*Khắc phục Khởi động lạnh (SnapStart)*<br>*- Giải quyết tình trạng khởi động chậm của Java 17 (1-3s) bằng cách bật AWS Lambda SnapStart, chụp sẵn bộ nhớ JVM để tăng tốc độ phản hồi.* | 04/07/2025 |

---

### Results Achieved | Kết quả đạt được

* **Robust Backend Logic:** Successfully deployed a fully functional, secure, and version-controlled backend API capable of handling complex document workflows.
  *Logic Backend Vững chắc: Triển khai thành công API backend đầy đủ chức năng, bảo mật và có khả năng kiểm soát phiên bản để xử lý các luồng tài liệu phức tạp.*

* **High-Performance Execution:** Dramatically improved API response times and user experience by leveraging Lambda Layers for efficient code management and SnapStart for instant execution.
  *Thực thi Hiệu năng cao: Cải thiện đáng kể thời gian phản hồi API và trải nghiệm người dùng nhờ tận dụng Lambda Layers để quản lý mã hiệu quả và SnapStart để thực thi tức thì.*