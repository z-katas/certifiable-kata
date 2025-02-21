# LLM Evaluation strategy Decision

Date: [2025-02-20]

## Status

Accepted

## Context

‍LLM evaluations, or evals for short, help assess the performance of a large language model to ensure outputs are accurate, safe, and aligned with user needs. The term applies in two key contexts:

1. Evaluation of the LLM itself.
2. Evaluation of systems built with LLMs.

When evaluating an LLM directly, the focus is on its raw abilities. There are hundreds of LLM benchmarks, each with its own set of test cases. However, while these benchmarks are great for choosing models and tracking industry progress, they’re not very useful for evaluating real-world products. They test broad capabilities, not the specific inputs the system might handle. They also focus on the LLM alone, but our product will involve other components. LLM product evaluation assesses the full system's performance for its specific task.
This includes not just the LLM, but everything else: the prompts, the logic connecting them, the knowledge databases used to augment the answers, etc.

The testing of a LLM based system differs from a traditional software system as they produce probabilistic outputs i.e generate different outputs for identical inputs. The challenges include - non deterministic behaviour, wide range of inputs, prompt injections, jail breaks, hallucinations etc.

Certifiable inc system uses LLM mainly for evaluation of short answers in Test 1, case study submissions in Test 2 and adding new questions to the aptitude test database and new case studies to case study database. To ensure accurate and fair automatic grading of text-based answers and architecture case studies using an LLM, as well as the generation of new questions based on emerging architecture patterns and trends, a robust evaluation strategy is required. The evaluation must balance accuracy, scalability, interpretability, and fairness while maintaining cost-effectiveness.

### Alternatives

![LLM evals techniques](/assets/LLM-evals-techniques.png "LLM evals techniques")

1. **Manual Evaluation (Human Review)**  
   - Experts manually assess a sample of LLM-graded responses and generated questions.  
   - **Why Needed:** Provides a gold-standard reference to validate automated approaches.  
   - **What It Evaluates:** Grading correctness, fairness, quality of generated questions.  
   - **Pros:** High accuracy and reliability.  
   - **Cons:** Time-consuming, costly, and not scalable.  

2. **Automated Evaluation Metrics**  
   - Uses heuristic-based metrics (e.g., BLEU, ROUGE, GPTScore) to compare LLM-generated grades and questions against reference responses.  
   - **Why Needed:** Provides a quick, scalable, and consistent baseline assessment.  
   - **What It Evaluates:** Surface-level correctness, coherence, similarity to reference grading/questions.  
   - **Pros:** Fast, scalable, and consistent.  
   - **Cons:** Lacks deep contextual understanding.  

3. **LLM as a Judge**  
   - Uses a secondary LLM to evaluate the correctness of grading and the relevance of generated questions.  
   - **Why Needed:** Enables automated review of grading/question quality with contextual understanding.  
   - **What It Evaluates:** Logical soundness, argument structure, factual correctness, alignment with intended learning outcomes.  
   - **Pros:** Fully automated and scalable.  
   - **Cons:** Requires fine-tuning and validation to ensure reliability.  

4. **Rubric-Based LLM Evaluation**  
   - Uses structured grading rubrics to assess LLM-generated grades and systematically evaluate question quality.  
   - **Why Needed:** Ensures structured, explainable, and transparent evaluation.  
   - **What It Evaluates:** Adherence to predefined grading criteria and question relevance.  
   - **Pros:** Improves interpretability and grading consistency.  
   - **Cons:** May not handle highly subjective or creative responses effectively.  

5. **Human-in-the-Loop Evaluation**  
   - Combines automated evaluation with selective human review.  
   - **Why Needed:** Provides human oversight for ambiguous or high-impact cases.  
   - **What It Evaluates:** Conflicting or uncertain grading/question generation decisions.  
   - **Pros:** Balances automation with expert oversight.  
   - **Cons:** Requires additional resources and workflow integration.  

### Evaluation Criteria

The following criteria will be used to assess the effectiveness of each strategy:

- **Accuracy:** How well the evaluation aligns with human judgment.
- **Scalability:** Ability to handle large volumes of evaluations efficiently.
- **Automation:** Degree of human involvement required.
- **Interpretability:** Clarity and explainability of evaluation results.
- **Fairness & Bias Mitigation:** Ability to identify and reduce biases.
- **Complexity:** Implementation difficulty and operational overhead.
- **Cost:** Resource and operational expenses.
- **Stress Testing:** Performance under adversarial, ambiguous, or high-volume grading/question generation scenarios.

### PrOACT Analysis

| Approach                     | Accuracy       | Scalability    | Automation    | Interpretability | Fairness & Bias Mitigation | Complexity   | Cost      | Stress Testing |
|------------------------------|---------------|---------------|--------------|------------------|----------------------------|--------------|----------|---------------|
| Manual Evaluation            | Very High     | Low           | Low          | Very High        | Very Strong                | Moderate     | High     | Very Strong   |
| Automated Evaluation Metrics | Moderate      | Very High     | Very High    | Moderate         | Weak                        | Low          | Low      | Weak          |
| LLM as a Judge               | Moderate      | Very High     | Very High    | Moderate         | Moderate                    | Moderate     | Medium   | Moderate      |
| Rubric-Based LLM Evaluation  | High          | High          | High         | Very High        | Moderate                    | Moderate     | Medium   | High          |
| Human-in-the-Loop Evaluation | Very High     | Moderate      | Moderate     | Very High        | Very Strong                | Moderate     | Medium   | Very Strong   |

## Decision

A **Hybrid Evaluation Strategy** will be implemented, combining:

- **Automated Evaluation Metrics** for initial screening and efficiency.  
  - Quickly flags potential grading inconsistencies and low-quality questions.
  - Helps prioritize human review where necessary.

- **Rubric-Based LLM Evaluation** for structured assessments.  
  - Ensures grading and question generation follow a clear, interpretable framework.
  - Improves consistency across evaluations.

- **LLM as a Judge** for deeper automated assessments.  
  - Provides contextual analysis of grading decisions.  
  - Detects logical flaws, incorrect reasoning, and vague or misleading questions.  

- **Human-in-the-Loop Review** for quality control.  
  - Resolves ambiguous or contentious cases.  
  - Ensures fairness and bias mitigation in automated evaluations.  

## Tradeoffs - Mitigations

- **Human Review Overhead:** Minimize human involvement to only edge cases and periodic audits.  
- **Bias in LLM-based Evaluation:** Perform fairness audits and bias correction through iterative model updates.  
- **Balancing Scalability and Accuracy:** Leverage automation for bulk processing while retaining human oversight for critical cases.  
- **Complexity of Multiple Approaches:** Phase-wise implementation to ensure smooth adoption.  
- **Stress Testing for Robustness:** Regularly introduce adversarial test cases to validate system resilience.  

This strategy ensures a balanced, scalable, and fair evaluation framework for LLM-based grading and question generation.
