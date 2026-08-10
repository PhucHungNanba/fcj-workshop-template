---
title: "1.5. Week 5 Worklog"
weight: 15
draft: false
---

# 1.5. Week 5: Tích hợp AI (OCR) & Lưu vết Truy cập (Audit Trail)

### Week 5 Objectives:

* Tích hợp công cụ quét ảnh (OCR) để tự động nhận diện chữ từ tài liệu hình ảnh/PDF.
* Cấu hình luồng xử lý sự kiện bất đồng bộ (asynchronous) thông qua S3 Event và Amazon EventBridge.
* Hoàn thiện hệ thống nhật ký truy cập (AuditLogs) trên DynamoDB để giám sát các hành vi nhạy cảm của người dùng.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Tích hợp công cụ OCR tự động trích xuất văn bản thô từ file tài liệu và lưu vào thực thể OCRResults | 20/07/2026 | 20/07/2026 | Business.pdf |
| 2 | Cấu hình Amazon EventBridge và S3 Event để kích hoạt luồng xử lý OCR bất đồng bộ khi có file mới | 21/07/2026 | 21/07/2026 | Cả 2 tài liệu |
| 3 | Lập trình tính năng ghi AuditLog cho các hành động nhạy cảm: DOWNLOAD, EXPORT, UPDATE_PERMISSION, DELETE | 22/07/2026 | 22/07/2026 | Business.pdf |
| 4 | Thu thập thông tin truy vết chuyên sâu: Thời gian phát sinh (Timestamp), địa chỉ IP máy khách, định danh người dùng (Cognito sub) | 23/07/2026 | 23/07/2026 | Cả 2 tài liệu |
| 5 | Tối ưu hóa cấu trúc ghi liên tục (write-heavy) của AuditLog trên DynamoDB | 24/07/2026 | 24/07/2026 | README.md |
---

### Chi tiết thực hiện

**1. Trích xuất Dữ liệu Thông minh (OCR)**
Hệ thống được nâng cấp với khả năng tự động nhận diện và trích xuất chữ (text) từ các tài liệu hình ảnh hoặc tệp PDF rõ chữ, nhằm tiết kiệm thời gian nhập liệu thủ công cho người dùng. Dữ liệu văn bản thô sau khi được quét sẽ được lưu trữ vào thực thể OCRResults, liên kết trực tiếp với tài liệu gốc thông qua `documentId`.

**2. Kiến trúc Xử lý Bất đồng bộ (Event-Driven)**
Để không làm gián đoạn trải nghiệm người dùng trong quá trình tải file, luồng xử lý OCR được thiết kế theo kiến trúc bất đồng bộ. Khi tệp vật lý được tải lên S3 thành công, một sự kiện (S3 Event) kết hợp cùng Amazon EventBridge sẽ được phát đi để kích hoạt Lambda function chạy ngầm xử lý trích xuất văn bản.

**3. Nhật ký Truy vết Doanh nghiệp (Enterprise Audit Trail)**
Nhằm phục vụ công tác kiểm toán và truy vết rò rỉ dữ liệu, quản trị viên (Administrator) được cung cấp hệ thống lưu vết mọi hành động tải xuống (Download) và thao tác nhạy cảm. 
Dữ liệu nhật ký được thiết kế dạng append-only (chỉ ghi thêm) trên DynamoDB nhằm đáp ứng tần suất ghi liên tục (write-heavy). Mọi bản ghi AuditLog đều đính kèm thông tin bắt buộc gồm: mốc thời gian (Timestamp), địa chỉ IP của máy khách khi thực hiện lệnh, định danh người dùng và chi tiết siêu dữ liệu thao tác.

---

### Khó khăn & Giải pháp

* **Khó khăn:** Các tài liệu định dạng PDF hoặc hình ảnh có dung lượng lớn thường mất nhiều thời gian để thực hiện quét OCR. Nếu xử lý đồng bộ (synchronous) ngay khi người dùng upload file, API Gateway sẽ bị quá thời gian chờ (timeout), gây lỗi hệ thống.
* **Giải pháp:** Phân tách hoàn toàn quy trình tải file và quy trình xử lý dữ liệu AI. Lambda function xử lý API upload chỉ làm nhiệm vụ ghi nhận metadata của file và trả về phản hồi thành công ngay lập tức cho client. Tác vụ OCR nặng nề được đẩy về phía hậu cảnh (background) và được kích hoạt tự động qua EventBridge.