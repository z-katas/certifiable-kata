# Title

Evaluating LLM-Based Strategies for Automating Short-Answer Grading

## Status

Accepted

## Context

Our goal is to automate short-answer grading using large language models (LLMs). We want a solution that:

- Achieves high accuracy on both seen and unseen questions.
- Generates not just a numeric score but also optional formative feedback.
- Minimizes extensive fine-tuning or data-collection overhead.

Recent advances in LLMs (e.g., Mistral, Llama models) open up new ways to accomplish short-answer grading—ranging from zero-shot prompting to retrieval-augmented generation (RAG). We have three main alternatives to evaluate.

### Alternatives

Below is a summary of key approaches:

| Approach                               | Key Strengths                                                                                         | Key Weaknesses                                                                                                  | Implementation Complexity                           | Performance on Unseen Questions                                                                    | Overall Suitability                                                                                |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| 1. Zero-Shot Prompting (ASAS-F-Z)      | • No fine-tuning needed. <br> • Quick to deploy. <br> • Decent performance in general.                | • Prompts can be brittle. <br> • May hallucinate or be inconsistent without examples. <br> • Hard to customize. | Low: Requires prompt crafting but no model training | Moderate: Performs fairly well but can degrade if questions diverge from model’s pretraining data. | Useful if data are sparse and time to market is paramount.                                         |
| 2. Fine-Tuned LLM                      | • Good on well-known question styles. <br> • Straightforward integration into existing pipelines.     | • Requires substantial labeled data for each domain. <br> • Quality drops significantly on unseen questions.    | High: Must gather/label data and train              | Low-to-Moderate: Struggles on novel questions, does well on training-like data.                    | Suitable for stable course setups with repeated question types.                                    |
| 3. RAG-Based Few Shot COT (ASAS-F-RAG) | • Dynamically retrieves relevant examples, guiding LLM. <br> • Strong generalization to unseen items. | • Requires indexing infrastructure. <br> • Retrieval adds an extra step (slightly more complex to implement).   | Moderate: Must set up retriever + pre-existing LLM  | High: Best for adapting to new questions and maintaining accuracy across varied answer patterns.   | Strong option if you expect new or frequently changing questions, and want robust feedback output. |

## PrOACT

### Problem:

We need a scalable way to score short answers with minimal overhead and strong performance—especially for new/unseen questions.

### Objectives:

- High accuracy on unseen questions
- Minimal fine-tuning cost
- Feasible to generate formative feedback

### Alternatives:

1. Zero-Shot Prompting,
2. Fine-Tuned LLM
3. Retrieval-Augmented Generation (RAG) based few shot learning chain of thought prompting

### Consequences:

- Zero-Shot Prompting can be fast but might degrade under domain shifts.
- Fine-Tuning can excel in stable, well-known questions but is prone to drops on new questions.
- RAG based approach adds complexity but yields more robust scores and feedback when questions evolve.

### Trade-Offs:

Balancing infrastructure complexity (RAG) vs. performance on new data (RAG is strong) vs. minimal engineering overhead (Zero-Shot).

## Decision

Adopt a Retrieval-Augmented Generation (RAG)based few shot learning chain of thought prompting approach for short-answer scoring. The indexing of existing labeled examples allows for robust feedback and more reliable scoring, especially on previously unseen questions. This method tends to outperform fine-tuned and purely zero-shot LLMs in more dynamic educational settings.

## Tradeoffs – Mitigations

- Extra Infrastructure (Retriever Index):

  - Mitigation: Use a lightweight dense-retrieval solution (ColBERT or a similar vector-based engine).

- Possible Hallucinations or Irrelevance:

  - Mitigation: Continue to refine prompt instructions to emphasize correct usage of retrieved examples.

- Higher Complexity Than Zero-Shot:

  - Mitigation: Establish modular design, so that the retrieval pipeline and LLM prompt can be maintained separately.

- Cost vs. Accuracy Tradeoff:
  - Mitigation: Dynamically adjust the number of retrievals (top-k) to control latency and cost, while still preserving performance.
