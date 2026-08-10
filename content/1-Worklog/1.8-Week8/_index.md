---
title: "1.8. Week 8 Worklog"
weight: 18
draft: false
---

# 1.8. Week 8: Kiểm thử, Giám sát & Tối ưu Chi phí Dự án

### Week 8 Objectives:

* Đảm bảo chất lượng mã nguồn thông qua Unit Test và Integration Test trên môi trường thực tế.
* Giám sát, phân tích hiệu năng hệ thống phân tán bằng AWS X-Ray và Amazon CloudWatch.
* Hoàn tất nghiệm thu, dọn dẹp tài nguyên (Clean up) để tối ưu hóa chi phí vận hành về 0 USD.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Viết Unit test cho các module backend Java 17 sử dụng framework JUnit 5 và Mockito | 10/08/2026 | 10/08/2026 | README.md |
| 2 | Chạy kịch bản kiểm thử tích hợp (E2E) trên môi trường Dev thật bằng Bash script | 11/08/2026 | 11/08/2026 | README.md |
| 3 | Tích hợp AWS X-Ray để theo dõi vết (distributed tracing) từ API Gateway tới Lambda và Database | 12/08/2026 | 12/08/2026 | README.md |
| 4 | Rà soát log hệ thống trên Amazon CloudWatch, phân tích nguyên nhân Cold Start | 13/08/2026 | 13/08/2026 | README.md |
| 5 | Dọn dẹp tài nguyên: Xóa S3 Bucket, xóa SAM stack, xóa Cognito User Pool để đưa chi phí về $0 | 14/08/2026 | 14/08/2026 | EDMS-Serverless-Roadmap.md |

---

### Chi tiết thực hiện

**1. Kiểm thử Tự động (Testing)**
Nhằm đảm bảo chất lượng phần mềm trước khi nghiệm thu, hệ thống đã trải qua hai cấp độ kiểm thử. Ở cấp độ mã nguồn, các bài Unit test được viết cho từng module Java riêng biệt, cho phép chạy cục bộ mà không tốn chi phí Cloud. Ở cấp độ hệ thống, các kịch bản Integration test được thực thi để giả lập luồng upload người dùng thực tế trên môi trường Dev đã triển khai.

**2. Giám sát & Theo dõi (Observability)**
Kiến trúc Serverless với nhiều dịch vụ phân tán rất khó để debug nếu chỉ dùng log thông thường. Hệ thống đã tích hợp AWS X-Ray để kích hoạt tính năng theo dõi vết (Distributed Tracing), giúp team dễ dàng vẽ lại bản đồ giao tiếp giữa các dịch vụ và xác định chính xác nút thắt cổ chai (bottleneck) về hiệu năng.

**3. Tối ưu Chi phí & Dọn dẹp (Tear down)**
Quản lý chi phí là một kỹ năng quan trọng trong Cloud Computing. Do một số dịch vụ không thể tự động scale về mức 0 USD khi nhàn rỗi, sau khi hoàn thành buổi demo và nghiệm thu dự án, toàn bộ hệ thống đã được "tear down" (dọn dẹp). Các lệnh xóa từ AWS CLI được sử dụng để dọn sạch hoàn toàn các tài nguyên đã khởi tạo, đảm bảo chi phí AWS trong các tháng tiếp theo sẽ được duy trì ở mức 0 USD.

---

### Khó khăn & Giải pháp

* **Khó khăn:** Quá trình chạy Integration Test bị lỗi ngẫu nhiên do hàm Lambda Java mất quá nhiều thời gian khởi động (Cold start), dẫn đến timeout ở tầng API Gateway.
* **Giải pháp:** Áp dụng kỹ thuật "khởi động ấm" (Warm up). Trước khi chạy các script test e2e tự động hoặc trước khi bắt đầu phiên demo trực tiếp, thực hiện invoke thử một lần tất cả các function để khởi tạo sẵn JVM (Java Virtual Machine), đảm bảo các request tiếp theo được xử lý trơn tru với độ trễ thấp.