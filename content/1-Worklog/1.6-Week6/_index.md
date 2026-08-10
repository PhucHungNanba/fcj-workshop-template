---
title: "Week 6: Workflow Automation, SNS & AWS SAM"
date: 2026-08-11
weight: 16
chapter: false
---

# Week 6: Workflow Automation, SNS & AWS SAM
*Tuần 6: Tự động hóa quy trình, SNS & Triển khai hạ tầng (AWS SAM)*

### Objectives | Mục tiêu tuần 6

* Automate document approval workflows using AWS Step Functions.
  *Tự động hóa quy trình phê duyệt tài liệu bằng AWS Step Functions.*
* Integrate Amazon SNS for automated email notifications and manage document lifecycles.
  *Tích hợp Amazon SNS để gửi email thông báo tự động và quản lý vòng đời tài liệu.*
* Package and deploy the entire Serverless backend using Infrastructure as Code (AWS SAM).
  *Đóng gói và triển khai toàn bộ backend Serverless bằng Code (AWS SAM).*

---

### Tasks Completed | Công việc đã thực hiện

| Day | Task Details | Date |
| :---: | :--- | :---: |
| **1** | **Approval Workflow (Step Functions)**<br>- Built a State Machine (`approval.asl.json`) on AWS Step Functions to orchestrate the document approval process.<br><br>*Quy trình Phê duyệt (Step Functions)*<br>*- Xây dựng State Machine trên AWS Step Functions để điều phối luồng phê duyệt tài liệu nghiêm ngặt.* | 27/07/2026 |
| **2** | **Event Notifications (Amazon SNS)**<br>- Integrated Amazon SNS to trigger automated email alerts for successful approvals or new document shares.<br><br>*Thông báo Sự kiện (Amazon SNS)*<br>*- Tích hợp Amazon SNS để kích hoạt gửi email tự động khi tài liệu được duyệt hoặc được chia sẻ.* | 28/07/2026 |
| **3** | **Secure Document Sharing**<br>- Programmed a controlled sharing feature generating time-limited Pre-signed URLs for external/internal access.<br><br>*Chia sẻ Tài liệu An toàn*<br>*- Lập trình chức năng chia sẻ có kiểm soát, tạo ra các đường link Pre-signed URL có giới hạn thời gian.* | 29/07/2026 |
| **4** | **Lifecycle: Soft Delete**<br>- Implemented a Soft Delete mechanism, moving documents to a TRASH state with a 30-day recovery window.<br><br>*Vòng đời: Xóa tạm thời*<br>*- Triển khai cơ chế Soft Delete, đưa tài liệu vào trạng thái Thùng rác và cho phép khôi phục trong 30 ngày.* | 30/07/2026 |
| **5** | **Lifecycle: Hard Delete Automation**<br>- Configured DynamoDB `ttl` attributes to automatically permanently delete expired documents without manual intervention.<br><br>*Vòng đời: Tự động Xóa vĩnh viễn*<br>*- Cấu hình thuộc tính `ttl` để hệ thống tự động xóa vĩnh viễn các tài liệu quá hạn mà không cần can thiệp thủ công.* | 31/07/2026 |
| **6** | **Infrastructure as Code (IaC)**<br>- Authored the `template.yaml` file using AWS SAM to define all Lambda functions, API Gateway endpoints, and DynamoDB tables.<br><br>*Triển khai Hạ tầng bằng Code (IaC)*<br>*- Viết file `template.yaml` bằng AWS SAM để khai báo toàn bộ Lambda, API Gateway và các bảng DynamoDB.* | 01/08/2026 |
| **7** | **Cloud Deployment**<br>- Executed `sam build` and `sam deploy` to provision the entire EDMS architecture onto the AWS Cloud environment.<br><br>*Triển khai lên Đám mây*<br>*- Thực thi lệnh build và deploy của SAM để tự động khởi tạo toàn bộ kiến trúc EDMS lên môi trường AWS Cloud.* | 02/08/2026 |

---

### Results Achieved | Kết quả đạt được

* **Automated Business Logic:** Successfully orchestrated complex enterprise workflows without writing messy nested code. AWS Step Functions handles the approvals, while SNS ensures users are instantly notified.
  *Tự động hóa Nghiệp vụ: Điều phối thành công các quy trình doanh nghiệp phức tạp mà không cần viết code lồng nhau rối rắm. Step Functions xử lý việc phê duyệt, trong khi SNS đảm bảo người dùng nhận được thông báo tức thì.*

* **Streamlined Deployment:** Replaced manual console configurations with AWS SAM. The entire project can now be spun up or torn down in minutes using code, drastically reducing operational overhead and garbage collection costs.
  *Triển khai Tối ưu: Thay thế thao tác thủ công trên giao diện bằng AWS SAM. Toàn bộ dự án giờ đây có thể được khởi tạo hoặc gỡ bỏ chỉ trong vài phút bằng code, giảm thiểu tối đa chi phí vận hành và dọn dẹp hệ thống.*