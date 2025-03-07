# Monitor software architecture trends & generate certification content

## Overview
Expert architects are responsible for **maintaining and updating certification content** to ensure alignment with **emerging industry trends and evolving best practices**. Currently, this process involves **manual research across industry articles, blogs, research papers, and conference talks**. Architects analyze industry developments, identify relevant topics, and create certification questions based on these insights. 
As the certification process requirements are not explicitly detailed, we assume that expert architects rely on **articles, journals, social media (LinkedIn, Twitter, Medium), podcasts, conference talks, and research papers** to stay updated with emerging trends in software architecture.

## Primary Goal
**HMW automate the identification of emerging software architecture trends and generate expert-level certification questions to assist architects in updating the certification database efficiently?**

## Challenges in Expansion Plans
- **Manual Trend Tracking** – Expert architects currently **manually review industry articles, blogs, research papers, and conference talks**, making the process **time-consuming and inefficient**.
- **Scalability Issues** – The **increasing volume of industry trends** makes it impractical for architects to manually assess, formulate, and validate new questions in real-time.
- **Consistency & Coverage** – There is **no structured approach** to ensuring that newly emerging topics are **systematically added to certification content**.
- **Expert Workload** – Architects are burdened with **identifying, reviewing, and structuring new questions**, delaying certification content updates.
- **Subjectivity & Bias Risks** – Individual architects may **overlook certain trends** or focus on **personally preferred topics**, leading to **gaps in certification coverage**.
- **Effort Workload in Creating New Questions Manually** – The process of manually drafting, validating, and integrating new questions requires significant time and cognitive effort from expert architects.

## Problem Statement & Scope
- The current manual process of **tracking trends and generating certification questions** is **inefficient, inconsistent, and unscalable**, leading to **delays in updating certification content**.
- **Generative AI** will automate **trend identification, question generation, and expert validation**, ensuring that **certification content remains updated, diverse, and industry-aligned**.
- **Key objectives** of the AI-driven solution:
  - **Efficiency** – Automate industry trend tracking and question generation to **reduce manual workload** on expert architects.
  - **Scalability** – Support **continuous updates to certification content** without adding excessive burden to expert reviewers.
  - **Consistency & Accuracy** – Ensure that **questions align with industry-validated trends** and **certification standards**.

## Key Functional Requirements

- **Trend Monitoring & Data Collection**  
  - Expert architects configure **sources and prompts** to guide AI in tracking industry trends.
  - AI continuously scrapes and aggregates data from:
    - Technical blogs & journals (ACM, IEEE, InfoQ, Martin Fowler, ThoughtWorks Radar, etc.)
    - Social media discussions (LinkedIn, Twitter, Reddit, Stack Overflow)
    - Conference talks & presentations (O’Reilly Software Architecture, QCon, DevOps Enterprise Summit)
    - Industry reports & whitepapers
  - AI processes and categorizes the extracted content into emerging software architecture topics.

- **Topic Analysis & Categorization**  
  - AI filters relevant topics based on:
    - Frequency of discussion (appearing in multiple sources)
    - Industry expert engagement (posts, citations, discussions)
    - Alignment with certification domains (Architectural Patterns, Scalability, Security, etc.)
  - Generates summarized insights on emerging trends.

- **Question Generation & Evaluation**  
  - AI generates:
    - Multiple-choice questions (MCQs) based on factual insights.
    - Short-answer questions focusing on critical thinking.
    - Case study scenarios for deeper application.
  - Questions include distractors and varying difficulty levels to ensure rigor.

- **Expert Architect Review & Approval**  
  - AI-generated questions are ranked by confidence level.
  - Architects evaluate AI-generated content, making modifications where necessary.
  - AI learns from modifications to improve future question generation.

- **Final Approval & Integration**
  - Approved questions are added to the certification question bank.
  - AI maintains a log of updates, tracking which trends led to new questions.
  - Periodic evaluation ensures question quality remains aligned with industry advancements.

## Assumptions
### Business Assumptions
- **Expert review remains essential** – AI assists in question generation, but final approval stays with expert architects.
- **AI must align with certification goals** – Trends and questions must map to certification learning objectives.
- **Bias prevention is critical** – AI should avoid generating misleading, biased, or overly niche questions.
- The persona is the designated expert architect(currently there are 5 designated experts) who serves as super admin to manage the test content.

### Technical Assumptions
- **AI will leverage Natural Language Processing (NLP)** to extract insights and generate questions.
- **Trend aggregation sources must be predefined** (ACM, IEEE, LinkedIn, ThoughtWorks Radar, etc.).
- **AI must provide confidence scores** for trend relevance and question quality.
- **AI-generated content must integrate seamlessly** with existing certification management systems.

## New User Journey / Golden Path using Jobs to be Done Framework

### **Persona:**  
[Chris,Designated Expert Architect](business-requirements/references/designated-expert-architect-persona.md)

### **Main Job:**  
Identify industry-relevant trends and generate expert-level certification questions efficiently.

### **Backstory:**  
Alex is responsible for keeping certification content **up to date** by ensuring **new software architecture trends** are incorporated into certification exams. Manually searching for industry trends, identifying relevant topics, and formulating certification questions is **time-consuming and inefficient**. AI-assisted automation is needed to streamline this process.

### **End Goal of the Main Job:**  
Ensure that **certification content reflects the latest industry advancements** by efficiently **identifying relevant trends and generating expert-validated certification questions**.

### **Job Steps (using universal job map):**
1. **Configure trend sources and search parameters** – Architects define sources and prompts for AI-based industry research.
2. **View AI-generated trend feed** – AI scrapes and presents insights from preconfigured sources[TBD].
3. **Review system-generated certification questions** – AI suggests MCQs, short-answer questions, and case study prompts.
4. **Assess AI-generated reasoning** – Validate AI's justification for trend relevance and question generation.
5. **Modify AI-generated content if necessary** – Experts refine AI-suggested questions and answers.
6. **Finalize and approve questions** – Validated questions are integrated into the certification database.
7. **Monitor AI learning improvements** – AI adjusts its trend analysis and question generation based on expert feedback.

**High level user flow:** [UI Mockup](https://claude.site/artifacts/043388db-7e9e-4716-8b82-8d5ca315adbc?fullscreen=true)

**Key screen:** 
![Admin dashboard-trends](/assets/admin-dashboard.png)


## Architecture Diagrams

### Container Diagram (C2)

![test 1 and test 2 content updates](/assets/new-questions-c2.png "test 1 and test 2 content updates")
New questions and case studies are automatically created using:

- Web search
- Large Language Models (LLMs)
- Embedding models
- Vector databases

**Key Components and Data Flow**

**1. AI Gateway**

- Acts as the interface between the system and the LLM.
- Uses prompt guards and evaluations to ensure quality control of generated content.

**2. Architecture Knowledge Ingestion Service**

- Fetches data from targeted web searches to specific sites and internal documents stored in object store.
- Performs data cleanup and transformation.
- Stores refined information in an Architecture Knowledge Base Vector Store.

**3. Case Study Preparation Service**

- Uses cleaned and structured data to generate new case studies.
- Passes case studies to the Case Study Maintenance Service.

**4. Case Study Maintenance Service**

- Maintains an updated repository of case studies in a Case Study Database.

**5. Aptitude Test Question Preparation Service**

- Generates MCQ-based aptitude test questions based on:
  - Existing knowledge from the vector store
  - LLM-generated insights
- Stores generated questions in the Aptitude Test Questions Database.

**6. Aptitude Test Maintenance Service**

- Maintains valid and updated aptitude test questions(MCQs and short answer questions) in an Aptitude Test Database.

**7. Expert User Interface & Admin API Gateway**

- Designated architect Experts can review and manage test questions, case studies.
- Connected via an Admin API Gateway.

### Flow Diagram

- **Description:** Flow involving chunking of documents, storing in vector store and retrieival by the expert Architect to update the tests
- **Diagram:**
![test 1 and test 2 content updates](/assets/New-test1-and-test2-questions.png "test 1 and test 2 content updates")

- Document Ingestion and Chunking: The process starts with ingesting documents (HTML, PDF, TXT) which are then broken down into smaller, manageable chunks. This is essential for processing large documents and ensuring relevant sections are used for question and case study generation. Chunking strategy discussed in [ADR](/ADRs/006-adr-architecture-knowledge-chunking-strategy.md).

- Embedding Generation and Vector Storage: The document chunks are fed into an embedding model, creating vector representations. These vectors, capturing the semantic meaning of the text, are stored in a vector store. This allows for efficient similarity searches later on.

- Knowledge Retrieval and LLM Interaction: When the Aptitude quesiton preparation service or case study preparation service requests a question or case study, the system queries the vector store to retrieve relevant document chunks based on semantic similarity. These chunks are then used as context for the Generative AI Model (LLM). The LLM processes this information to generate questions, case studies.

- Aptitude question preparation Service: For test1 MCQs and short answer questions, the system triggers Aptitude question preparation Service on a schedule or on demand. This service interacts with the LLM to generate questions and stores them in an Aptitude test questions database. These questions are pulled by Aptitude test maintenance service when designated expert architects tries to view them in User interface. Designated Expert Architects can drop or modify or add these questions to the tests. The tests are then stored in Aptitude test database

- Case Study preparation Service: For test 2 i.e case study-based exam, the system triggers Case Study preparation Service on a schedule or on demand. This service works in conjunction with the LLM to create case studies, which are then stored in a Case Study Database. These case studies are pulled by Case study maintenance service when designated expert architects tries to view them in User interface. Similar to questions, expert architects can edit, drop or include them in the test.

- Feedback Loop and Iteration: Both the question and case study generation processes involve expert review, allowing for feedback and improvement. The system can also learn from user interactions and refine its search and generation capabilities over time. This iterative process ensures the quality and relevance of the generated content[TBD].

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

- [**ADR 1 - Architecture documents chunking strategy**](/ADRs/006-adr-architecture-knowledge-chunking-strategy.md)

- [**ADR 2 - Strategy for generating new questions and case studies**](/ADRs/004-adr-new-questions-and-case-studies-strategy.md)

## Implementation Details

### **Gen AI Technical Components & Architecture**

- **Local Inference & Cloud Services:**
  - A cheap **cloud-based LLMs** such as gpt 4omini
- **Fine-Tuning & Adaptation:**
  - We don't need to fine tune our model as this is a generic usecase where we are accessing mostly public information about architecture
  patterns to come up with questions and case studies.
- **LLM Inference & Structured Outputs:**
  - Implementation of **structured response generation** for candidate feedback and grading justifications.
- **Prompt Engineering & Validation:**
  - **Dynamic prompt orchestration** for AI models ensuring contextual accuracy.
  - **Guardrails & validation mechanisms** to filter out misleading or biased responses. Strategy discussed in [Guardrials ADR](/ADRs/010-adr-llm-guardrails.md)
- **Information Retrieval & Search Engine:**
  - **Vector-based search** using embeddings to improve knowledge retrieval for generating new aptitude test questions and case studies.
  - **Search Engine** to retrieve latest architecture content including patterns, trends and techniques.
- **Observability & Performance Monitoring:**
  - **Prompt & model evaluation pipelines** discussed in [evals ADR](/ADRs/009-adr-llm-evaluation.md)
  - **LLM observability tools** to track model behavior and response drift. Discussed in [Observability ADR](/ADRs/011-adr-llm-observability.md)

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
