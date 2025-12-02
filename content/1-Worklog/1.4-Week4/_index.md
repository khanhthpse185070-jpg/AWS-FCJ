---
title: "Week 4 Worklog"
 
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 4 Objectives:

* Deploy and integrate relational (RDS) and No SQL (DynamoDB) databases securely.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Deploy Amazon RDS (MySQL/PostgreSQL) into a Private Subnet.                                                                                                   | 27/09/2025 | 29/09/2025      | <https://cloudjourney.awsstudygroup.com/>|
| 3   | - Configure Security Groups for secure EC2 to RDS connection.                                              | 28/09/2025 | 30/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Create and perform basic CRUD operations with DynamoDB Table (NoSQL). | 30/09/2025 | 01/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Understand ElastiCache (Redis/Memcached) and its use-cases.                            | 01/10/2025 | 02/10/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Deploy a simple ToDo List application (EC2 + RDS).                                                                                     | 02/10/2025 | 03/10/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 4 Achievements:

* Secure Relational Deployment: Successfully deployed a fully managed Amazon RDS instance:

    * Deployed the database into the Private Subnet, ensuring isolation.

    * Access was strictly controlled via a dedicated Security Group, only allowing connections from the EC2 Application Layer.

* NoSQL Proficiency: Mastered key differences between relational and NoSQL models:

    * Created a scalable DynamoDB table, optimized with Partition/Sort Keys.

    * Performed basic CRUD operations using both the AWS Console and the CLI/SDK.

* Performance Enhancement Fundamentals:

    * Acquired theoretical knowledge of in-memory caching services like Amazon ElastiCache (Redis/Memcached).

    * Understood its architectural role in reducing database load and improving application latency.


