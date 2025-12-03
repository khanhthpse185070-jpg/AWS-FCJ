---
title: "Event 1"
 
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy it verbatim** into your report, including this warning.
{{% /notice %}}

# Summary Report: “AWS Well-Architected Security Pillar”

### Event Objectives

- Share best practices based on the **AWS Well-Architected Framework (Security Pillar)**.

- Deep dive into the **Shared Responsibility Model** and core principles like **Zero Trust** and **Least Privilege**.

- Provide technical guidance on modernizing **Identity & Access Management (IAM)**.

- Demonstrate strategies for **Detection, Data Protection**, and **Incident Response (IR)** automation.

### Speakers

- **Nguyen Tuan Thinh** – Cloud Engineer Trainee
- **Tran Duc Anh** – Cloud Security Engineer Trainee
- **Nguyen Do Thanh Dat** – Cloud Engineer Trainee
- **Kha Van** - Community Leader AWS

### Key Highlights

#### Security Foundation & Core Principles
- **Shared Responsibility Model**: Clarifying the line between security of the cloud (AWS) and security in the cloud (Customer).

- **Core Principles**:

    * **Least Privilege**: Granting only necessary permissions.

    * **Zero Trust**: "Never trust, always verify" — inside and outside the network.

    * **Defense in Depth**: Layered security controls.

- **Context**: Analysis of top cyber threats specifically within the Vietnam cloud environment.

#### Pillar 1: Identity & Access Management (IAM)
- **Modern IAM Architecture**:

    * Shift from long-term credentials (access keys) to temporary credentials (Roles).

    * **IAM Identity Center**: Implementing SSO (Single Sign-On) for centralized access.

- **Multi-Account Strategy**: Using **SCPs (Service Control Policies)** and permission boundaries to manage permissions at the Organization level.

- **Credential Hygiene**: Enforcing MFA, regular credential rotation, and using **Access Analyzer**.

#### Pillar 2: Detection & Monitoring
- **Continuous Monitoring**:

    * **CloudTrail**: Auditing API calls at the organization level.

    * **GuardDuty**: Intelligent threat detection.

    * **Security Hub**: Centralized security posture management.

- **Logging**: Implementing logging at all layers (VPC Flow Logs, ALB Logs, S3 Access Logs).

- **Detection-as-Code**: Automating alerting via EventBridge.

#### Pillar 3 & 4: Infrastructure & Data Protection
- **Network Security**:

    * VPC segmentation and distinguishing between **Security Groups** (stateful) and **NACLs** (stateless).

    * Perimeter protection using WAF, Shield, and Network Firewall.

- **Data Encryption**:

    * **KMS (Key Management Service)**: Managing key policies and rotation.

    * Encryption At-rest (S3, EBS, RDS) and In-transit (TLS).

- **Secrets Management**: Replacing hard-coded passwords with Secrets Manager or Parameter Store.

#### Pillar 5: Incident Response (IR)
- **IR Lifecycle**: Preparation, Detection, Containment, Eradication, Recovery, Post-Incident Activity.

- **Playbooks**: Specific guides for scenarios like:

    * Compromised IAM keys.

    * S3 public data exposure.

    * EC2 malware infection.

- **Automation**: Using Lambda and Step Functions to auto-remediate simple threats (e.g., isolating an instance).
 

### Key Takeaways

#### Design Mindset

- **Identity is the New Perimeter**: Focus heavily on IAM as the primary control point, not just network firewalls.  
- **Automate Security**: Move away from manual checks to "Security as Code" using tools like CloudFormation and EventBridge.
- **Assume Breach**: Design systems assuming an attack will happen, focusing on minimizing blast radius (segmentation).

#### Technical Architecture

- **Centralized Logging**: Logs from VPC, S3, and Applications must be centralized and immutable for effective forensics
- **Encryption by Default**: Enable encryption for all storage services (EBS, S3, RDS) immediately upon creation
- **Account Segmentation**: Use separate AWS accounts for production, development, and logging (log Archive) to limit the impact of a breach  

#### Modernization Strategy

- **Phased Implementation**: Start with basics (MFA, CloudTrail) before moving to advanced automation (Auto-remediation).

- **Regular Game Days**: Practice IR Playbooks regularly to ensure the team knows how to react during a real "Compromised Key" event.

- **Learning Roadmap**: Pursue AWS Certified Security – Specialty to deepen knowledge.

### Applying to Work

- **Audit IAM Policies**: Review current users/roles to remove long-term access keys and enforce MFA.

- **Enable GuardDuty**: Turn on GuardDuty in all regions to start detecting threats immediately.

- **Refactor Secrets**: Scan code for hard-coded credentials and move them to AWS Secrets Manager.

- **Develop IR Playbooks**: Write and test a specific procedure for "S3 Public Bucket" and "Compromised IAM Credential" scenarios.

- **Implement SCPs**: If using AWS Organizations, apply Service Control Policies to prevent root account usage or disabling of CloudTrail. 

### Event Experience

Attending the **“AWS Well-Architected Security Pilar”** session was highly effective, providing a structured approach to cloud security rather than just a list of tools. Key experiences included:

#### Learning from highly skilled speakers
- The breakdown of the **Shared Responsibility Model** clarified exactly what the development team needs to own versus what AWS handles.

- Understanding the specific threat landscape in **Vietnam** helped prioritize which security controls to implement first. 

#### Hands-on technical exposure
- **Mini Demo (IAM)**: The demonstration of validating IAM Policies and simulating access was incredibly practical for debugging permission errors without risking production security.

- **IR Simulation**: visualizing the workflow of detecting an EC2 malware infection -> taking a snapshot -> isolating the instance was a highlight.

#### Leveraging modern tools
- Saw the power of **Access Analyzer** in identifying unintended public access.

- Learned how **EventBridge** can turn a passive log into an active alert or remediation action. 

#### Networking and discussions
- The Q&A session on "Common pitfalls in Vietnamese enterprises" provided realistic warnings about configuring Security Groups and S3 permissions incorrectly.

#### Lessons learned
- Security is not a blocker but an enabler when "Detection-as-Code" is implemented.

- Effective Incident Response relies heavily on preparation (Playbooks) and automation; trying to figure out what to do during an attack is too late.
#### Some event photos
*Add your event photos here*  

> Overall, the event not only provided technical knowledge but also helped me reshape my thinking about application design, system modernization, and cross-team collaboration.
