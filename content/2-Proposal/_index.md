---
title: "Proposal"
 
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

In this section, you need to summarize the contents of the workshop that you **plan** to conduct.

# **Jewelry E-Commerce Platform**  
## **Cloud-Based Online Sales System Using React, .NET, and MySQL on AWS Lightsail**  

---

## **1. EXECUTIVE SUMMARY**

The AWS Jewelry Web is a project to build a jewelry e-commerce website platform (Jewelry E-commerce Website) with the backend system and database running on AWS Lightsail and the React frontend deployed on Amazon S3 + CloudFront. The system aims for scalability, high security, and optimized operating costs by utilizing basic but effective Cloud services.

The system provides the following main features:

  * Jewelry product management

  * Product image upload

  * Shopping cart

  * Sign up / Sign in using AWS Cognito

  * Backend API running on Lightsail and storing MySQL/Postgres data

  * CDN to speed up page loading and handle international standard SSL.

### **1.1 PROJECT SUCCESS CRITERIA**
  * Fast international website load time < 2s thanks to CloudFront CDN.

  * Backend operates stably on Lightsail with real-world traffic.

  * Database operates securely and retrieves data quickly.

  * Stable user management using Cognito.

  * Image uploads via S3 are secured.

  * Comprehensive API logging via CloudWatch.

### **1.2 ASSUMPTIONS**
  * Moderate traffic level (<100k requests/month).

  * No advanced autoscaling is required.

  * The Domain is already owned or will be purchased via Route 53.

  * The development team is familiar with Node.js/React.

## **2. SOLUTION ARCHITECTURE / ARCHITECTURAL DIAGRAM**

### **2.1 TECHNICAL ARCHITECTURE DIAGRAM**


### **2.2 TECHNICAL PLAN**

  * Frontend: S3 hosting + CloudFront CDN + HTTPS with ACM.

  * Backend API: Running Node.js on Lightsail.

  * Database: MySQL/Postgres on Lightsail.

  * Auth: Cognito User Pool.

  * Image storage: S3.

  * Logging: CloudWatch.

  * Secrets: Secrets Manager.

### **2.3 PROJECT PLAN**
  * Implementation time is 6 weeks -> 12 weeks depending on the scope.

### **2.4 SECURITY CONSIDERATIONS**
  * S3 private access, only CloudFront has read permission.

  * API uses private key stored in Secrets Manager.

  * HTTPS across the entire system.

  * Cognito protects user login.


## **3. ACTIVITIES AND DELIVERABLES**

### **3.1 ACTIVITIES AND DELIVERABLES**

| Project Phase | Timeline | Activities | Deliverables / Milestones | MD |
| :--- | :--- | :--- | :--- | :--- |
| **Assessment** | Week 1 | - Phân tích hệ thống Jewelry Web | - Architecture Diagram | 5 |
| | | - Vẽ Architecture Diagram | - DB Schema | |
| | | - Thiết kế DB (Lightsail MySQL/Postgres) | - Danh sách secrets | |
| | | - Xác định secrets cần sử dụng (DB password, bucket-name) | | |
| **Setup Base Infrastructure** | Week 2 | - Setup S3 hosting + React build | - Frontend CDN hoạt động | 7 |
| | | - Setup CloudFront CDN + ACM SSL | - Backend API hoạt động | |
| | | - Route 53 domain mapping | - DB kết nối | |
| | | - Setup Lightsail API instance | - Cognito login hoạt động | |
| | | - Setup Lightsail Database | - Secrets Manager chứa DB password & bucket-name | |
| | | - Setup Cognito Login | | |
| | | - Tạo Secrets Manager: + secret 1: DB\_PASSWORD + secret 2: APP\_CONFIG (bucket-name) | | |
| | | - Gán IAM cho API instance được phép đọc secrets | | |
| | | - Bật CloudWatch logs | | |
| **Setup Component 1 – Backend API** | Week 3 | - API đọc DB password từ Secrets Manager | - API hoạt động ổn định | 7 |
| | | - API đọc bucket-name từ Secrets Manager | - Upload ảnh OK | |
| | | - Upload ảnh lên S3 (presigned URL) | - Login OK | |
| | | - CRUD sản phẩm trang sức | - Secrets Manager hoàn toàn thay thế config hardcode | |
| | | - Tích hợp Cognito | | |
| | | - Gửi logs lên CloudWatch | | |
| **Setup Component 2 – Frontend React** | Week 4 | - Xây UI Jewelry Shop | - UI hoàn chỉnh | 7 |
| | | - Login Cognito | - Kết nối API | |
| | | - Upload ảnh trang sức | | |
| | | - Lấy dữ liệu từ API | | |
| | | - Build deploy lên S3 + CloudFront | | |
| **Testing & Go-live** | Week 5 | - Integration testing FE ↔ BE ↔ S3 ↔ DB | - Test Report | 5 |
| | | - Security test IAM + Secrets Manager | - Security checklist | |
| | | - End-to-end testing | | |
| **Handover** | Week 6 | - Hướng dẫn dùng Secrets Manager để đổi bucket name/DB password | - Runbook đầy đủ | 5 |
| | | - Bàn giao AWS account | - Project closure | |
| | | - Runbook Documentation | | |

### **3.2 OUT OF SCOPE**

  * AI/ML Features.

  * Complex E-commerce Features.

  * Advanced Image Processing.

  * No Multi-region / DR site deployment.

  * No support for complex administration system.

  * Does not include integration of 3rd party systems.

### **3.3 PATH TO PRODUCTION**

  * Operational Excellence Optimization

  * Secrets Management – Production Hardening

  * Extended Error Handling

  * Deployment & Production Verification

  * Disaster Recovery Plan

  * Production Handover


## **4. EXPECTED AWS COST BREAKDOWN BY SERVICES**

| Service Name | Upfront cost  | Monthly cost  | Region |
| :--- | :--- | :--- | :--- |
| **Amazon S3** | 0.00 USD | 0.26 USD | Asia Pacific (Singapore) |
| **Amazon CloudFront (CDN for FE)** | 0.00 USD | 0.17 USD | Asia Pacific (Singapore) |
| **AWS ACM** | 0.00 USD | 0 USD | Asia Pacific (Singapore) |
| **Amazon Route 53** | 0.00 USD | 0.50–1.00 USD | Asia Pacific (Singapore) |
| **AWS Lightsail – Database** | 0.00 USD | 10–15 USD | Asia Pacific (Singapore) |
| **Amazon Cognito** | 0.00 USD | 2.00 USD | Asia Pacific (Singapore) |
| **AWS Secrets Manager** | 0.00 USD | 0.40 USD | Asia Pacific (Singapore) |
| **Amazon CloudWatch** | 0.00 USD | 0.30 USD | Asia Pacific (Singapore) |
| **AWS Lightsail – API Server** | 0.00 USD | 5 - 10 USD | Asia Pacific (Singapore) |

## **5. TEAM**

### **Partner Executive Sponsor** 

| Name  | Title  | Description | Email / Contact Info |
| :--- | :--- | :--- | :--- |
| | | | |

---

### **Project Stakeholders** 

| Name  | Title  | Stakeholder for  | Email / Contact Info  |
| :--- | :--- | :--- | :--- |
| | | | |

---

### **Partner Project Team** 

| Name  | Title  | Role  | Email / Contact Info  |
| :--- | :--- | :--- | :--- |
| | Product Owner | | |
| | Project Manager | | |
| ... | ... | | |
| | Software Developer | Developer | |
| ... | ... | | |
| | Software Developer | Developer | |
| ... | ... | | |
| | Software Developer | Developer | |
| ... | ... | | |
| | Software Developer | Developer | |

---

### **Project Escalation Contacts** 

| Name  | Title  | Role  | Email / Contact Info  |
| :--- | :--- | :--- | :--- |
| | | | |

## **6. Estimated Budget**

| **Service** | **Description** | **Estimated Monthly Cost (USD)** | **Notes** |
|--------------|----------------|----------------------------------|------------|
| Lightsail Instance (.NET API) | 2–4 vCPU, 4–8 GB RAM | $10–$40 | Recommended ≥$20 plan |
| Lightsail MySQL Database | 20–50 GB managed DB | $15–$50 | Better kept separate from instance |
| Amazon S3 | Store static files and images | $1–$5 | Includes request fees |
| Amazon CloudFront | CDN distribution | $1–$30 | First 1TB free/month |
| Route 53 + ACM | Domain and SSL | $1–$4 | ACM free; domain ~$12/year |
| Amazon Cognito | User management | $0–$10 | First 10k users free |
| CloudWatch + CloudTrail | Monitoring and logging | $1–$10 | Depends on log volume |
| Backups | Snapshots and versioning | $1–$10 | Weekly auto-backups recommended |

**Estimated total:** $30–$160/month (≈ $90–$480 for 3 months)

---

### **Cost Optimization Tips**

1. Use AWS Free Tier for Lightsail, S3, CloudFront, and Cognito.  
2. Deploy in ap-southeast-1 (Singapore) for minimal latency.  
3. Apply S3 Lifecycle Policies to move old files to Glacier Deep Archive.  
4. Enable billing alerts with AWS Cost Explorer and Budgets.  
5. Schedule weekly snapshots and enable MFA Delete on S3.  

---

## **7. Risk Assessment**

| **Risk ID** | **Description** | **Severity** | **Impact** |
|--------------|----------------|--------------|-------------|
| R1 | Lightsail instance failure | Medium | Temporary downtime |
| R2 | Database corruption | High | Loss of transactional data |
| R3 | Credential leakage | Medium | Unauthorized access risk |
| R4 | Traffic surge overload | Medium | Slow or unresponsive website |

---

### **7.1 Mitigation Strategies**

- R1: Daily Lightsail snapshots and detailed recovery procedures.  
- R2: Automated DB backups exported to S3 for redundancy.  
- R3: Secrets Manager enforced with key rotation.  
- R4: Optimize CloudFront caching and scale Lightsail when traffic spikes.  

---

### **7.2 Contingency Plan**

- System Recovery: Restore instance from latest snapshot within 4 hours.  
- Data Restoration: Recover MySQL backups stored in S3.  
- Continuity: Serve a maintenance page via S3 + CloudFront during downtime.  
- Security Incident: Rotate keys and investigate with CloudTrail logs.  

---

### **7.3 Risk Monitoring Plan**

- Operational Monitoring: CloudWatch alarms for CPU/network thresholds.  
- Security Review: Weekly CloudTrail audits for unusual API activities.  
- Quarterly Risk Review: Reassess risk matrix after major updates.  

---

## **8. Expected Outcomes**

### **8.1 Success Metrics (KPIs)**

**Technical KPIs**
- Frontend latency < 200ms (via CloudFront)  
- API response < 350ms (via API Gateway + Lightsail)  
- 99.9% uptime with automated recovery  
- 70%+ requests served from CDN cache  
- Zero major security incidents (Cognito + WAF)  
- RTO < 30 minutes, RPO = 0 for data protection  

**Business KPIs**
- 20–30% increase in conversions  
- 15–25% customer retention improvement  
- 25–40% infrastructure cost reduction  
- Lower transaction costs aligned with AWS value efficiency  

---

### **8.2 Short-Term Benefits (0–6 Months)**

- 40–70% faster page load, lower bounce rate  
- Reduced backend load with CDN caching  
- Stronger authentication via Cognito  
- Automated alerts and backups with CloudWatch  
- Faster feature deployment thanks to decoupled architecture  

---

### **8.3 Mid-Term Benefits (6–18 Months)**

- Lower storage cost via S3 → Glacier lifecycle  
- Stable API under high traffic  
- Cost forecasting through AWS Cost Explorer  
- Continuous performance tuning with CloudWatch dashboards  
- Reduced maintenance workload for developers  

---

### **8.4 Long-Term Value (18+ Months)**

- Fully scalable cloud-native platform, ready for mobile or marketplace expansion  
- AI/ML readiness for personalized jewelry recommendations  
- 80–90% storage cost reduction via Glacier archiving  
- Enterprise-grade security and compliance (IAM, WAF, CloudTrail)  
- Global reach with CloudFront Edge Network  
- Sustainable, resilient operations for long-term growth  

---

### **8.5 User Experience Enhancements**

- Faster image loading and product browsing  
- Smooth login and order tracking via Cognito  
- Reduced lag and downtime during peak hours  
- Increased customer trust through AWS-grade reliability  

---

### **8.6 Strategic Capabilities Gained**

- Cloud-native architecture, ready for microservices evolution  
- FinOps maturity with detailed cost tracking  
- Operational excellence via centralized monitoring and auditing  
- Future-ready infrastructure expandable to ECS, EKS, or RDS  
- High-level security compliance using IAM, Cognito, WAF, Secrets Manager  
- Solid foundation for data analytics and AI integration