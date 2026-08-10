---
title: "1.3. Week 3 Worklog"
weight: 13
draft: false
---

# 1.3. Week 3: Xác thực Danh tính & Quản lý Tệp Vật lý

### Week 3 Objectives:

* Tích hợp dịch vụ Amazon Cognito để quản lý xác thực định danh người dùng an toàn.
* Triển khai cơ chế kiểm soát tải tệp tin vật lý lên hạ tầng Amazon S3 thông qua Presigned URL[cite: 1, 2].
* Thiết lập cấu trúc mã nguồn dùng chung (Lambda Layers) để tối ưu hoá backend Java 17.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Tích hợp Amazon Cognito để ủy quyền toàn bộ quá trình đăng nhập và xác thực mật khẩu | 06/07/2026 | 06/07/2026 | Business.pdf |
| 2 | Khởi tạo các nhóm phân quyền (Groups) trong Cognito User Pool theo cấu trúc phòng ban (VD: SALES, HR) | 07/07/2026 | 07/07/2026 | README.md |
| 3 | Cấu hình Amazon S3 để lưu trữ file gốc và tích hợp tính năng tạo Presigned URL cho việc upload | 08/07/2026 | 08/07/2026 | EDMS-Serverless-Roadmap.md |
| 4 | Cấu hình giới hạn thời gian sống (Expiration) từ 5-10 phút cho URL tải lên để tăng cường bảo mật | 09/07/2026 | 09/07/2026 | Business.pdf |
| 5 | Đóng gói mã nguồn Java dùng chung thành AWS Lambda Layers phục vụ cho 9 function backend độc lập | 10/07/2026 | 10/07/2026 | README.md |

---

### Chi tiết thực hiện

**1. Quản lý Danh tính & Phân quyền (IAM)**
Hệ thống EDMS đã được tích hợp với Amazon Cognito để xử lý việc định danh người dùng thông qua các giao thức bảo mật tiêu chuẩn, trong đó việc xác thực mật khẩu được giao phó hoàn toàn cho Cognito. Nhằm đáp ứng bài toán quản lý tài liệu theo mô hình doanh nghiệp, các nhóm người dùng (Groups) đã được tạo sẵn trong Cognito để phân luồng người dùng theo từng phòng ban chức năng.

**2. Kiểm soát Tải lên Tệp vật lý (Upload Protection)**
Để tối ưu hóa luồng dữ liệu và tránh nghẽn băng thông tại tầng API, hệ thống thực hiện cơ chế tải file vật lý trực tiếp lên Amazon S3 thông qua Presigned URL. 
Cơ chế này được cấu hình các quy chuẩn bảo mật Enterprise: mỗi URL được cấp phát chỉ có thời gian sống (Expiration) rất ngắn từ 5-10 phút và bị áp đặt giới hạn về dung lượng tải lên. Nếu đường link hết hạn hoặc tệp tin vượt mức cho phép, đường truyền sẽ tự động bị đóng lại ở tầng Cloud, ngăn chặn triệt để các hành vi lạm dụng.

**3. Tối ưu hoá Mã nguồn Backend (Lambda Layers)**
Hệ thống backend được cấu thành từ 9 Lambda function viết bằng Java 17. Quá trình phát triển cho thấy có nhiều thư viện và đoạn mã (utils) được sử dụng lặp lại giữa các function. Giải pháp được triển khai trong tuần này là trích xuất các thành phần dùng chung đó và thiết lập thành AWS Lambda Layers, giúp giảm kích thước gói triển khai (fat-jar) và chuẩn hóa cấu trúc mã nguồn.

---

### Khó khăn & Giải pháp

* **Khó khăn:** Yêu cầu thiết kế kiến trúc phải cho phép người dùng cuối (client) upload và tải tài liệu nhanh chóng, an toàn nhưng tuyệt đối không được làm lộ thông tin xác thực (credentials) của AWS.
* **Giải pháp:** Sử dụng kết hợp Lambda function và S3 Presigned URL. Khi người dùng cần tải file, client sẽ gọi API để Lambda (có quyền IAM an toàn) sinh ra một đường dẫn upload tạm thời. Client sau đó dùng đường dẫn này đẩy thẳng file lên S3, đáp ứng trọn vẹn mục tiêu bảo mật đề ra.