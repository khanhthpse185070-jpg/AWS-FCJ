---
title: "Blog 1"
 
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# Build a scalable AI assistant to help refugees using AWS

by Taras Tsarenko, Anton Garvanko, and Vitalii Bozadzhy, Vladyslav Horbatenko on 03 JUN 2025 in Amazon Bedrock, Amazon Machine Learning, Amazon Rekognition, Amazon Translate, Architecture, Artificial Intelligence, Customer Solutions | Permalink |  Comments | Share
This post is co-written with Taras Tsarenko, Vitalil Bozadzhy, and Vladyslav Horbatenko. 

As organizations worldwide seek to use AI for social impact, the Danish humanitarian organization Bevar Ukraine has developed a comprehensive virtual generative AI-powered assistant called Victor, aimed at addressing the pressing needs of Ukrainian refugees integrating into Danish society. This post details our technical implementation using AWS services to create a scalable, multilingual AI assistant system that provides automated assistance while maintaining data security and GDPR compliance.

Bevar Ukraine was established in 2014 and has been at the forefront of supporting Ukrainian refugees in Denmark since the full-scale war in 2022, providing assistance to over 30,000 Ukrainians with housing, job search, and integration services. The organization has also delivered more than 200 tons of humanitarian aid to Ukraine, including medical supplies, generators, and essential items for civilians affected by the war.


## Background and challenges

The integration of refugees into host countries presents multiple challenges, particularly in accessing public services and navigating complex legal procedures. Traditional support systems, relying heavily on human social workers, often face scalability limitations and language barriers. Bevar Ukraine’s solution addresses these challenges through an AI-powered system that operates continuously while maintaining high standards of service quality.

## Solution overview 

The solution’s backbone comprises several AWS services to deliver a reliable, secure, and efficient generative AI-powered digital assistant for Ukrainian refugees. The team consisting of three volunteer software developers developed the solution within weeks.

The following diagram illustrates the solution architecture.
![picture 1](/images/image3.1.1.png)

Amazon Elastic Compute Cloud (Amazon EC2) serves as the primary compute layer, using Spot Instances to optimize costs. Amazon Simple Storage Service (Amazon S3) provides secure storage for conversation logs and supporting documents, and Amazon Bedrock powers the core natural language processing capabilities. Bevar Ukraine uses Amazon DynamoDB for real-time data access and session management, providing low-latency responses even under high load.

In the process of implementation, we discovered that Anthropic’s Claude 3.5 large language model (LLM) is best suited due to its advanced dialogue logic and ability to maintain a human-like tone. It’s best for thorough, reasoned responses and generating more creative content, which makes Victor’s replies more natural and engaging.

Amazon Titan Embeddings G1 – Text v1.2 excels at producing high-quality vector representations of multilingual text, enabling efficient semantic search and similarity comparisons. This is particularly valuable when Victor needs to retrieve relevant information from a large knowledge base or match users’ queries to previously seen inputs. Amazon Titan Embeddings also integrates smoothly with AWS, simplifying tasks like indexing, search, and retrieval.

In real-world interactions with Victor, some queries require short, specific answers, whereas others need creative generation or contextual understanding. By combining Anthropic’s Claude 3.5. for generation and Amazon Titan Embeddings G1 for semantic retrieval, Victor can route each query through the most appropriate pipeline, retrieving relevant context through embeddings and generating a response, resulting in more accurate and context-aware answers.

Amazon Bedrock provides a remarkable interface to call Anthropic’s Claude 3.5 and Amazon Titan Embeddings G1 (along with other models) without creating separate integrations for each provider, simplifying development and maintenance.

For multilingual support, we used embedders that support multi-language embeddings and translated our materials using Amazon Translate. This enhances the resilience of our Retrieval Augmented Generation (RAG) system. The application is built securely and uses AWS services to accomplish this. AWS Key Management Service (AWS KMS) simplifies the process of encrypting data within the application, and Amazon API Gateway supports the applications REST endpoints. User authentication and authorization capabilities are supported by Amazon Cognito, which provides secure and scalable customer identity and access management (CIAM) capabilities.

The application runs on AWS infrastructure using services that are designed to be secure and scalable like Amazon S3, AWS Lambda, and DynamoDB.

## Tips and recommendations

Building an AI assistant solution for refugees using Amazon Bedrock and other AWS services has provided valuable insights into creating impactful AI-powered humanitarian solutions. Through this implementation, we discovered key considerations that organizations should keep in mind when developing similar solutions. The experience highlighted the importance of balancing technical capabilities with human-centric design, providing multilingual support, maintaining data privacy, and creating scalable yet cost-effective solutions. These learnings can serve as a foundation for organizations looking to use AI and cloud technologies to support humanitarian causes, particularly in creating accessible and helpful digital assistance for displaced populations. The following are the main.

  * Use the Amazon Bedrock playground to test multiple LLMs side by side using the same prompt. This helps you find the model that gives the best quality, style, and tone of response for your specific use case (for example, factual accuracy vs. conversational tone).
  * Experiment with prompts and settings to improve responses.
  * Keep costs in mind; set up monitoring and budgets in AWS.
  * For tasks involving information retrieval or semantic search, select an embedding model while making sure to pick the appropriate settings. Pay attention to the size of the embeddings, because larger vectors can capture more meaning but might increase costs. Also, check that the model supports the languages your application requires.
  * If you’re using a knowledge base, use the Amazon Bedrock knowledge base playground to experiment with how content is chunked and how many passages are retrieved for each query. Finding the right number of retrieved passages can make a big difference in how clear and focused the final answers are—sometimes fewer, high-quality chunks work better than sending too much context.
  * To enforce safety and privacy, use Amazon Bedrock Guardrails. Guardrails can help prevent the model from leaking sensitive information, such as personal data or internal business content, and you can block harmful responses or enforce a specific tone and formatting style.
  * Start with a simple prototype, test the embedding quality in your domain, and expand iteratively.

## Integration and enhancement layer

Bevar Ukraine has extended the core AWS infrastructure with several complementary technologies:

  * Pinecone vector database – For efficient storage and        retrieval of semantic embeddings
  * DSPy framework – For structured prompt engineering and optimization of Anthropic’s Claude 3.5 Sonnet responses
  * EasyWeek – For appointment scheduling and resource management
  * Telegram API – For UI delivery
  * Amazon Bedrock Guardrails – For security policy enforcement
  * Amazon Rekognition – For document verification
  * GitHub-based continuous integration and delivery (CI/CD) pipeline – For rapid feature deployment

## Key technical insigts

The implementation revealed several crucial technical considerations. The DSPy framework was crucial in optimizing and enhancing our language model prompts. By integrating additional layers of reasoning and context awareness tools, DSPy notably improved response accuracy, consistency, and depth. The team found that designing a robust knowledge base with comprehensive metadata was fundamental to the system’s effectiveness.

GDPR compliance required careful architectural decisions, including data minimization, secure storage, and clear user consent mechanisms. Cost optimization was achieved through strategic use of EC2 Spot Instances and implementation of API request throttling, resulting in significant operational savings without compromising performance.

## Future enhancements

Our roadmap includes several technical improvements to enhance the system’s capabilities:

  * Implementing advanced context dispatching using machine learning algorithms to improve service coordination across multiple domains
  * Developing a sophisticated human-in-the-loop validation system for complex cases requiring expert oversight
  * Migrating suitable components to a serverless architecture using Lambda to optimize resource utilization and costs
  * Enhancing the knowledge base with advanced semantic search capabilities and automated content updates

## Results

This solution, which serves hundreds of Ukrainian refugees in Denmark daily, demonstrates the potential of AWS services in creating scalable, secure, and efficient AI-powered systems for social impact. As a result, volunteers and employees of Bevar Ukraine have saved thousands of hours, and instead of answering repetitive questions from refugees, can support them in more complicated life situations. For refugees, the virtual assistant Victor is a lifeline support that allows users to get responses to the most pressing questions about public services in Denmark and many other questions in seconds instead of having to wait for an available volunteer to help. Given the vast knowledge base Victor is using to generate responses, the quality of support has improved as well.

## Conclusion

Through careful architecture design and integration of complementary technologies, we’ve created a platform that effectively addresses the challenges faced by refugees while maintaining high standards of security and data protection.

The success of this implementation provides a blueprint for similar solutions in other social service domains, potentially supporting refugees and other people in need around the world, highlighting the importance of combining robust cloud infrastructure with thoughtful system design to create meaningful social impact.

## About the Authors

![picture 2](/images/image3.1.2.png)

Taras Tsarenko is a Program Manager at Bevar Ukraine. For over a decade in the world of technology, Taras has led everything from tight-knit agile teams of 5 or more to a company of 90 people that became the best small IT company in Ukraine under 100 people in 2015. Taras is a builder who thrives at the intersection of strategy and execution, where technical expertise meets human impact, whether it’s streamlining workflows, solving complex problems, or empowering teams to create meaningful products. Taras specializes in AI-driven solutions and data engineering, leveraging technologies like machine learning and generative AI using Amazon SageMaker AI, Amazon Bedrock, Amazon OpenSearch Service, and more. Taras is an AWS Certified ML Engineer Associate.

![picture 3](/images/image3.1.3.png)

Anton Garvanko is a Senior Analytics Sales Specialist for Europe North at AWS. As a finance professional turned salesman, Anton spent 15 years in various finance leadership roles in supply chain and logistics as well as financial services industries. Anton joined Amazon over 5 years ago and has been part of specialist sales teams focusing on business intelligence, analytics, and generative AI for over 3 years. He is passionate about connecting the worlds of finance and IT by making sure that business intelligence and analytics powered by generative AI support everyday decision-making across industries and use cases.

![picture 4](/images/image3.1.4.png)

Vitalii Bozadzhy is a Senior Developer with extensive experience in building high-load, cloud-based solutions, specializing in Java, Golang, SWIFT, and Python. He specializes in scalable backend systems, microservice architectures designed to automate business processes, as well as building reliable and secure cloud infrastructures. Furthermore, he has experience in optimizing compute resources and building advanced solutions integrated into products. His expertise covers the full development cycle—from design and architecture to deployment and maintenance—with a strong focus on performance, fault tolerance, and innovation.

![picture 5](/images/image3.1.5.png)

Vladyslav Horbatenko is a computer science student, Professor Assistant, and Data Scientist with a strong focus on artificial intelligence. Vladyslav began his journey with machine learning, reinforcement learning, and deep learning, and gradually became more interested in large language models (LLMs) and their potential impact. This led him to deepen his understanding of LLMs, and now he works on developing, maintaining, and improving LLM-based solutions. He contributes to innovative projects while staying up to date with the latest advancements in AI.
