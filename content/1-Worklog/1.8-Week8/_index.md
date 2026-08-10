---
title: "Week 8: Testing, Observability & Cost Optimization"
date: 2026-08-11
weight: 18
chapter: false
---

# Week 8: Testing, Observability & Cost Optimization
*Tuần 8: Kiểm thử, Giám sát & Tối ưu Chi phí Dự án*

### Objectives | Mục tiêu tuần 8

* Ensure code quality through Unit Tests and Integration Tests on real environments.
  *Đảm bảo chất lượng mã nguồn thông qua Unit Test và Integration Test trên môi trường thực tế.*
* Monitor and analyze distributed system performance using AWS X-Ray and Amazon CloudWatch.
  *Giám sát, phân tích hiệu năng hệ thống phân tán bằng AWS X-Ray và Amazon CloudWatch.*
* Finalize project handover, complete documentation, and clean up resources to optimize costs to $0.
  *Hoàn tất nghiệm thu, viết báo cáo và dọn dẹp tài nguyên để tối ưu hóa chi phí vận hành về 0 USD.*

---

### Tasks Completed | Công việc đã thực hiện

| Day | Task Details | Date |
| :---: | :--- | :---: |
| **1** | **Unit Testing**<br>- Wrote unit tests for Java 17 backend modules using the JUnit 5 and Mockito frameworks.<br><br>*Kiểm thử Đơn vị*<br>*- Viết Unit test cho các module backend Java 17 sử dụng framework JUnit 5 và Mockito.* | 10/08/2026 |
| **2** | **Integration Testing (E2E)**<br>- Executed end-to-end integration test scripts using Bash on the actual deployed Dev environment.<br><br>*Kiểm thử Tích hợp*<br>*- Chạy kịch bản kiểm thử tích hợp (E2E) trên môi trường Dev thật bằng Bash script.* | 11/08/2026 |
| **3** | **Distributed Tracing (AWS X-Ray)**<br>- Integrated AWS X-Ray to trace requests from API Gateway through Lambda to the Database.<br><br>*Theo dõi Phân tán (AWS X-Ray)*<br>*- Tích hợp AWS X-Ray để theo dõi vết (distributed tracing) từ API Gateway tới Lambda và Database.* | 12/08/2026 |
| **4** | **System Monitoring (CloudWatch)**<br>- Reviewed system logs on Amazon CloudWatch and analyzed root causes for Lambda Cold Starts.<br><br>*Giám sát Hệ thống (CloudWatch)*<br>*- Rà soát log hệ thống trên Amazon CloudWatch, phân tích nguyên nhân Cold Start.* | 13/08/2026 |
| **5** | **Documentation & Report**<br>- Compiled the final internship report and documented the entire Serverless EDMS architecture.<br><br>*Viết Báo cáo & Tài liệu*<br>*- Hoàn thiện báo cáo thực tập cuối kỳ và viết tài liệu cho toàn bộ kiến trúc Serverless EDMS.* | 14/08/2026 |
| **6** | **Final Demo & Handover**<br>- Conducted the final project demonstration, presenting the automated workflows and AI integration to the mentors.<br><br>*Demo Nghiệm thu*<br>*- Thực hiện buổi demo dự án cuối kỳ, trình bày các luồng tự động hóa và tích hợp AI với các mentor.* | 15/08/2026 |
| **7** | **Resource Cleanup (Tear Down)**<br>- Executed clean-up commands to delete S3 Buckets, Cognito User Pools, and the SAM stack, successfully reducing ongoing AWS costs to $0.<br><br>*Dọn dẹp Tài nguyên*<br>*- Chạy lệnh xóa S3 Bucket, Cognito User Pool và hạ tầng SAM, đưa chi phí duy trì AWS về 0 USD.* | 16/08/2026 |

---

### Results Achieved | Kết quả đạt được

* **System Reliability & Observability:** Ensured the system runs flawlessly through rigorous multi-level testing. The integration of AWS X-Ray and CloudWatch provides complete visibility into the distributed architecture, making debugging highly efficient.
  *Độ tin cậy & Khả năng giám sát: Đảm bảo hệ thống chạy mượt mà thông qua các bài test nghiêm ngặt đa cấp độ. Việc tích hợp AWS X-Ray và CloudWatch mang lại khả năng quan sát toàn diện kiến trúc phân tán, giúp việc gỡ lỗi trở nên cực kỳ hiệu quả.*

* **Cost Efficiency Mastery:** Successfully demonstrated cloud cost management skills. By systematically tearing down all provisioned resources post-demo, the project guarantees zero unexpected charges moving forward.
  *Làm chủ Tối ưu Chi phí: Thể hiện thành công kỹ năng quản lý chi phí đám mây. Bằng cách dọn dẹp có hệ thống toàn bộ tài nguyên sau buổi demo, dự án đảm bảo không phát sinh bất kỳ khoản phí ngoài ý muốn nào trong tương lai.*

---

### Challenges & Solutions | Khó khăn & Giải pháp

* **Challenge (Khó khăn):** The Integration Test process occasionally failed due to Java Lambda functions taking too long to start (Cold Start), resulting in API Gateway timeouts.
  *(Quá trình chạy Integration Test bị lỗi ngẫu nhiên do hàm Lambda Java mất quá nhiều thời gian khởi động, dẫn đến timeout ở tầng API Gateway.)*
* **Solution (Giải pháp):** Applied a "Warm Up" technique. Prior to running automated e2e scripts or starting the live demo, all functions were invoked once to pre-initialize the JVM, ensuring subsequent requests were processed smoothly with minimal latency.
  *(Áp dụng kỹ thuật "khởi động ấm". Trước khi chạy các script test tự động hoặc demo trực tiếp, thực hiện gọi thử một lần tất cả các function để khởi tạo sẵn JVM, đảm bảo các request tiếp theo được xử lý trơn tru với độ trễ thấp.)*