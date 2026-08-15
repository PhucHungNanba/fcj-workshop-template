---
title: "Tuần 5"
date: 2026-07-26
weight: 15
chapter: false
---

# Tuần 5: Dự án EDMS - Logic Backend & API Gateway

### Mục tiêu

* Phát triển các API quản lý tài liệu cốt lõi (CRUD) sử dụng Java 17 và AWS Lambda.
* Triển khai Kiểm soát phiên bản (Versioning Control), Kiểm soát truy cập dựa trên vai trò (RBAC) và tối ưu hóa hiệu suất.

---

### Các công việc đã hoàn thành

| Ngày | Chi tiết công việc | Ngày tháng |
| :---: | :--- | :---: |
| **1** | **Phát triển API Cốt lõi**<br>- Lập trình các hàm Lambda (`document_crud`, `list_documents`) bằng Java 17 (Amazon Corretto) để xử lý việc tạo mới và truy xuất tài liệu. | 20/07/2026 |
| **2** | **Tối ưu hóa Code (Lambda Layers)**<br>- Tách các thư viện và tiện ích dùng chung từ 9 hàm Lambda độc lập đưa vào AWS Lambda Layers để giảm kích thước gói triển khai. | 21/07/2026 |
| **3** | **Kiểm soát Phiên bản & Khôi phục (Rollback)**<br>- Triển khai logic kiểm soát phiên bản để tự động tạo `versionNumber` mới khi có chỉnh sửa.<br>- Xây dựng tính năng Rollback giúp khôi phục các phiên bản trước đó, đồng thời khóa dữ liệu lịch sử ở chế độ Chỉ đọc (Read-only). | 22/07/2026 |
| **4** | **Kiểm soát Truy cập dựa trên Vai trò (RBAC)**<br>- Hoàn thiện module Phân quyền để áp đặt ranh giới truy cập nghiêm ngặt cho Người sở hữu (Owners), Người chỉnh sửa (Editors) và Người xem (Viewers) ở cấp độ API. | 23/07/2026 |
| **5** | **Khắc phục độ trễ khởi động (Cold Start Mitigation)**<br>- Giải quyết độ trễ cold start của Java 17 (1-3s) bằng cách kích hoạt AWS Lambda SnapStart, sử dụng các bản chụp (snapshots) JVM đã khởi tạo sẵn để tăng tốc độ phản hồi. | 24/07/2026 |

---

### Kết quả đạt được

* **Logic Backend Mạnh mẽ:** Triển khai thành công một backend API đầy đủ chức năng, bảo mật và được kiểm soát phiên bản, có khả năng xử lý các luồng công việc tài liệu phức tạp.
* **Thực thi Hiệu suất cao:** Cải thiện đáng kể thời gian phản hồi của API và trải nghiệm người dùng bằng cách tận dụng Lambda Layers để quản lý code hiệu quả và SnapStart để thực thi gần như tức thì.