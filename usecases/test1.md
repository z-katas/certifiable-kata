# Test 1: Analysis

This document analyzes the current Test 1 grading process and outlines a new solution approach for scaling short answer grading using LLMs.

## Key Points from the Problem Statement

- Expert Software Architect Consultant count: 300
- Designated Expert Software Architect count: 5
- Pay rate for Expert Software Architects: $50 per hour
- Current capacity: 200 certifications per week
- Expected growth (after considering all factors): 5-10× increase
- Certification exam price: Fixed
- Test 1 details:
  - Aptitude test is timed to prevent candidates from looking up answers.
  - Multiple choice questions are auto-graded.
  - Short answer questions are manually graded by expert software architects.
  - Manual grading turnaround time for short answers: 1 week
  - Passing grade in Test 1: 80%
  - If the percentage of incorrect answers exceeds 95%, the question will undergo modification.
- Market data:
  - Number of software architects in the US: 176,000
  - Number of software architects in the UK, Europe, and Asia: 600,000
  - Number of certified software architects in Certifiable DB: 120,000
  - Percentage of companies insisting on or accepting Certifiable, Inc.’s certification: 80%
- Concerns:
  - Significant cost overruns with AI (acceptable in the short term).
- Additional details:
  - Manual grading and feedback for a short answer takes 3 hours.
  - Test 1 feedback includes:
    - Detailed explanations for incorrect answers.
    - Detailed explanations for partially incorrect answers.
- Bias implications:
  - Negative bias (grade lower than deserved) may harm the candidate.
  - Positive bias (grade higher than deserved) may harm Certifiable, Inc.

## Solution Approach Outline

The existing manual grading process for short answer questions in Test 1 is not scalable given the anticipated growth. To address this, we propose developing an AI-powered Automated Short Answer Scoring (ASAS) pipeline that works alongside the manual grading process. The two critical requirements for the AI solution are:

1. Accuracy: The AI grade should closely mirror the manual grading process and provide detailed feedback explaining its evaluation.
2. Cost effectiveness: The long-term average cost per graded submission via AI should be equal to or less than the cost incurred through the manual grading process.

## Assumptions

- The number of Expert Software Architect Consultants and Designated Expert Software Architects remains constant.
- We estimate the average capacity will increase to 10× the current capacity (i.e., the maximum of the 5–10× range).
- The system will be designed for peak capacity, assumed to be 1.2× the average capacity (i.e., 20% above average), while considering cost factors.
- Multiple choice grading is handled by the existing scalable architecture with no additional cost.
- AI-based grading is considered feasible as long as the cost of grading via AI is comparable to or lower than manual grading.
- Previously graded short answer submissions and associated feedback are stored and available for reuse.
- Stored grading data will be leveraged to enhance the performance of the new AI-powered ASAS.
- The new ASAS solution will operate alongside the current manual process. Submissions not picked for manual grading will be processed by AI.
- Any submission pending short answer grading for more than two days (unless explicitly marked otherwise) can be processed by AI.

## High-Level Solution Approach

We will develop an ASAS solution that leverages Large Language Models (LLMs) to automatically grade short answer responses and generate candidate feedback. The solution consists of two key services:

1. ASAS Grader: Grades short answer submissions and provides detailed feedback.
2. ASAS Judge: Assigns a confidence score to the grading outcome, ensuring quality and consistency.

Workflow:

- The ASAS Judge provides a confidence score for the generated grading.
- If the confidence score exceeds a configurable threshold, the result is finalized automatically.
- Submissions with scores below the threshold are stored for manual review by Expert Software Architects.
- The manual review outcomes feed back into the ASAS Judge to improve its confidence scoring over time.

This hybrid approach ensures that the AI-generated results closely mimic manual grading.

## High-Level Data Flow Diagram

Below is the high-level data flow diagram for Test 1:

![Test 1 High Level Data Flow](/assets/test1-high-level-flow-diagram.jpg "Test 1 High Level Data Flow")

Recent research ([Ref1](https://arxiv.org/abs/2409.20042), [Ref2](https://arxiv.org/abs/2408.03811)) shows that a Retrieval-Augmented Generation (RAG) approach combined with Few-Shot examples and Chain-of-Thought reasoning significantly improves performance in Automated Short Answer Scoring tasks across multiple LLMs—with no fine-tuning. This is the strategy we will adopt. Please refer to this [ADR](/ADRs/adr-llm-based-short-answer-evalaution-strategy.md) for a more detailed analysis of this choice.

## Short Answer Grade ETL Service

The ETL (Extract, Transform, Load) service will:

- Load existing, manually graded short answer submissions along with feedback.
- Transform the data into a standardized schema.
- Embed the data using the selected embedding model (see [ADR](/ADRs/adr-llm-embedding-model.md)) and store it in the chosen vector store (see [ADR](/ADRs/adr-llm-vector-store.md)).

This ETL process is scheduled regularly to ensure that newly manually graded tests continuously improve the vector store, thereby enhancing ASAS’s future grading outcomes.

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
    - [Prompt Orchestrator](/ADRs/adr-prompt-orchestrator.md)
    - [Structured Output](/ADRs/adr-llm-structured-output.md)
    - [Embedding Model](/ADRs/adr-llm-embedding-model.md)
    - [Vector Store](/ADRs/adr-llm-vector-store.md)
    - [Vector Search](/ADRs/adr-llm-vector-search.md)
11. Other links
    - [Example Test 1 Grading Process](/business-requirements/test1-grading-process.md) : Could be used for creating system prompt fot ASAS Grader

## ASAS Judge

The ASAS Judge is responsible for evaluating the quality of the AI-generated grading. It uses various LLM as Judge tools/frameworks to perform it's duties. Its workflow includes:

1. Retrieve a grading submission awaiting judgment.
2. Use the vector search to fetch relevant historical submissions.
3. Retrieve the appropriate prompt template from an external Prompt Management System.
4. Uses the selected LLM evaluation techniques (see [ADR](/ADRs/adr-llm-evaluation.md))
5. (Optional) Publish the query to the LLM query queue and subscribe to the LLM response queue.
6. Update the grading submission in the ASAS database with the computed confidence score.
7. Compare the confidence score against a predefined, configurable threshold:
   - If above the threshold, finalize the grading.
   - If below, update the status to “Pending Manual Review.”
8. Integrate the outcomes of manual review to continuously refine the judgment prompt.
9. Relevant ADRs
   - [Observability](/ADRs/adr-llm-observability.md)

## AI Model Gateway

The AI Model Gateway orchestrates communication between queued queries and the LLM models. Its responsibilities include:

1. Pulling queries from the LLM query queue and performing generic guardrail checks.
2. Looking up cached responses; if none exist, batching the query for processing.
3. Identifying the appropriate model for each query batch and routing them accordingly.
4. Updating the cache with optimized LLM outputs.
5. Publishing responses to the LLM response queue.
6. Relevant ADRs
   - [AI Gateway](/ADRs/adr-using-ai-gateway.md)
   - [LLM Deplyment](/ADRs/adr-llm-deployment.md)
   - [Multi Model AI](/ADRs/adr-ai-multi-model-strategy.md)

## ASAS Grader C2 Diagram

The diagram below illustrates the core components of the AI Grader service:

![ASAS Grader C2 Diagram](/assets/test1-grader-c2.jpg "ASAS Grader C2 Diagram")

Note: Due to time constraints and brevity, C2 diagrams for the other components are omitted.
