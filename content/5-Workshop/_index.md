---
title: "Workshop"
 
weight: 5
chapter: false
pre: " <b> 5. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# AWS Jewelry Web Workshop

![Architecture](/images/imageworkshop.png)
<p align="center"><em>Figure: Simplified AWS Jewelry Web architecture (CloudFront + S3, Lightsail API/DB, Cognito, Secrets, CloudWatch).</em></p>

#### Overview

This workshop documents the AWS Jewelry Web project: a secure, cost-aware jewelry e-commerce stack using AWS managed services.

- **Frontend**: React SPA on **S3 + CloudFront** with ACM TLS and Route 53 domain.
- **Backend**: **Lightsail** instance running Node.js API; **Lightsail MySQL/Postgres** for data.
- **Identity**: **Amazon Cognito** User Pool for signup/login and JWT verification on the API.
- **Media**: Private **S3** bucket for product images; uploads via **presigned PUT**; CloudFront reads objects.
- **Secrets & Observability**: **AWS Secrets Manager** for DB password and bucket config; **CloudWatch Logs** for API/business events.

Design goals:

- Page load <2s globally via CloudFront.
- Stable API under expected traffic (<100k req/month).
- Secure DB operations; no hardcoded secrets (Secrets Manager only).
- Secure uploads; complete API logging for operations and basic analytics.

#### Content Map

**[5.1. Objectives & Scope](5.1-objectives--scope/)**  
**[5.2. Architecture Walkthrough](5.2-architecture-walkthrough/)**  
**[5.3. Implementing Clickstream Ingestion](5.3-implementing-clickstream-ingestion/)**  
**[5.4. Building the Private Analytics Layer](5.4-building-private-analytics-layer/)**  
**[5.5. Visualizing Analytics with Shiny Dashboards](5.5-visualizing-analytics-with-shiny-dashboards/)**  
**[5.6. Summary & Clean up](5.6-summary-cleanup/)**