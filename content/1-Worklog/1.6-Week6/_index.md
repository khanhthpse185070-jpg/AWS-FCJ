---
title: "Week 6 Worklog"
 
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 6 Objectives:

* Build basic serverless APIs with Lambda/API Gateway and utilize CDN (CLoudFront) for content delivery.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | -  Deploy a simple Web application on Lightsail.                                                                                                  | 12/10/2025 | 13/10/2025      |<https://cloudjourney.awsstudygroup.com/> |
| 3   | - Write a basic Lambda function and trigger it with an Event (S3/SNS).                                              | 13/10/2025 | 14/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Configure API Gateway (REST API) integrated with Lambda. | 14/10/2025 | 15/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Configure CloudFront to accelerate and protect an S3 Static Website.                            | 15/10/2025 | 16/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | -  Learn about Route 53 (Record Types, Routing Policies) and Lambda@Edge.                                                                                    | 16/10/2025 | 17/10/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 6 Achievements:

* Serverless API Creation: Successfully implemented a core Serverless API workflow:

  * Wrote and deployed an AWS Lambda function .

  * Integrated the function with API Gateway to create a publicly accessible REST endpoint.

* Decoupled Events: Demonstrated knowledge of event-driven architectures:

  * Configured Lambda functions to be triggered by various AWS event sources .

* Global Content Acceleration: Implemented and configured Amazon CloudFront as a Content Delivery Network (CDN):

  * Used CloudFront in front of an S3 origin, significantly improving asset delivery performance.

  * Provided basic DDoS protection at the edge layer.

* Domain Routing Expertise: Gained practical experience with Amazon Route 53:

  * Configured various record types (A, CNAME).

  * Experimented with advanced routing policies like Simple, Failover, or Latency-based Routing.
