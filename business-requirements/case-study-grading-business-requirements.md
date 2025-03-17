## Challenges in Expansion Plans

- The current **manual grading process** for Test 2 case study submissions is **slow, expensive, and unscalable**.
- Each submission requires **8 hours** of expert evaluation. With the planned **5-10X expansion** ( 2000 new candidates per week), the number of Test 2 evaluations is expected to reach **1,200-1,500 candidates per week** on average. This would result in a **grading workload of 9,600-12,000 hours per week**, far exceeding the capacity of available experts.
- The **$960K-$1.2M per week** cost of manual grading makes scaling financially unsustainable.
- Grading inconsistencies, including negative bias (grading lower than deserved) that may harm candidates and positive bias (grading higher than deserved) that may impact Certifiable, Inc., contribute to scoring variability and delays in feedback, ultimately affecting the candidate experience.

## Problem Statement & Scope

- The current manual grading process for Test 2 is unsustainable, requiring **8 hours per candidate**, making it infeasible to support the projected **5-10X growth in applicants**.
- **Generative AI** will automate grading while ensuring **scalability, accuracy, cost-effectiveness, and efficiency**, maintaining expert-level evaluation quality as mentioned in the main readme.md.
- **Cost-effectiveness** – AI-driven grading must be **less than the current $960K-$1.2M per week manual grading budget**.
- **Productivity** – The solution must **improve grading efficiency by at least 4X** to meet scaling demands and expert workload constraints.

### Requirements for AI-Driven Grading System:

- **Automated Grading Pipeline** – AI models must evaluate case study responses based on predefined scoring criteria.
- **Human-in-the-loop (HITL) validation** – Experts must oversee AI grading and refine models for continuous improvement.
- **Structured Feedback Generation** – AI must provide **detailed explanations and justifications** for grading decisions.
- **Confidence-Based Expert Review** – AI must flag low-confidence evaluations for expert validation.
- **Adaptive Learning Mechanism** – AI models must continuously improve based on expert corrections and evolving certification criteria.
- **Security & Compliance** – AI must handle grading data with strict **privacy and security protocols**.

## Assumptions

### Business Assumptions

- The **evaluation process and scoring criteria** are linked to the detailed [Test 2 Requirements Document](/business-requirements/test2-grading-process.md).
- AI-driven automation **must not impact certification credibility**, ensuring continued recognition across industry standards.

### Technical Assumptions

- **Grading data is structured**, with predefined evaluation criteria used by human experts.
- **Current workflows include manual review interfaces** used by expert architects to evaluate responses and provide feedback.
- **Historical grading records are available**, which can be used for AI model training.
- The **existing certification system operates under strict security and compliance standards** such as **GDPR and ISO 27001**.
- The **architecture must allow AI-driven grading to integrate as a modular service** without disrupting existing workflows.
- **Response evaluation logic is well-documented**, ensuring AI implementation aligns with established grading methodologies.
