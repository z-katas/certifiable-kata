# LLM Embedding Model Decision

Date:  [2025-02-14]

## Status

Accepted

## Context

We need to decide on the approach for generating text embeddings using an LLM for semantic search, adding new test questions and candidate's tests submission analysis. The embedding model must generate high-quality vector representations for ideal answers of the questions given data and test submission metrics while ensuring scalability and adaptability for domain-specific needs.

### Alternatives

- **Pre-trained Embedding Model**: Use an existing pre-trained embedding model (e.g., OpenAI, BERT, Sentence Transformers) without any customization.
- **Custom Fine-Tuned Embedding Model**: Provides a better fit for domain-specific tasks, though it introduces training overhead and infrastructure requirements.
- **Train from Scratch**: Delivers maximum control and potentially the best performance for niche tasks, but at the cost of significant computational and time resources.

### PrOACT

**Problem**: Choose the best embedding model approach to meet the unique needs, ensuring high performance in tasks like test submission analysis, analysing metrics with high level of accuracy and reliability.

**Objectives**:

- Generate high-quality embeddings for semantic analysis of test submissions
- Ensure embeddings are relevant to case study and short answers.
- Minimize operational costs and avoid unnecessary complexity.
- Maintain flexibility and scalability to accommodate future feature expansion.

| **Component**   | **Pre-trained Model**                                                                    | **Fine-tuned Model**                                                                  | **Domain-specific Model**                                                                            |
| --------------- | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Latency**     | Low latency, can be used directly with minimal setup.                                    | Moderate latency due to additional training time, but offers better domain relevance. | High latency in development and usage due to complex training and optimization processes.            |
| **Computation** | Low computational overhead, already optimized for general use.                           | Moderate computational cost during fine-tuning, but improves search relevance.        | High computational power required for training and maintaining a domain-specific model from scratch. |
| **Cost**        | Low cost, minimal infrastructure needed; no need for additional training.                | Medium cost, involves fine-tuning but cheaper than training a model from scratch.     | High cost in both training and maintaining infrastructure for a custom model.                        |
| **Accuracy**    | General-purpose accuracy; may lack domain-specific insights needed for DEI and HR tasks. | Improved accuracy for HR and DEI tasks through fine-tuning.                           | Maximum accuracy for the domain but dependent on data quality and volume, with high resource demand. |
| **Scalability** | Highly scalable; plug-and-play across various domains.                                   | Scalable, but requires additional resources for periodic fine-tuning and updating.    | Scalability challenges due to infrastructure requirements and frequent retraining.                   |

## Decision

Choosing from Hugging Face's leaderboard ensures that we start with a proven, high-performing foundation model, and fine-tuning will adapt it for the unique needs of the platform. This approach avoids the significant overhead of training a domain-specific model from scratch while still achieving the desired accuracy and performance improvements.

## Tradeoffs - Mitigations

- **Complexity**: Fine-tuning introduces complexity but avoids the need to train from scratch. We will mitigate this by starting with a strong pre-trained base model, which reduces the amount of data and time needed for fine-tuning.
- **Cost**: Fine-tuning requires computational resources but is more cost-effective than building a model from scratch. We will mitigate costs by optimizing the training process and fine-tuning only critical layers for HR-specific tasks.
- **Performance**: While a domain-specific model could offer slightly better performance, fine-tuning a pre-trained model provides a strong balance of accuracy and efficiency. We will ensure the fine-tuned model meets the accuracy through iterative testing.
- **Scalability**: The fine-tuned model will scale effectively across growing dataset. We will periodically retrain or fine-tune the model to accommodate changes in new test questions and submission metrics without needing to overhaul the entire system.