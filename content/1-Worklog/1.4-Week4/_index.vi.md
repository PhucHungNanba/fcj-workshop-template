---
title: "Tuần 4"
date: 2026-07-19
weight: 14
chapter: false
---

# Tuần 4: Dự án EDMS - Thiết lập Cơ sở dữ liệu & Lưu trữ

### Mục tiêu

* Thiết kế và triển khai kiến trúc cơ sở dữ liệu đa ngôn ngữ lưu trữ (Polyglot Persistence) sử dụng Amazon Aurora và DynamoDB.
* Cấu hình lưu trữ đối tượng an toàn cho các tệp vật lý và thiết lập hệ thống xác thực người dùng tập trung.

---

### Các công việc đã hoàn thành

| Ngày | Chi tiết công việc | Ngày tháng |
| :---: | :--- | :---: |
| **1** | **Thiết kế Lược đồ Cơ sở dữ liệu**<br>- Thiết kế lược đồ Polyglot Persistence: sử dụng Aurora Serverless v2 (MySQL) cho dữ liệu quan hệ (Tài liệu, Phiên bản, Thẻ tag) và DynamoDB cho Nhật ký kiểm toán (AuditLogs). | 13/07/2026 |
| **2** | **Cấu hình DynamoDB & TTL**<br>- Cấu hình bảng AuditLogs trên DynamoDB với Khóa phân vùng (Partition Key) là (`DOC#<documentId>`) và Khóa sắp xếp (Sort Key) là (`LOG#<timestamp>`).<br>- Kích hoạt tính năng Time-To-Live (TTL) để tự động xóa các log hết hạn nhằm tiết kiệm chi phí. | 14/07/2026 |
| **3** | **Quản lý Danh tính với Cognito**<br>- Tích hợp Amazon Cognito User Pool để xử lý đăng nhập và xác minh mật khẩu.<br>- Tạo các nhóm người dùng (ví dụ: HR, SALES) để hỗ trợ mô hình kiểm soát quyền truy cập dựa trên vai trò (role-based access control) cấp doanh nghiệp. | 15/07/2026 |
| **4** | **Lưu trữ An toàn với S3 Presigned URLs**<br>- Thiết lập một Amazon S3 bucket để lưu trữ tệp tin vật lý.<br>- Xây dựng cơ chế tải lên an toàn sử dụng Presigned URLs với thời gian hết hạn nghiêm ngặt từ 5-10 phút để ngăn chặn việc lạm dụng băng thông. | 16/07/2026 |

---

### Kết quả đạt được

* **Kiến trúc Cơ sở dữ liệu có khả năng mở rộng:** Tách biệt thành công luồng ghi dữ liệu lớn (write-heavy) của AuditLog sang DynamoDB, giải quyết hoàn toàn nguy cơ thắt nút cổ chai hiệu suất (bottlenecks) trên cơ sở dữ liệu quan hệ chính Aurora.
* **Bảo mật Cấp Doanh nghiệp:** Thiết lập một vành đai bảo mật vững chắc bằng cách kết hợp Cognito để quản lý danh tính và S3 Presigned URLs có thời hạn ngắn để tải file lên trực tiếp mà không cần cung cấp thông tin xác thực (credential-free).