# Monitor software architecture trends

## Use Case & Problem Statement
- **Primary Goals:** HMW monitor software architecture trends for expert architects so that certification content stays aligned with evolving industry standards?
- **Scope:**
- **Current Challenges:**
- **Limitations of Existing System:**
- **Impact of Identified Issues:**

## Assumptions
- **Business Assumptions:**
- **Technical Assumptions:**
- **Regulatory & Compliance Considerations:**

## New User Journey / Golden Path
- **Job To Be Done (JTBD):**
- **High-Level User Flow:**
- **Key Steps in the Process:**
- **Expected Outcomes:**

## Architecture Diagrams
### Container Diagram (C2)
- **Description:** Containers and interactions
- **Diagram:**
![test 1 and test 2 content updates](/assets/new-questions-c2.png "test 1 and test 2 content updates")
### Flow Diagram
- **Description:** Flow involving chunking of documents, storing in vector store and retrieival by the expert Architect to update the tests
- **Diagram:**
![test 1 and test 2 content updates](/assets/New-test1-and-test2-questions.png "test 1 and test 2 content updates")

## Constraints
- **Technical Constraints:** 
- **Operational Constraints:** 
- **Security & Compliance Constraints:**

## Architectural Decision Records (ADRs)
- [**ADR 1 - Architecture documents chunking strategy**](/ADRs/architecture-knowledge-chunking-strategy.md)

- **ADR 2 - Title:**

## Implementation Details

### **Gen AI Technical Components & Architecture**
- **Local Inference & Cloud Services:**
  - Hybrid architecture utilizing **on-prem inference** for sensitive data and **cloud-based LLMs** for scalability.
- **Fine-Tuning & Adaptation:**
  - Custom-trained models leveraging **domain-specific fine-tuning** to improve grading and feedback accuracy.
- **LLM Inference & Structured Outputs:**
  - Implementation of **structured response generation** for candidate feedback and grading justifications.
- **Prompt Engineering & Validation:**
  - **Dynamic prompt orchestration** for AI models ensuring contextual accuracy.
  - **Guardrails & validation mechanisms** to filter out misleading or biased responses.
- **Information Retrieval & Search Engine:**
  - **Vector-based search** using embeddings to improve knowledge retrieval for candidate responses.
  - **Ranking models** to ensure relevant test question mapping.
- **Observability & Performance Monitoring:**
  - **Prompt & model evaluation pipelines** for continuous improvement.
  - **LLM observability tools** to track model behavior and response drift.
  - **Conversation analytics** for monitoring candidate interactions with AI-driven systems.
- **Agent-Based Automation:**
  - AI-driven **autonomous agents** to review test patterns and optimize grading workflows.
  - **Adaptive AI agents** capable of iterating on responses based on real-time evaluation.

## Conclusion
- **Summary of Changes:** AI-driven automation for grading, feedback, and certification content updates.
- **Benefits of the New Architecture:** Increased scalability, faster turnaround, and reduced manual workload.
- **Potential Risks & Mitigations:** AI bias monitoring, human oversight mechanisms, and periodic model retraining.
- **Next Steps:** Pilot AI grading system, evaluate AI explainability, and refine model accuracy based on real-world data.
