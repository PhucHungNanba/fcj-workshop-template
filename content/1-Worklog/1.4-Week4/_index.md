---
title: "1.4. Week 4 Worklog"
weight: 14
draft: false
---

# 1.4. Week 4: Xây dựng API Cốt lõi (Backend Java 17)

### Week 4 Objectives:

* Phát triển các Lambda function xử lý nghiệp vụ quản lý tài liệu (Document CRUD) bằng ngôn ngữ Java 17.
* Xây dựng logic quản lý phiên bản (Versioning Control) và tính năng khôi phục (Rollback) cho tài liệu.
* Xử lý logic phân quyền truy cập tài liệu với các vai trò (Role): Owner, Editor, Viewer.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Lập trình Lambda function `document_crud` bằng Java 17 để tạo, đọc, sửa, xóa tài liệu | 13/07/2026 | 13/07/2026 | README.md |
| 2 | Xử lý dữ liệu văn bản từ Rich-text editor, tự động chuyển đổi sang định dạng JSON để lưu trữ | 14/07/2026 | 14/07/2026 | Business.pdf |
| 3 | Triển khai luồng quản lý phiên bản, tự động sinh `versionNumber` mới sau mỗi lần Editor lưu | 15/07/2026 | 15/07/2026 | Business.pdf |
| 4 | Lập trình chức năng Rollback, cho phép khôi phục bản cũ và khóa các bản trong quá khứ ở chế độ Read-only | 16/07/2026 | 16/07/2026 | Business.pdf |
| 5 | Hoàn thiện module Phân quyền (Permissions), thiết lập từ chối truy cập nếu không có quyền hợp lệ | 17/07/2026 | 17/07/2026 | Business.pdf |

---

### Chi tiết thực hiện

**1. Xây dựng API Quản lý Tài liệu**
Backend của hệ thống được phát triển hoàn toàn bằng Java 17 (Amazon Corretto) và AWS SDK v2. Các hàm Lambda cốt lõi như `document_crud`, `list_documents`, `folder_mgmt` đã được lập trình để xử lý dữ liệu truyền lên từ không gian soạn thảo trực tuyến (Rich-text Editing Workspace). Tại Frontend, các định dạng văn bản đặc thù (Heading, Code Snippet, Highlight) được tự động chuyển đổi sang định dạng JSON trước khi Backend tiến hành lưu trữ xuống cơ sở dữ liệu.

**2. Quản lý Phiên bản (Versioning Control)**
Nhằm bảo vệ tính toàn vẹn của lịch sử tài liệu, hệ thống tự động ghi nhận mọi thao tác chỉnh sửa của các thành viên (Editor) thành các phiên bản độc lập. 
* Mặc định, phiên bản mới nhất (`versionNumber` lớn nhất) sẽ được đặt làm bản hiện hành (`isCurrent: true`). 
* Khi người dùng thực hiện thao tác Rollback, hệ thống sẽ khôi phục một version cũ làm bản sử dụng chung, đồng thời các version trong quá khứ sẽ tự động bị khóa ở chế độ "Chỉ xem" (Read-only).

**3. Kiểm soát Phân quyền Truy cập (RBAC)**
Hệ thống hoàn thiện logic phân quyền thông qua thực thể Permissions. Chủ sở hữu tài liệu (Owner) được cấp công cụ để chia sẻ quyền hạn cho các thành viên khác bao gồm View Only (Viewer - chỉ xem) và Editor (được phép chỉnh sửa). Hệ thống được cấu hình để từ chối truy cập lập tức nếu người dùng gửi request không đi kèm quyền hợp lệ trong bảng Permissions.

---

### Khó khăn & Giải pháp

* **Khó khăn:** Các hàm Lambda viết bằng Java 17 thường gặp phải tình trạng khởi động chậm (Cold start) mất khoảng 1-3s, chậm hơn nhiều so với Python, gây ảnh hưởng đến trải nghiệm người dùng khi gọi API lần đầu.
* **Giải pháp:** Áp dụng tính năng Lambda SnapStart (chỉ hỗ trợ cho môi trường Java). Việc khai báo thuộc tính `SnapStart: ApplyOn: PublishedVersions` trong template cấu hình giúp AWS chụp sẵn snapshot của JVM đã được khởi tạo (init), từ đó giảm đáng kể thời gian khởi động lạnh của hệ thống khi có request.