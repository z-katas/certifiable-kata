# Grading short answers

## Primary Goal

**HMW implement AI-driven grading models for expert architects so that they can evaluate short-answer submissions 4X faster?**

## Challenges in Expansion Plans

- The current **manual grading process** for Test 1 short-answer responses is **slow, expensive, and unscalable**.
- Each submission requires **3 hours** of expert evaluation, limiting grading capacity to **200 candidates per week**.
- With planned expansion to **2,000 candidates weekly**, grading workload would surge to **6,000 hours per week**, overwhelming available experts.
- The **$300K per week** cost of manual grading makes scaling financially unsustainable.
- Inconsistent grading across experts leads to **scoring variability and delays in feedback**, impacting candidate experience.

## Problem Statement & Scope

- The current manual grading process for Test 1 is unsustainable, requiring **3 hours per candidate**, making it infeasible to support the projected **5-10X growth in applicants**.
- This leads to excessive costs, grading delays, and inconsistencies due to expert workload limitations.
- **Generative AI** will automate grading while ensuring **scalability, accuracy, cost-effectiveness, and efficiency**, maintaining expert-level evaluation quality.
- **Cost-effectiveness** – AI-driven grading must be ** less than the current $300K per week manual grading budget**.
- **Productivity** – The solution must **improve grading efficiency by at least 4X** to meet scaling demands and expert workload constraints.

### Requirements for AI-Driven Grading System:

- **Automated Grading Pipeline** – AI models must evaluate short-answer responses based on predefined scoring criteria.
- **Human-in-the-loop (HITL) validation** – Experts must oversee AI grading and refine models for continuous improvement.
- **Structured Feedback Generation** – AI must provide **detailed explanations and justifications** for grading decisions.
- **Confidence-Based Expert Review** – AI must flag low-confidence evaluations for expert validation.
- **Adaptive Learning Mechanism** – AI models must continuously improve based on expert corrections and evolving certification criteria.
- **Security & Compliance** – AI must handle grading data with strict **privacy and security protocols**.
- **Integration with Certification Systems** – AI grading must seamlessly integrate with existing certification infrastructure.

## Assumptions

### Business Assumptions

- The **evaluation process and scoring criteria** are linked to the detailed [Test 1 Requirements Document](/business-requirements/test1-grading-process.md).
- AI-driven automation **must not impact certification credibility**, ensuring continued recognition across industry standards.

### Technical Assumptions

- **Grading data is structured**, with predefined evaluation criteria used by human experts.
- **Current workflows include manual review interfaces** used by expert architects to evaluate responses and provide feedback.
- **Historical grading records are available**, which can be used for AI model training.
- The **existing certification system operates under strict security and compliance standards** such as **GDPR and ISO 27001**.
- The **architecture must allow AI-driven grading to integrate as a modular service** without disrupting existing workflows.
- **Response evaluation logic is well-documented**, ensuring AI implementation aligns with established grading methodologies.

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
