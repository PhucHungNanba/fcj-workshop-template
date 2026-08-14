---
title: "Week 6"
date: 2026-08-02
weight: 16
chapter: false
---

# Week 6: Workflow Automation, SNS & AWS SAM

### Objectives

* Automate document approval workflows using AWS Step Functions.
* Integrate Amazon SNS for automated email notifications and manage document lifecycles.
* Package and deploy the entire Serverless backend using Infrastructure as Code (AWS SAM).

---

### Tasks Completed

| Day | Task Details | Date |
| :---: | :--- | :---: |
| **1** | **Approval Workflow (Step Functions)**<br>- Built a State Machine (`approval.asl.json`) on AWS Step Functions to orchestrate the document approval process. | 27/07/2026 |
| **2** | **Event Notifications (Amazon SNS)**<br>- Integrated Amazon SNS to trigger automated email alerts for successful approvals or new document shares. | 28/07/2026 |
| **3** | **Secure Document Sharing**<br>- Programmed a controlled sharing feature generating time-limited Pre-signed URLs for external/internal access. | 29/07/2026 |
| **4** | **Lifecycle: Soft Delete**<br>- Implemented a Soft Delete mechanism, moving documents to a TRASH state with a 30-day recovery window. | 30/07/2026 |
| **5** | **Lifecycle: Hard Delete Automation**<br>- Configured DynamoDB `ttl` attributes to automatically permanently delete expired documents without manual intervention. | 31/07/2026 |
| **6** | **Infrastructure as Code (IaC)**<br>- Authored the `template.yaml` file using AWS SAM to define all Lambda functions, API Gateway endpoints, and DynamoDB tables. | 01/08/2026 |
| **7** | **Cloud Deployment**<br>- Executed `sam build` and `sam deploy` to provision the entire EDMS architecture onto the AWS Cloud environment. | 02/08/2026 |

---

### Results Achieved

* **Automated Business Logic:** Successfully orchestrated complex enterprise workflows without writing messy nested code. AWS Step Functions handles the approvals, while SNS ensures users are instantly notified.
* **Streamlined Deployment:** Replaced manual console configurations with AWS SAM. The entire project can now be spun up or torn down in minutes using code, drastically reducing operational overhead and garbage collection costs.