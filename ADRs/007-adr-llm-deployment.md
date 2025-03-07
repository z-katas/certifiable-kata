# ADR-007: LLM Deployment Model Decision

Date: [2025-02-13]

## Status

Accepted

## Context

We need to select the appropriate deployment model for integrating Large Language Models (LLMs) into the platform, which focuses on test submissions, adding new questionere. The deployment model must balance performance, cost, data privacy, and compliance with various regulatory bodies. Additionally, it should ensure scalability and maintain high standards of data security, given the sensitive nature of candidate information.

### Alternatives

1. **Cloud-based Deployment**: Use managed LLM services from providers like OpenAI, AWS, or Azure to host the model in the cloud.
2. **On-premises Deployment**: Deploy the LLM on private infrastructure to retain complete control over data and ensure compliance with internal privacy policies.
3. **Hybrid Deployment**: Combine cloud-based services for general LLM operations with on-premises solutions for sensitive tasks requiring higher levels of privacy and control.

### PrOACT

**Problem**: Select the best deployment model to integrate LLMs into the platform that aligns with privacy, scalability, cost-effectiveness, and accuracy  requirements.

**Objectives**:

- Ensure high data privacy and security for candidate information.
- Minimize operational costs and infrastructure complexity.
- Allow scalability to handle variable query volumes.
- Ensure compliance with GDPR/DPDP standards and reduce bias in AI-generated outcomes.

## Decision

We will adopt a **Hybrid Deployment Model** . Sensitive candidate information, such as anonymized personal details, will be processed on-premises to maintain privacy, while less sensitive tasks (such as general NLP queries and resume writing assistance) will be handled in the cloud using managed LLM services. This approach ensures compliance with data security standards while leveraging the scalability and cost-efficiency of cloud-based LLMs.

We can start with serverless architecture in the begining and evolve to a dedicated service which wraps around LLM models. This can also leverage the use of AI agents to orchestrate between different LLM models

## Tradeoffs - Mitigations

- **Complexity**: The hybrid model introduces complexity in managing both on-premises and cloud-based systems. We will mitigate this by using automated workflows and clear data segregation policies to ensure tasks are routed correctly.
- **Cost**: On-premises deployment may increase operational costs due to infrastructure maintenance. However, we will offset these costs by limiting on-premises operations to sensitive data only, reducing the need for large-scale infrastructure.
- **Data Privacy**: While cloud-based services may raise privacy concerns, we mitigate this by processing sensitive data on-premises and ensuring that no identifiable information is exposed to cloud-based systems.
- **Scalability**: The hybrid model allows us to handle high query volumes efficiently by using cloud resources for non-sensitive tasks. We will monitor usage patterns and adjust scaling policies as needed to maintain cost-efficiency and performance.