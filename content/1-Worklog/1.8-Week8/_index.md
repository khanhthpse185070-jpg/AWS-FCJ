---
title: "Week 8 Worklog"
 
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 8 Objectives:

* Automate infrastructure deployment using CloudFormation.
* Implement comprehensive CloudWatch monitoring.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Learn about CloudWatch Metrics, Logs, Alarms.                                                                                                   | 25/10/2025 | 26/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Set up CloudWatch Dashboard and Alarms for key services.                                              | 26/10/2025 | 27/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Learn about AWS CloudFormation and Template structure. | 27/10/2025 | 28/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Write a CloudFormation Template to deploy an EC2 Instance.                            | 28/10/2025 | 29/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Write a CloudFormation Template for VPC and use Parameters/Outputs.                                                                                    | 29/10/2025 | 30/10/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 8 Achievements:

* Infrastructure Automation: Demonstrated proficiency in Infrastructure as Code (IaC) by authoring complex AWS CloudFormation (CFN) templates:

  * Created a stack that successfully provisioned an entire networking environment (VPC, Subnets, IGW, etc.).

* Template Reusability: Applied best practices to make CFN templates dynamic:

  * Used Parameters to accept custom input values.

  * Used Outputs to allow stacks to export data for use by other dependent stacks.

* Advanced Observability: Implemented a robust monitoring solution using Amazon CloudWatch:

  * Set up custom metrics and centralized log groups for application logs (CloudWatch Logs).

  * Defined Alarms with specific notification actions (via SNS) for critical system events.
