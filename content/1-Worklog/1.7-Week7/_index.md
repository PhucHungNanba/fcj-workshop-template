---
title: "1.7. Week 7 Worklog"
weight: 17
draft: false
---

# 1.7. Week 7: Tự động hóa CI/CD & Bảo mật Hệ thống (Enterprise Security)

### Week 7 Objectives:

* Xây dựng luồng tích hợp và triển khai liên tục (CI/CD) tự động hoàn toàn bằng GitHub Actions.
* Triển khai cơ chế xác thực OIDC (OpenID Connect) giữa GitHub và AWS, loại bỏ rủi ro lộ lọt AWS Access Keys.
* Thiết lập các lớp bảo mật nâng cao (Security Layers) cho cơ sở dữ liệu và API bao gồm AWS Secrets Manager và AWS WAF.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Cấu hình IAM Role với trust policy cho phép GitHub Actions xác thực qua OIDC | 03/08/2026 | 03/08/2026 | README.md |
| 2 | Viết workflow `deploy.yml`: Tự động chạy unit test và deploy hạ tầng khi có code mới | 04/08/2026 | 04/08/2026 | README.md |
| 3 | Tích hợp AWS Secrets Manager để quản lý và tự động xoay vòng (rotate) credential của cơ sở dữ liệu | 05/08/2026 | 05/08/2026 | README.md |
| 4 | Cấu hình tường lửa AWS WAF (Web Application Firewall) chặn bot, spam và áp dụng rate-limit tại edge | 06/08/2026 | 06/08/2026 | Business.pdf |
| 5 | Phối hợp cùng Vương rà soát toàn bộ AWS IAM Policies, áp dụng nguyên tắc Least Privilege | 07/08/2026 | 07/08/2026 | README.md |

---

### Chi tiết thực hiện

**1. Tự động hóa Triển khai (CI/CD Pipeline)**
Hệ thống CI/CD được thiết lập dựa trên GitHub Actions kết hợp với AWS Serverless Application Model (SAM). Mỗi khi có nhánh code mới được hợp nhất (merge) vào `main`, workflow sẽ tự động kích hoạt. Quá trình bắt đầu bằng việc chạy kiểm thử tự động (Unit test) cho từng module. Nếu test pass, hệ thống mới tiến hành đóng gói (build) và triển khai (deploy) hạ tầng lên AWS.

**2. Xác thực không dùng Key (OIDC)**
Để đảm bảo an toàn tối đa cho môi trường triển khai, quy trình CI/CD hoàn toàn không sử dụng static AWS key (Access Key/Secret Key). Thay vào đó, một IAM Role đã được tạo sẵn kết nối qua giao thức OIDC (OpenID Connect), cho phép GitHub Actions xin cấp quyền truy cập tạm thời một cách an toàn.

**3. Bảo mật Dữ liệu & Tường lửa (WAF)**
* **Tầng Cơ sở dữ liệu:** Việc lưu trữ mật khẩu truy cập (credentials) của cụm cơ sở dữ liệu quan hệ được giao cho AWS Secrets Manager, đảm bảo tính năng tự động xoay vòng mật khẩu (auto-rotation).
* **Tầng Giao tiếp (Edge):** Tường lửa ứng dụng (AWS WAF) được thiết lập nhằm nhận diện và chặn đứng các địa chỉ IP có hành vi dùng tool tự động (spam tools) để upload dữ liệu rác, đảm bảo tài nguyên không bị tấn công cạn kiệt.

---

### Khó khăn & Giải pháp

* **Khó khăn:** Khi thiết lập workflow deploy tự động, GitHub Actions liên tục báo lỗi do thiếu quyền khởi tạo tài nguyên, mặc dù đã sử dụng OIDC.
* **Giải pháp:** Cùng Vương rà soát lại file cấu hình `trust-policy-oidc.json`. Nguyên nhân do IAM Role chưa được đính kèm đúng policy. Đã khắc phục bằng cách sử dụng AWS CLI để đính kèm policy cần thiết vào Role, đảm bảo workflow có đủ quyền triển khai hạ tầng.