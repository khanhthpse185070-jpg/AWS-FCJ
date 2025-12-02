---
title: "Week 5 Worklog"
 
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 5 Objectives:

* Implement a highly available, fault-tolerant, and auto-scaling architecture using ALB and ASG.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Configure Application Load Balancer (ALB) and Target Group.                                                                                                   | 05/10/2025 | 07/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Create Launch Template for EC2 and set up Auto Scaling Group (ASG).                                              | 06/10/2025 | 08/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Deploy HA/ASG Multi-AZ architecture attached to the ALB. | 06/10/2025 | 08/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Configure Scaling Policy based on CPU Utilization and perform Load Test.                            | 08/10/2025 | 09/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Complete a comprehensive Lab on Fault-Tolerant Web Application architecture.                                                                                    | 08/10/2025 | 10/10/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 5 Achievements:

* Fault-Tolerant Architecture: Designed and deployed a true High Availability (HA) architecture:

    * Successfully spanned the architecture across multiple Availability Zones for resilience.

* Advanced Load Balancing: Configured an Application Load Balancer (ALB):

    * Set up listeners (HTTP/HTTPS) and created Target Groups.

    * Implemented precise health check configurations to ensure traffic is only routed to healthy instances.

* Dynamic Scaling Implementation: Created a robust Auto Scaling Group (ASG) using a detailed Launch Template:

    * Implemented both Target Tracking Scaling Policies.

    * Successfully validated the automatic scale-out and scale-in events through intentional load testing.
