# Monitor software architecture trends

## Use Case & Problem Statement
- **Primary Goals:** HMW monitor software architecture trends for expert architects so that certification content stays aligned with evolving industry standards?
- **Scope:**
- **Current Challenges:**
- **Limitations of Existing System:**
- **Impact of Identified Issues:**

## Assumptions
- **Business Assumptions:**
- **Technical Assumptions:**
- **Regulatory & Compliance Considerations:**

## New User Journey / Golden Path
- **Job To Be Done (JTBD):**
- **High-Level User Flow:**
- **Key Steps in the Process:**
- **Expected Outcomes:**

## Architecture Diagrams
### Container Diagram (C2)
- **Description:** Containers and interactions
- **Diagram:**
![test 1 and test 2 content updates](/assets/new-questions-c2.png "test 1 and test 2 content updates")
### Flow Diagram
- **Description:** Flow involving chunking of documents, storing in vector store and retrieival by the expert Architect to update the tests
- **Diagram:**
![test 1 and test 2 content updates](/assets/New-test1-and-test2-questions.png "test 1 and test 2 content updates")

## Constraints
- **Technical Constraints:** 
  - Embedding model limitations around accuracy, relevancy and scalability
    - Mitigation - optimizing the number of dimensions
  - Vector store performance due to growing number of vectors
    - Mitigation - Sharding, appropriate indexing strategy(e.g - HNSW)
  - LLM model context window limitations and cost implications
    - Mitigation - Passing summarized architecture context to LLM, self hosting open source models
- **Operational Constraints:** 
  - Expert Architect Involvement to review questions and case studies before including them in the tests
    - Mitigation - Only show top rated new questions and case studies so as to reduce time spent by experts in reviewing questions  
  
- **Security & Compliance Constraints:**
  - Access control: To restrict access to sensitive data.
  - Data Masking and Anonymization: Data masking and anonymization techniques to protect sensitive information.


## Architectural Decision Records (ADRs)
- [**ADR 1 - Architecture documents chunking strategy**](/ADRs/adr-architecture-knowledge-chunking-strategy.md)

- [**ADR 2 - Strategy for generating new questions and case studies**](/ADRs/adr-new-questions-and-case-studies-strategy.md)

## Implementation Details

### **Gen AI Technical Components & Architecture**
- **Local Inference & Cloud Services:**
  - A cheap **cloud-based LLMs** such as gpt 4omini 
- **Fine-Tuning & Adaptation:**
  - We don't need to fine tune our model as this is a generic usecase where we are accessing mostly public information about architecture
  patterns to come up with questions and case studies.
- **LLM Inference & Structured Outputs:**
  - Implementation of **structured response generation** for candidate feedback and grading justifications.
- [**Prompt Engineering & Validation:**](/ADRs/adr-llm-guardrails.md)
  - **Dynamic prompt orchestration** for AI models ensuring contextual accuracy.
  - **Guardrails & validation mechanisms** to filter out misleading or biased responses.
- **Information Retrieval & Search Engine:**
  - **Vector-based search** using embeddings to improve knowledge retrieval for generating new aptitude test questions and case studies.
  - **Search Engine** to retrieve latest architecture content including patterns, trends and techniques.
- **Observability & Performance Monitoring:**
  - **Prompt & model evaluation pipelines** 
  - **LLM observability tools** to track model behavior and response drift.


## Conclusion

- **Summary of Changes:** AI-driven automation for adding new aptitude test questions and case studies. We propose a robust system for expanding our proprietary architecture knowledge base with new questions and case studies, leveraging Retrieval Augmented Generation (RAG) for intelligent information retrieval.  The process begins with secure ingestion and chunking of new content from various formats (HTML, PDF, etc.).  These chunks are then converted into vector embeddings using a specialized model, enabling semantic search and retrieval.
These embeddings are stored in a secure, high-performance vector store, optimized for scalability and speed.

- **Benefits of the New Architecture:** 
  - Automated generation of new architecture aptitude test questions and case studies, thereby reducing manual workload
  - Continous update of knowledge base with latest architecture content
  - Reduced Risk of Knowledge Loss due to expert turnovers
  - Reduced "Shelf Life" of Leaked case studies 
- **Potential Risks & Mitigations:** AI bias monitoring, human oversight mechanisms, LLM Hallucinations, Integration challenges
- **Next Steps:** Phase wise implementation and Governance
