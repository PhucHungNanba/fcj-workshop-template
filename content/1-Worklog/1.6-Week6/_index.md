---
title: "1.6. Week 6 Worklog"
weight: 16
draft: false
---

# 1.6. Week 6: Quy trình Phê duyệt & Quản lý Vòng đời Tài liệu

### Week 6 Objectives:

* Xây dựng quy trình điều phối phê duyệt tài liệu tự động bằng AWS Step Functions.
* Tích hợp Amazon SNS để gửi thông báo tự động (email) cho các sự kiện quan trọng trong hệ thống.
* Triển khai cơ chế chia sẻ tài liệu an toàn và quản lý vòng đời tài liệu (Lifecycle Management) đa cấp độ.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Xây dựng State Machine (`approval.asl.json`) trên AWS Step Functions để điều phối luồng phê duyệt tài liệu | 27/07/2026 | 27/07/2026 | README.md |
| 2 | Tích hợp Amazon SNS để cấu hình gửi thông báo email tự động khi có sự kiện duyệt hoặc chia sẻ tài liệu | 28/07/2026 | 28/07/2026 | README.md |
| 3 | Lập trình chức năng chia sẻ tài liệu có kiểm soát thông qua các đường dẫn hết hạn (Pre-signed URL) | 29/07/2026 | 29/07/2026 | README.md |
| 4 | Triển khai cơ chế Soft Delete, đưa tài liệu vào thùng rác (trạng thái TRASH) và cho phép khôi phục trong 30 ngày | 30/07/2026 | 30/07/2026 | Business.pdf |
| 5 | Cấu hình thuộc tính `ttl` để hệ thống tự động xóa vĩnh viễn (Hard Delete) tài liệu quá hạn | 31/07/2026 | 31/07/2026 | Business.pdf |

---

### Chi tiết thực hiện

**1. Điều phối Quy trình Phê duyệt (Step Functions)**
Nhằm giải quyết bài toán không có quy trình phê duyệt trước khi công bố nội bộ, hệ thống đã ứng dụng AWS Step Functions. Một State Machine được định nghĩa (thông qua file `approval.asl.json`) để điều phối logic của Lambda function `approval_tasks`, đảm bảo tài liệu phải trải qua các bước kiểm duyệt nghiêm ngặt từ cấp quản lý trước khi được gắn nhãn APPROVED và công bố cho toàn công ty.

**2. Thông báo tự động (Amazon SNS)**
Để tăng tính tương tác, module thông báo (`notify` function) đã được triển khai thông qua Amazon SNS. Hệ thống sẽ tự động phát (publish) một tin nhắn báo động qua email người dùng mỗi khi một tài liệu mà họ sở hữu/theo dõi được phê duyệt thành công, hoặc khi họ nhận được lượt chia sẻ tài liệu mới từ đồng nghiệp.

**3. Quản lý Vòng đời & Chia sẻ (Lifecycle & Sharing)**
* **Chia sẻ (Sharing):** Tính năng chia sẻ tài liệu ra bên ngoài (hoặc nội bộ có kiểm soát) được thực hiện bằng cách khởi tạo các đường link có giới hạn thời gian (Pre-signed URL). 
* **Quản lý vòng đời (Lifecycle):** Để ngăn ngừa thao tác xóa nhầm lẫn từ người dùng, hệ thống cung cấp hai mức độ xóa. Mức Soft Delete sẽ đánh dấu tài liệu (`status: TRASH`), đưa vào thùng rác và cho phép khôi phục trong 30 ngày. Mức Hard Delete sẽ thực sự xóa bỏ tài liệu vĩnh viễn khỏi hệ thống. Thuộc tính Time-To-Live (`ttl`) được sử dụng để tự động dọn dẹp các tài liệu nằm trong thùng rác vượt quá thời gian quy định mà không cần viết code luồng chạy ngầm phức tạp.

---

### Khó khăn & Giải pháp

* **Khó khăn:** Quản lý việc dọn dẹp các tài liệu (Hard delete) sau 30 ngày lưu trong thùng rác thường đòi hỏi phải thiết lập các kịch bản chạy ngầm (cron jobs) để quét toàn bộ cơ sở dữ liệu định kỳ, gây tiêu tốn tài nguyên tính toán.
* **Giải pháp:** Tối ưu hóa bằng cách kết hợp cơ chế `ttl` của cơ sở dữ liệu (tự động xóa bản ghi khi mốc Unix Timestamp hết hạn) cùng với Amazon EventBridge Scheduled rule (soft-delete cleanup) để ủy thác toàn bộ gánh nặng dọn dẹp (garbage collection) cho hạ tầng AWS. 