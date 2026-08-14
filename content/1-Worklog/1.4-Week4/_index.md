---
title: "Week 4"
date: 2026-07-19
weight: 14
chapter: false
---

# Week 4: EDMS Project - Database & Storage Setup

### Objectives

* Design and implement a Polyglot Persistence database architecture using Amazon Aurora and DynamoDB.
* Configure secure object storage for physical files and set up centralized user authentication.

---

### Tasks Completed

| Day | Task Details | Date |
| :---: | :--- | :---: |
| **1** | **Database Schema Design**<br>- Designed the Polyglot Persistence schema: Aurora Serverless v2 (MySQL) for relational data (Documents, Versions, Tags) and DynamoDB for AuditLogs. | 13/07/2026 |
| **2** | **DynamoDB & TTL Configuration**<br>- Configured the DynamoDB AuditLogs table with Partition Key (`DOC#<documentId>`) and Sort Key (`LOG#<timestamp>`).<br>- Enabled Time-To-Live (TTL) to automatically delete expired logs and save costs. | 14/07/2026 |
| **3** | **Identity Management with Cognito**<br>- Integrated Amazon Cognito User Pool to handle login and password verification.<br>- Created user groups (e.g., HR, SALES) to support enterprise-level role-based access control. | 15/07/2026 |
| **4** | **Secure Storage with S3 Presigned URLs**<br>- Set up an Amazon S3 bucket for physical file storage.<br>- Engineered a secure upload mechanism using Presigned URLs with a strict 5-10 minute expiration window to prevent bandwidth abuse. | 16/07/2026 |

---

### Results Achieved

* **Scalable Database Architecture:** Successfully decoupled the write-heavy AuditLog stream to DynamoDB, fully resolving potential performance bottlenecks on the main Aurora relational database.
* **Enterprise-Grade Security:** Established a robust security perimeter by combining Cognito for identity management and short-lived S3 Presigned URLs for direct, credential-free file uploads.