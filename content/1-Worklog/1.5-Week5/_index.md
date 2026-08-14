---
title: "Week 5"
date: 2026-07-26
weight: 15
chapter: false
---

# Week 5: EDMS Project - Backend Logic & API Gateway

### Objectives

* Develop core document management APIs (CRUD) using Java 17 and AWS Lambda.
* Implement Versioning Control, Role-Based Access Control (RBAC), and optimize performance.

---

### Tasks Completed

| Day | Task Details | Date |
| :---: | :--- | :---: |
| **1** | **Core API Development**<br>- Programmed Lambda functions (`document_crud`, `list_documents`) using Java 17 (Amazon Corretto) to handle document creation and retrieval. | 20/07/2026 |
| **2** | **Code Optimization (Lambda Layers)**<br>- Extracted shared libraries and utilities from 9 independent Lambda functions into AWS Lambda Layers to reduce deployment package size. | 21/07/2026 |
| **3** | **Versioning Control & Rollback**<br>- Implemented version control logic to automatically generate a new `versionNumber` upon edits.<br>- Built a Rollback feature that restores previous versions while locking historical data in Read-only mode. | 22/07/2026 |
| **4** | **Role-Based Access Control (RBAC)**<br>- Finalized the Permissions module to enforce strict access boundaries for Owners, Editors, and Viewers at the API level. | 23/07/2026 |
| **5** | **Cold Start Mitigation (SnapStart)**<br>- Resolved Java 17 cold start delays (1-3s) by enabling AWS Lambda SnapStart, taking pre-initialized JVM snapshots to accelerate response times. | 24/07/2026 |

---

### Results Achieved

* **Robust Backend Logic:** Successfully deployed a fully functional, secure, and version-controlled backend API capable of handling complex document workflows.
* **High-Performance Execution:** Dramatically improved API response times and user experience by leveraging Lambda Layers for efficient code management and SnapStart for instant execution.