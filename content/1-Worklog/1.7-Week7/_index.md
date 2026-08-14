---
title: "Week 7"
date: 2026-08-09
weight: 17
chapter: false
---

# Week 7: CI/CD Automation, Security & AI Integration

### Objectives

* Establish a fully automated CI/CD pipeline using GitHub Actions and keyless OIDC authentication.
* Implement advanced security layers (AWS WAF, Secrets Manager) and review IAM policies.
* Integrate OCR capabilities via EventBridge for asynchronous document text extraction.

---

### Tasks Completed

| Day | Task Details | Date |
| :---: | :--- | :---: |
| **1** | **OIDC Authentication Setup**<br>- Configured an IAM Role with a trust policy allowing GitHub Actions to authenticate securely via OIDC, eliminating static AWS Keys. | 03/08/2026 |
| **2** | **CI/CD Pipeline (GitHub Actions)**<br>- Authored the `deploy.yml` workflow to automatically run unit tests and deploy infrastructure upon new code merges. | 04/08/2026 |
| **3** | **Database Security (Secrets Manager)**<br>- Integrated AWS Secrets Manager to securely store and auto-rotate the Aurora database credentials. | 05/08/2026 |
| **4** | **Edge Protection (AWS WAF)**<br>- Configured AWS Web Application Firewall (WAF) to block spam bots and enforce rate-limiting at the network edge. | 06/08/2026 |
| **5** | **IAM Least Privilege Review**<br>- Collaborated with group partner Nguyễn Như Vương to audit all AWS IAM Policies, ensuring the Least Privilege principle is strictly enforced. | 07/08/2026 |
| **6** | **AI Data Extraction (OCR)**<br>- Integrated OCR tools to automatically extract raw text from uploaded images and PDFs, saving it to the `OCRResults` entity. | 08/08/2026 |
| **7** | **Asynchronous Event Processing**<br>- Configured S3 Events and Amazon EventBridge to trigger the heavy OCR tasks asynchronously in the background, preventing API timeouts. | 09/08/2026 |

---

### Results Achieved

* **Zero-Key Deployment & Enterprise Security:** Achieved a highly secure deployment environment using OIDC. Database credentials are auto-rotated, and the system is shielded from malicious traffic by AWS WAF.
* **High-Performance AI Automation:** Successfully decoupled the heavy AI extraction process from the user upload flow. The event-driven architecture ensures users experience zero lag while the OCR runs asynchronously.