---
title: "Event 2"
 
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy it verbatim** into your report, including this warning.
{{% /notice %}}

# Summary Report: “DevOps on AWS”

### Event Objectives

- Share best practices on building a **DevOps Culture** and automating the software development lifecycle.

- Deep dive into the **AWS Native Toolchain** to build complete CI/CD Pipelines.

- Provide technical guidance on transitioning from manual operations ("ClickOps") to **Infrastructure as Code (IaC)**.

- Demonstrate strategies for application modernization using Containers and establishing full-stack **Observability**.

### Speakers
| Speaker Name | Title | Organization |
| :--- | :--- | :--- |
| **Nguyen Tuan Huy** | Director of Digital Transformation | Mobifone |
| **Minh Hoang** | Chief Data Officer | Techcom Securities |
| **Vincent Nguyen** | Managing Director | Nam Long Commercial Property |
| **Seunghoon Chae** | General Director | MegazoneCloud Vietnam |
| **Uy Tran** | Co-Founder & COO | Katalon |
| **Thai Huy Chuong** | Head of Application Development | Bao Viet Holdings |
| **Tran Dinh Khiem** | Digital Bank Director | Techcombank |
| **Christopher Bennett** | Chief Technology Officer | TymeX |
| **Selma Belhadjamor** | Principal Data Scientist | Onebyzero |
| **Ngo Manh Ha** | Co-CEO, CTO | TechX Corp |
| **Nguyen Thanh Binh** | Head of DevOps | Renova Cloud 

### Key Highlights

#### DevOps Mindset & Culture

- Core Mindset: DevOps is not a role, but a combination of Culture, Tools, and Processes.

- Key Metrics (DORA): Focusing on the 4 gold standards to measure performance:

    * Deployment Frequency.

    * Lead Time for Changes.

    * Mean Time to Recovery (MTTR).

    * Change Failure Rate.

#### Pillar 1: Pipeline Automation (CI/CD)

- AWS Standard Workflow:

    * CodeCommit: Centralized source control (Git-based).

    * CodeBuild & CodeTest: Automating compilation and running Unit Tests/SAST.

    * CodeDeploy: Automating code deployment to infrastructure.

- Deployment Strategies:

    * Blue/Green: Instant traffic shifting between old and new environments, ensuring Zero-downtime.

    * Canary: Gradual traffic distribution (10% -> 50%) to minimize risk.

- Demo: Setting up a full pipeline with a Manual Approval gate before Production release.

#### Pillar 2: Infrastructure as Code (IaC)

- Combating "ClickOps": Eliminating manual configuration on the Console to avoid errors and configuration drift.

- IaC Tools:

    * CloudFormation: The foundational platform using JSON/YAML templates.

    * AWS CDK (Cloud Development Kit): The modern trend allowing infrastructure definition via programming languages (TypeScript, Python) with highly reusable Constructs.

- Drift Detection: Techniques to detect deviations between actual infrastructure and IaC code.

#### Pillar 3: Container & Serverless Infrastructure

- Compute Selection:

    * Amazon ECS: Simple, deeply integrated, suitable for teams focusing purely on applications.

    * Amazon EKS: For systems requiring standard Kubernetes extensibility and high customization.

    * AWS App Runner: A fully managed solution, requiring no server or orchestrator management.

- Image Management: Using Amazon ECR with automated vulnerability scanning.
 
#### Pillar 4: Monitoring & Observability

- Comprehensive Monitoring:

    * CloudWatch: Collecting Metrics, Logs, and setting intelligent Alarms.

    * AWS X-Ray: Distributed Tracing to map services and find latency bottlenecks in Microservices architectures.

- Dashboards: Building centralized dashboards for both Dev and Ops teams.

### Key Takeaways

#### Design Mindset

- Fail Fast: Integrate automated testing directly into the Build phase to catch errors as early as possible.

- Shift Left: Move security and testing to the beginning of the development process, rather than waiting for deployment.

- Infrastructure is Software: Manage infrastructure versions exactly like application source code (Version Control).

#### Technical Architecture

- Immutable Infrastructure: Never patch running servers; replace them with entirely new servers/containers.

- Git Strategies: Use Trunk-based Development for high-velocity projects instead of overly complex GitFlow processes.

#### Modernization Strategy

- Container First: Prioritize packaging applications into Docker containers to ensure consistency across environments (Dev/Test/Prod).

- Platform Engineering: Build a Self-service platform so Developers can deploy without waiting for Ops.

### Applying to Work

- Adopt CDK: Start migrating new infrastructure projects to AWS CDK (TypeScript) for better maintainability.

- Automate Rollback: Configure CloudWatch Alarms to automatically trigger a Rollback in CodeDeploy if HTTP 5xx error rates spike.

- Enable X-Ray: Activate tracing for Lambda functions and ECS services to debug performance issues.

- Audit Pipelines: Add a Static Security Scan step to the current pipeline.  

### Event Experience

Event Experience Attending the "DevOps on AWS" workshop provided a comprehensive view of modern development processes. Key experiences included:

#### Learning from highly skilled speakers
- The debate on GitFlow vs. Trunk-based clarified the pros and cons of each source control strategy.

- Understanding how AWS operates internally reinforced the belief in the "You build it, you run it" culture.

#### Hands-on technical exposure
- Blue/Green Demo: Witnessing smooth traffic switching between two application versions without service interruption was the clearest proof of DevOps value.

- IaC Simulation: Seeing the convenience of CDK, where just a few lines of TypeScript code could provision an entire VPC and Cluster.

#### Leveraging modern tools
- Impressed by App Runner for its ability to deploy extremely fast from source code without writing complex Dockerfiles.

- Saw the power of X-Ray in visualizing calls between microservices.  

#### Networking and discussions
-  The coffee break discussions were valuable, particularly the debate on "Jenkins vs. AWS CodePipeline". Many peers shared their fatigue with managing self-hosted Jenkins servers and expressed interest in migrating to managed services to reduce operational overhead.

- Exchanged contacts with engineers from a fintech startup who shared their war stories about "Alert Fatigue" and how they tuned CloudWatch to reduce noise.

#### Lessons learned
- Automation is not just a tool, but a way to liberate humans from boring repetitive tasks.

- Observability is mandatory for Microservices; without Tracing, debugging is like "finding a needle in a haystack."
#### Some event photos
![Your profile picture](/images/event2.png) 

> Overall, the event not only provided technical knowledge but also helped me reshape my thinking about application design, system modernization, and cross-team collaboration.
