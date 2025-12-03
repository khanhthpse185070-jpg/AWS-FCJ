---
title: "Week 7 Worklog"
 
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 7 Objectives:

* Containerize an application, deploy it on ECS Fargate
* Utilize decoupled messaging services (SNS/SQS)

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Master Docker, write a Dockerfile, and push the Image to ECR.                                                                                                   | 20/10/2025 | 21/10/2025      |<https://cloudjourney.awsstudygroup.com/> |
| 3   | - Deploy ECS Cluster and Task Definition (Fargate Launch Type).                                              | 21/10/2025 | 22/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Create an ECS Service and integrate it with the ALB. | 20/10/2025 | 22/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Configure SNS (Simple Notification Service) and SQS (Simple Queue Service).                           | 23/10/2025 | 24/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Deploy an application using ECS/Fargate.                                                                                     | 23/10/2025 | 24/10/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 7 Achievements:

* Container Workflow Mastery: Developed a working Dockerfile, built a custom application image, and managed the container lifecycle:

  * Pushed the application image to a private Amazon Elastic Container Registry (ECR) repository.

* Serverless Container Deployment: Successfully deployed the containerized application using AWS ECS Fargate:

  * Eliminated the need to manage underlying EC2 worker nodes.

  * Ingrated the ECS Service with the ALB.

* Asynchronous Communication: Implemented a critical component of a microservices architecture:

  * Configured and utilized SQS (Simple Queue Service) for decoupling application components.

  * Used SNS (Simple Notification Service) for fan-out messaging to multiple subscribers.
