## Architecture characteristics Analysis

### AI Usecases

1. *Implement AI-driven grading models for expert architects so that they can evaluate short-answer submissions 4X faster.*
   * Initial Thoughts:
      * Use an LLM to grade the candidate's short answer submissions. Provide a pre-determined set of rules, reference answer
      and previously human graded Q&As as retrieval context. High-confidence evaluations can be finalized, while low-confidence ones can be further reviewed by expert architects.
   * NFRs:
     * **Accuracy** - The system must grade the short answers with accuracy levels equivalent to that of manual grading performed by expert software architects.
     * **Explainability** - The system should provide accurate reasoning for the grades and evaluation so as to be able to pass on the feedback to candidates.
     * **Scalability** - The system should handle increasing numbers of short answer submissions efficiently without performance degradation.
     * **Security** - The system must ensure secure handling of candidate submissions, preventing unauthorized access and ensuring data integrity.
     * **Privacy** – The system must comply with data protection regulations, ensuring that candidate responses and grading results are stored and processed securely without exposing personal information.


2. *Implement AI-driven grading models for expert architects so that they can evaluate case study submissions 4X faster?*
   * Initial Thoughts:
      * Use a multi-model strategy to grade each section of case study submission separately preferrably with a different architecture pattern for each section depending on the applicability. For e.g - Fine tuned LLM for C4 diagrams and RAG for design document. 
   * NFRs:
     * **Scalability** - The system must support large-scale evaluation of case studies without degradation of performance.
     * **Explainability** - The system should provide accurate reasoning for the grades and evaluation so as to be able to pass on the feedback to candidates
     * **Accuracy** - The system must grade the case studies with accuracy levels equivalent to that of manual grading performed by expert software architects.
     * **Evolvability** - The architecture should allow for continuous improvements, such as refining grading models or incorporating new evaluation techniques.
     * **Security** - The system must ensure secure handling of candidate submissions, preventing unauthorized access and ensuring data integrity.
     * **Privacy** – The system must comply with data protection regulations, ensuring that candidate responses and grading results are stored and processed securely without exposing personal information.

3. *Automate the identification of emerging software architecture trends and generate expert-level certification questions to assist architects in updating the certification database efficiently*
   * Initial Thoughts:
      * Use a web search + RAG LLM architecture to ingest the latest architecture trends via targeted searches, storing them in a vector database with semantic chunking. Questions are generated on demand or on a schedule by passing pre-configured prompts and relevant context to the LLM. Expert architects review and approve the questions before inclusion in tests.
   * NFRs:
     * **Workflow** - The pipeline should ensure seamless automation of architecture knowledge ingestion, question generation, and expert validation, minimizing manual effort and maintaining consistency.
     * **Accuracy** – The generated questions must be factually correct and aligned with real-world architectural trends to ensure their relevance and reliability.
     * **Evolvability** - The system should adapt to new architecture patterns and changing industry standards over time.
     * **Observability** - The platform should provide monitoring and logging capabilities to track trends, question quality, and system performance.
     * **Security** – The system must ensure secure ingestion, storage, and processing of architecture trends and generated questions, protecting against unauthorized access, data tampering, and leakage of proprietary or sensitive information.


### Requirements vs NFRs  

| Given Requirements | Top 3 NFRs |  
|--------------------|------------|  
| Implement AI-driven grading models for expert architects to evaluate short-answer submissions 4X faster. | Accuracy, Explainability, Scalability |  
| Implement AI-driven grading models for expert architects to evaluate case study submissions 4X faster. | Scalability, Explainability, Accuracy |  
| Automate the identification of emerging software architecture trends and generate expert-level certification questions. | Workflow, Accuracy, SecuritEvolvability |  
