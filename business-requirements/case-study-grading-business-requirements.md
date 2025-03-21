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

## New User Journey / Golden Path using Jobs to be Done Framework

**Persona:** [Alex, Expert Architect](/business-requirements/exper-architect-persona.md)

**Main Job:** Evaluate and grade case study submissions efficiently across multiple artifacts.

**Backstory:** After completing their primary architectural work, Alex is assigned to evaluate Test 2 case study submissions for **4-5 candidates per week**. With limited time available, Alex relies on AI-assisted grading to enhance efficiency and ensure consistency in evaluations across five key submission artifacts.

**End Goal of the Main Job:** Ensure fair, structured, and expert-level grading of case study submissions while reducing the grading workload and maintaining high evaluation standards.

**Job Steps (using universal job map):**
1. **View candidate submissions** – Access all case study artifacts.
2. **Review system-generated scoring for each artifact** – Ensure AI-assigned scores align with grading criteria.
3. **Assess system-generated reasoning** – Verify AI explanations for grading decisions.
4. **Modify the system-generated assessment** – Adjust AI evaluations where necessary.
5. **Adjust final score if required** – Confirm that scores reflect accurate assessment.
6. **Generate structured feedback reports** – Provide candidates with AI-assisted, expert-reviewed feedback for each artifact.
7. **Modify feedback reports if necessary** – Ensure clarity and relevance before submission.
8. **Submit final evaluation results** – Confirm scores and update certification records for candidate progression.

