---
title: "Blog 4"
 
weight: 1
chapter: false
pre: " <b> 3.4. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# Architecting for AI excellence: AWS launches three Well-Architected Lenses at re:Invent 2025

by Anitha Selvan and Arvind Raghunathan on 19 NOV 2025 in Amazon Machine Learning, Announcements, Artificial Intelligence, AWS Well-Architected, Generative AI |Permalink | Comments | Share

At re:Invent 2025, we introduce one new lens and two significant updates to the AWS Well-Architected Lenses specifically focused on AI workloads: the Responsible AI Lens, the Machine Learning (ML) Lens, and the Generative AI Lens. Together, these lenses provide comprehensive guidance for organizations at different stages of their AI journey, whether you’re just starting to experiment with machine learning or already deploying complex AI applications at scale.

The AWS Well-Architected Framework provides the best architectural practices for designing and operating reliable, secure, performance efficient, cost-optimized, and sustainable workloads in the cloud.

## The Responsible AI Lens: Embedding trust in AI systems
The Responsible AI Lens offers a structured approach for developers to assess and track their AI workloads against established best practices, identify potential gaps in their AI implementation and receive actionable guidance to improve their AI systems’ quality and alignment with responsible AI principles. By using the Responsible AI Lens you can make informed decisions that balance business and technical requirements, accelerating your path from AI experimentation to production-ready solutions.

Key takeaways from the Responsible AI Lens:

  * Every AI system has a Responsible AI consideration: Whether intentionally designed or not, AI systems inherently carry Responsible AI implications that need to be actively managed rather than left to chance.
  * AI systems can be used beyond original intent and may have unintended impacts: Applications often get utilized in ways developers didn’t anticipate, and due to their probabilistic nature, AI systems can produce unexpected outcomes even within intended use cases, making robust Responsible AI decisions essential from the start.
  * Responsible AI is an enabler to innovation and trust: Rather than being a constraint, Responsible AI practices can accelerate innovation by proactively building stakeholder and customer trust and reducing downstream risks.

The Responsible AI Lens serves as the foundational guidance for AI development activities, providing critical guidelines that inform both the Machine Learning Lens and the Generative AI Lens implementations.

## The Machine Learning Lens: Foundation for ML workloads
The Machine Learning Lens provides you with a set of established cloud-agnostic best practices in the form of Well-Architected Framework pillars for each machine learning (ML) lifecycle phase. The updated Machine Learning Lens provides a consistent approach for designing, building, and operating machine learning workloads on AWS. It addresses the full spectrum of ML workloads, from traditional supervised and unsupervised learning to modern AI applications.

The updated Machine Learning Lens incorporates the latest AWS ML capabilities (evolved since their introduction in 2023). What’s new in the updated ML Lens:

  * Enhanced data and AI collaborative workflows through Amazon SageMaker Unified Studio.
  * AI-assisted development for code generation and productivity enhancement.
  * Distributed training infrastructure for foundation model development and fine-tuning with Amazon SageMaker HyperPod.
  * Model customization capabilities such as knowledge distillation and fine-tuning domain-specific applications using Amazon Bedrock with Kiro and Amazon Q Developer.
  * No-code ML development using Amazon SageMaker Canvas with Amazon Q integration.
  * Improved bias detection with enhanced fairness metrics and Responsible AI capabilities in Amazon SageMaker Clarify.
  * Automated dashboard creation for business insights through Amazon Quick Sight.
  * Modular inference architecture for flexible model deployment with Inference Components.
  * Advanced observability with improved debugging and monitoring capabilities across the ML lifecycle.
  * Enhanced cost optimization for resource management through Amazon SageMaker Training Plans, Savings Plans, and Spot Instance support.

You can use the ML Lens wherever you are on your cloud journey. You can choose to apply this guidance either during the design of your ML workloads or after your workloads have entered production as part of the continuous improvement process. These improvements are powered by key AWS services including Amazon SageMaker Unified Studio, Amazon Q, Amazon SageMaker HyperPod, and Amazon Bedrock.

## The Generative AI Lens: Specialized guidance for foundation models
The Generative AI Lens provides a consistent approach for customers to evaluate architectures that use large language models (LLMs) to achieve their business goals. This lens addresses common considerations relevant to model selection, prompt engineering, model customization, workload integration, and continuous improvement. We identify best practices that help you architect your cloud-based applications and workloads according to AWS Well-Architected design principles gathered from supporting thousands of customer implementations. While the Machine Learning (ML) Lens covers the broad spectrum of ML workloads, the Generative AI Lens focuses specifically on foundation models and generative AI applications. The Generative AI Lens provides the best architectural practices for designing and operating generative AI workloads on AWS.

The updated Generative AI Lens includes several new additions:

  * Amazon SageMaker HyperPod guidance for orchestrating complex, long-running generative AI workflows that includes additional service capabilities.
  * Enhanced Responsible AI preamble with detailed discussion on the eight core dimensions of Responsible AI as described by AWS.
  * Updated data architecture preamble with strategic considerations needed to architect a data system for generative AI workloads.
  * New agentic AI preamble introducing architecture paradigms for agentic systems.
  * Eight architecture scenarios covering common generative AI-powered business applications such as autonomous call centers, knowledge worker co-pilots, and multi-tenant generative AI service systems.

The Generative AI Lens builds upon the foundation established by the ML Lens, providing specialized guidance for the unique challenges and opportunities presented by foundation models and generative AI applications.

## Implementation strategy for Well-Architected AI/ML guidance: A unified approach
The new lenses – Responsible AI Lens, Machine Learning Lens, and Generative AI Lens – work together to provide comprehensive guidance for AI development. The Responsible AI Lens guides safe, fair, and secure AI development. It helps balance business needs with technical requirements, streamlining the transition from experimentation to production. The Machine Learning Lens guides organizations in evaluating workloads across both modern AI and traditional machine learning approaches. Recent updates focus on key areas including enhanced data and AI collaborative workflows, AI-assisted development capabilities, large-scale infrastructure provisioning, and customizable model deployment. The Generative AI Lens helps customers evaluate large language model (LLM) based architectures and its updates include guidance for Amazon SageMaker HyperPod users, new insights on agentic AI, and updated architectural scenarios.

## What are the next steps?
The launch of these new lenses at re:Invent 2025 helps organizations build AI systems that are responsible, trustworthy, powerful, and effective. By providing comprehensive guidance across the full spectrum of AI workloads, AWS supports organizations to accelerate their AI initiatives while maintaining the highest standards of responsible AI and technical excellence.

Learn more about the AWS Well-Architected Framework and implement the best practice guidance provided using the GitHub repository. These lenses are practical tools designed to help you build AI systems that deliver real business value while maintaining the highest standards of ethics, security, and operational excellence.

For additional reading, refer to the AWS Well-Architected Framework and pillar whitepapers, or contact your AWS Solutions Architect or Account Representative for support on implementing these lenses in your organization.

## About the authors
![picture 1](/images/image3.4.1.png)
Anitha Selvan is a Go-To-Market Lead for the Cloud Optimization organization at AWS. With over 8 years of experience in product marketing and orchestrating go-to-market strategies across AWS support products, she now focuses on helping organizations accelerate their cloud transformation and AI adoption journeys. Anitha specializes in product launches and go-to-market strategy, combining tactical execution with expertise in architectural best practices and organizational change management to drive product adoption and customer engagements

![picture 2](/images/image1.png)
Arvind Raghunathan is a Principal Operations Specialist at AWS and is passionate about helping customers in different phases of their cloud journey with a specialty in cloud operations and optimization. He loves yoga, meditation, trying his skills cooking vegetarian dishes and following international cricket