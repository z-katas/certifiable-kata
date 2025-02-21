# Strategy for Question and Case Study Generation

Date: [2025-02-20]  

## Status  

Accepted  

## Context  

Our system needs to generate new questions and case studies based on evolving architectural patterns and trends. The chosen approach must:  
- Adapt dynamically to new trends.  
- Ensure high-quality, relevant outputs.  
- Minimize manual intervention.  

## Alternatives  

Two primary options were considered:  
1. **Web Search + RAG (Retrieval-Augmented Generation)**  
2. **Structured Knowledge Base + Query Generation**  

### Option 1: Web Search + RAG (Chosen)  
- Uses web search APIs to retrieve the latest architectural discussions and papers.  
- Retrieves and processes external knowledge dynamically.  
- Leverages Proact to improve retrieval consistency.  
- Uses an LLM to generate structured questions and case studies.  

**Pros**  
- Dynamically captures emerging trends.  
- Scalable without significant manual updates.  
- Broad coverage across multiple sources.  

**Cons**  
- Risk of misinformation and inconsistencies.  
- Less explainability compared to structured knowledge bases.  
- Requires filtering to ensure relevance and reliability.  

### Option 2: Structured Knowledge Base + Query Generation (Not Chosen)  
- Stores curated architectural best practices, case studies, and historical data.  
- Uses structured queries with an LLM to generate new questions and case studies.  

**Pros**  
- Ensures high accuracy and explainability.  
- Avoids misinformation through manual curation.  
- Provides stable and consistent knowledge retrieval.  

**Cons**  
- Requires continuous manual updates to stay relevant.  
- Limited adaptability to new trends.  
- High maintenance and operational costs.  

## PrOACT  

**Problem**  
The system must generate high-quality questions and case studies that stay relevant to evolving architectural trends while minimizing manual intervention.  

| Feature                 | Web Search + RAG                                  | Structured Knowledge Base + Query Generation |
|-------------------------|--------------------------------------------------|---------------------------------------------|
| **Adaptability**        | High - Captures emerging trends dynamically     | Low - Requires frequent manual updates     |
| **Scalability**         | High - Expands with web data                     | Medium - Limited by curated content        |
| **Explainability**      | Low - Needs filtering and verification           | High - Based on structured, validated data |
| **Risk of Misinformation** | Medium - Requires filtering and validation  | Low - Content is manually curated          |
| **Maintenance Effort**  | Low - Automated retrieval and generation        | High - Needs frequent knowledge updates    |

## Decision  

We choose **Web Search + RAG** as the primary approach for generating questions and case studies.  
To mitigate risks, we will implement:  
1. **Rule-Based Filtering** – To remove low-quality or irrelevant sources.  
2. **LLM-Based Evaluation** – To assess and validate the generated content.  
3. **Human-in-the-Loop (HITL) Review** – For final verification of high-stakes content.  

## Tradeoffs - Mitigations  

| Tradeoff                      | Mitigation Strategy |
|--------------------------------|---------------------|
| Potential misinformation      | Rule-based filters to exclude unreliable sources |
| Inconsistent retrieval        | Proact to retain and rank high-quality retrieved knowledge |
| Explainability concerns       | HITL review for final validation |
| Computational overhead        | Caching and indexing for efficient retrieval |
