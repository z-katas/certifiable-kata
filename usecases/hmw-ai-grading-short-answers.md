# Grading short answers

## Use Case & Problem Statement
- **Primary Goals:** HMW implement AI-driven grading models for expert architects so that they can evaluate short-answer submissions 4X faster?
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
### Context Diagram (C1)
- **Description:**
- **Diagram:**

### Container Diagram (C2)
- **Description:**
- **Diagram:**

## Constraints
- **Technical Constraints:**
- **Operational Constraints:**
- **Security & Compliance Constraints:**

## Architectural Decision Records (ADRs)
- **ADR 1 - Title:**
  - **Context:**
  - **Decision:**
  - **Consequences:**

- **ADR 2 - Title:**
  - **Context:**
  - **Decision:**
  - **Consequences:**

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
