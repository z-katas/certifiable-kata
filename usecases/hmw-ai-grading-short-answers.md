# Grading short answers

## Primary Goal

**HMW implement AI-driven grading models for expert architects so that they can evaluate short-answer submissions 4X faster?**

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

**High-Level User Flow:** [UI Mockup](https://claude.site/artifacts/f0f8e1fc-f904-4f28-9466-125f77e69127?fullscreen=true)

**Key screen:**

![Test 1 grading UI screen](/assets/Test1-grading.png)

## High-Level Solution Approach

Below is the high-level diagram for Test 1. ( see [Implementation Details](#implementation-details))

![Test 1 High Level Data Flow](/assets/test1-high-level-flow-diagram.jpg "Test 1 High Level Data Flow")

We will develop an ASAS solution that leverages Large Language Models (LLMs) to automatically grade short answer responses and generate candidate feedback. The solution consists of two key services:

1. ASAS Grader: Grades short answer submissions and provides detailed feedback.
2. ASAS Judge: Assigns a confidence score to the grading outcome, ensuring quality and consistency.

**Workflow:**

- The ASAS Judge provides a confidence score for the generated grading.
- If the confidence score exceeds a configurable threshold, the result is finalized automatically.
- Submissions with scores below the threshold are stored for manual review by Expert Software Architects.
- The manual review outcomes feed back into the ASAS Judge to improve its confidence scoring over time.

This hybrid approach ensures that the AI-generated results closely mimic manual grading. Splitting the Grader and Judge into separate components allows us improve/test one component while keeping the other component constant.

## ASAS Grader Preliminary C3 Diagram

The diagram below illustrates the core components of the AI Grader service. ( see [Implementation Details](#implementation-details))

![ASAS Grader Preliminary C3 Diagram](/assets/test1-grader-c3.jpg "ASAS Grader Preliminary C3 Diagram")

Note: Due to time constraints and brevity, C3 diagrams for the other components are omitted.

## Implementation Details

Below is a summarised version of the analysis. A more thorough version could be found [here](/usecases/test1-approach.md)

Recent research ([Ref1](https://arxiv.org/abs/2409.20042), [Ref2](https://arxiv.org/abs/2408.03811)) shows that a Retrieval-Augmented Generation (RAG) approach combined with Few-Shot examples and Chain-of-Thought reasoning significantly improves performance in Automated Short Answer Scoring tasks across multiple LLMs—with no fine-tuning. This is the strategy we will adopt. Please refer to this [ADR](/ADRs/003-adr-llm-based-short-answer-evalaution-strategy.md) for a more detailed analysis of this choice.

## ASAS Grader

The ASAS Grader will execute the following steps:

1. Retrieve a short answer submission pending grading.
2. Check for an existing entry in the ASAS database:
   - If an entry exists, bypass further processing and finalize the grade.
   - Otherwise, create a new entry and mark it as “being processed.”
3. Use vector search (with caching and re-ranking) to fetch relevant positively and negatively graded submissions.
4. Retrieve the necessary prompt template from an external Prompt Management System (e.g., Haystack, PromptHub, PromptLayer) that supports versioning and organization.
5. Construct a RAG-based Few-Shot Example Chain-of-Thought prompt to instruct the LLM to evaluate the submission and generate detailed feedback.
6. Filter the prompt using input guardrails to redact malicious or sensitive content.
7. Publish the query to the LLM query queue and subscribe to the LLM response queue.
8. Process the LLM response through output guardrails (to ensure valid structure, appropriate language, etc.).
9. Store the grading result in the ASAS database with a status of “Awaiting Judgement.”
10. Relevant ADRs
    - [Prompt Orchestrator](/ADRs/005-adr-prompt-orchestrator.md)
    - [Structured Output](/ADRs/012-adr-llm-structured-output.md)
    - [Embedding Model](/ADRs/008-adr-llm-embedding-model.md)
    - [Vector Store](/ADRs/014-adr-llm-vector-store.md)
    - [Vector Search](/ADRs/013-adr-llm-vector-search.md)
11. Other links
    - [Example Test 1 Grading Process](/business-requirements/test1-grading-process.md) : Could be used for creating system prompt fot ASAS Grader

## ASAS Judge

The ASAS Judge is responsible for evaluating the quality of the AI-generated grading. It uses various LLM as Judge tools/frameworks to perform it's duties. Its workflow includes:

1. Retrieve a grading submission awaiting judgment.
2. Use the vector search to fetch relevant historical submissions.
3. Retrieve the appropriate prompt template from an external Prompt Management System.
4. Uses the selected LLM evaluation techniques (see [ADR](/ADRs/009-adr-llm-evaluation.md))
5. (Optional) Publish the query to the LLM query queue and subscribe to the LLM response queue.
6. Update the grading submission in the ASAS database with the computed confidence score.
7. Compare the confidence score against a predefined, configurable threshold:
   - If above the threshold, finalize the grading.
   - If below, update the status to “Pending Manual Review.”
8. Integrate the outcomes of manual review to continuously refine the judgment prompt.
9. Relevant ADRs
   - [Observability](/ADRs/011-adr-llm-observability.md)

## AI Model Gateway

The AI Model Gateway orchestrates communication between queued queries and the LLM models. Its responsibilities include:

1. Pulling queries from the LLM query queue and performing generic guardrail checks.
2. Looking up cached responses; if none exist, batching the query for processing.
3. Identifying the appropriate model for each query batch and routing them accordingly.
4. Updating the cache with optimized LLM outputs.
5. Publishing responses to the LLM response queue.
6. Relevant ADRs
   - [AI Gateway](/ADRs/001-adr-using-ai-gateway.md)
   - [LLM Deplyment](/ADRs/007-adr-llm-deployment.md)
   - [Multi Model AI](/ADRs/002-adr-ai-multi-model-strategy.md)

## Conclusion

- **Summary of Changes:**
   - AI-driven automation replaces manual grading, significantly reducing the time required for evaluating short-answer responses.
   - Structured feedback generation ensures candidates receive detailed, consistent explanations for their scores.
   - Confidence-based review mechanism allows experts to validate AI-generated grades when necessary.
- **Benefits of the New Architecture:**
   - Scalability – Enables grading for thousands of candidates per week without increasing expert workload.
   - Faster Turnaround – Reduces grading time per response, ensuring candidates receive results in hours instead of days.
   - Reduced Manual Workload – Experts focus on validation and edge cases rather than routine grading.
- **Potential Risks & Mitigations:**
   - AI Bias & Inconsistencies – Implementing bias-detection mechanisms and benchmarking AI evaluations against historical grading patterns.
   - Quality Assurance – Expert oversight ensures AI-generated scores align with certification standards.
   - System Adaptability – AI models are periodically retrained using new grading patterns to maintain relevance and accuracy.
- **Next Steps:** Pilot AI grading system, evaluate AI explainability, and refine model accuracy based on real-world data.
