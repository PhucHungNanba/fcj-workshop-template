---
title: "Week 8"
date: 2026-08-16
weight: 18
chapter: false
---

# Week 8: Testing, Observability & Cost Optimization

### Objectives

* Ensure code quality through Unit Tests and Integration Tests on real environments.
* Monitor and analyze distributed system performance using AWS X-Ray and Amazon CloudWatch.
* Finalize project handover, complete documentation, and clean up resources to optimize costs to $0.

---

### Tasks Completed

| Day | Task Details | Date |
| :---: | :--- | :---: |
| **1** | **Unit Testing**<br>- Wrote unit tests for Java 17 backend modules using the JUnit 5 and Mockito frameworks. | 10/08/2026 |
| **2** | **Integration Testing (E2E)**<br>- Executed end-to-end integration test scripts using Bash on the actual deployed Dev environment. | 11/08/2026 |
| **3** | **Distributed Tracing (AWS X-Ray)**<br>- Integrated AWS X-Ray to trace requests from API Gateway through Lambda to the Database. | 12/08/2026 |
| **4** | **System Monitoring (CloudWatch)**<br>- Reviewed system logs on Amazon CloudWatch and analyzed root causes for Lambda Cold Starts. | 13/08/2026 |
| **5** | **Documentation & Report**<br>- Compiled the final internship report and documented the entire Serverless EDMS architecture. | 14/08/2026 |
| **6** | **Final Demo & Handover**<br>- Conducted the final project demonstration, presenting the automated workflows and AI integration to the mentors. | 15/08/2026 |
| **7** | **Resource Cleanup (Tear Down)**<br>- Executed clean-up commands to delete S3 Buckets, Cognito User Pools, and the SAM stack, successfully reducing ongoing AWS costs to $0. | 16/08/2026 |

---

### Results Achieved

* **System Reliability & Observability:** Ensured the system runs flawlessly through rigorous multi-level testing. The integration of AWS X-Ray and CloudWatch provides complete visibility into the distributed architecture, making debugging highly efficient.
* **Cost Efficiency Mastery:** Successfully demonstrated cloud cost management skills. By systematically tearing down all provisioned resources post-demo, the project guarantees zero unexpected charges moving forward.

---

### Challenges & Solutions

* **Challenge:** The Integration Test process occasionally failed due to Java Lambda functions taking too long to start (Cold Start), resulting in API Gateway timeouts.
* **Solution:** Applied a "Warm Up" technique. Prior to running automated e2e scripts or starting the live demo, all functions were invoked once to pre-initialize the JVM, ensuring subsequent requests were processed smoothly with minimal latency.