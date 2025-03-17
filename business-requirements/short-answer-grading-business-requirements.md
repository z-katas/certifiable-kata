## Challenges in Expansion Plans

- The current **manual grading process** for Test 1 short-answer responses is **slow, expensive, and unscalable**.
- Each submission requires **3 hours** of expert evaluation, limiting grading capacity to **200 candidates per week**.
- With planned expansion to **2,000 candidates weekly**, grading workload would surge to **6,000 hours per week**, overwhelming available experts.
- The **$300K per week** cost of manual grading makes scaling financially unsustainable.
- Grading inconsistencies, including negative bias (grading lower than deserved) that may harm candidates and positive bias (grading higher than deserved) that may impact Certifiable, Inc., contribute to scoring variability and delays in feedback, ultimately affecting the candidate experience.

## Problem Statement & Scope

- The current manual grading process for Test 1 is unsustainable, requiring **3 hours per candidate**, making it infeasible to support the projected **5-10X growth in applicants**.
- **Generative AI** will automate grading while ensuring **scalability, accuracy, cost-effectiveness, and efficiency**, maintaining expert-level evaluation quality as mentioned in the main readme.md.
- **Cost-effectiveness** – AI-driven grading must be ** less than the current $300K per week manual grading budget**.
- **Productivity** – The solution must **improve grading efficiency by at least 4X** to meet scaling demands and expert workload constraints.

### Requirements for AI-Driven Grading System:

- **Automated Grading Pipeline** – AI models must evaluate short-answer responses based on predefined scoring criteria.
- **Human-in-the-loop (HITL) validation** – Experts must oversee AI grading and refine models for continuous improvement.
- **Structured Feedback Generation** – AI must provide **detailed explanations and justifications** for grading decisions.
- **Confidence-Based Expert Review** – AI must flag low-confidence evaluations for expert validation.
- **Adaptive Learning Mechanism** – AI models must continuously improve based on expert corrections and evolving certification criteria.
- **Security & Compliance** – AI must handle grading data with strict **privacy and security protocols**.

## Assumptions

### Business Assumptions

- The **evaluation process and scoring criteria** are linked to the detailed [Test 1 Requirements Document](/business-requirements/test1-grading-process.md).
- The number of Expert Software Architect Consultants and Designated Expert Software Architects remains constant.
- Multiple choice grading is handled by the existing scalable architecture with no additional cost.
- AI-driven automation **must not impact certification credibility**, ensuring continued recognition across industry standards.

### Technical Assumptions

- We estimate the average capacity will increase to 10× the current capacity (i.e., the maximum of the 5–10× range).
- The system will be designed for peak capacity, assumed to be 1.2× the average capacity (i.e., 20% above average), while considering cost factors.
- AI-based grading is considered feasible as long as the cost of grading via AI is comparable to or lower than manual grading.
- Stored grading data will be leveraged to enhance the performance of the new AI-powered ASAS.
- The new ASAS solution will operate alongside the current manual process. Submissions not picked for manual grading will be processed by AI.
- Any submission pending short answer grading for more than two days (unless explicitly marked otherwise) can be processed by AI.
- **Grading data is structured**, with predefined evaluation criteria used by human experts.
- **Current workflows include manual review interfaces** used by expert architects to evaluate responses and provide feedback.
- **Historical grading records are available**, which can be used for AI model training.
- The **existing certification system operates under strict security and compliance standards** such as **GDPR and ISO 27001**.
- The **architecture must allow AI-driven grading to integrate as a modular service** without disrupting existing workflows.
- **Response evaluation logic is well-documented**, ensuring AI implementation aligns with established grading methodologies.

## New User Journey / Golden Path using Jobs to be done framework

**Persona:** [Alex,Expert Architect](/business-requirements/exper-architect-persona.md)

**Main Job:** Evaluate and grade short-answer responses efficiently.

**Backstory:** After completing their main project, the expert architect must evaluate Test 1 responses for **5-7 candidates per week**. With a maximum of 2 hours available per day, Alex logs into the application to begin the evaluation process.

**End Goal of the Main Job:** Ensure consistent, fair, and expert-level grading with structured and justifiable feedback.

**Job Steps(using universal job map):**

1. **View candidate submissions** – Access all short-answer responses in the system.
2. **Analyze AI-generated grading recommendations** – Review AI-suggested scores and feedback for accuracy.
3. **Validate flagged responses** – Manually assess AI-flagged responses requiring expert review.
4. **Adjust grading if discrepancies are found** – Modify AI-assigned scores based on expert judgment.
5. **Finalize and confirm scores** – Ensure all reviewed responses meet grading standards.
6. **Generate structured feedback reports** – Provide candidates with AI-assisted, expert-reviewed feedback.
7. **Modify feedback reports if necessary** – Ensure clarity and relevance before submission.
8. **Submit final evaluation results** – Confirm scores and update certification records for candidate progression.
