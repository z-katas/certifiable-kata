#Test 2 AI automation

This document highlights the process of automating the case study in test 2 using multi model strategy

## Highlevel details from given for test 2

- Number of candidates taking exam per week: 200
- Score required to pass test 2: 80%
- Number of hours spent by Expert Architect to review the case study: 8 hours
- Expected increase in growth: 5-10X
  

Assumptions:
-------------
A typical architecture submission of a case study involves the following documents

| 🗂 Document Type     | ⭐ Document Name               | 📋 Purpose |
|---------------------|-----------------------------|------------|
| **Business Docs**   | BRD                          | Define business goals & user needs |
|                     | FRS                          | Define functional features & use cases |
|                     | NFRs                         | Define performance, security, and compliance needs |
| **Design Docs**     | ADRs                         | Justify architectural choices |
|                     | HLAD / SDD                   | Define high-level system design |
|                     | C4 Model Diagrams           | Visualize system architecture |
|                     | DFDs                         | Show data flow & dependencies |
|                     | Sequence Diagrams           | Show process flow in interactions |
|                     | API Contracts               | Define API structure and behavior |
|                     | Infra & Security Docs       | Define cloud infrastructure, security, and compliance |
| **Implementation Docs** | CI/CD & DevOps Strategy  | Define deployment pipelines & best practices |
|                     | Performance Reports         | Measure system scalability & speed |
|                     | DR & BCP                     | Plan for failures & recovery |
|                     | Migration Plan              | Ensure smooth transitions between architectures |
|                     | Knowledge Base              | Assist in onboarding & troubleshooting |

- Number of candidates that pass the first test (per week)- 60% = 120 (current)
- Number of candidates will increase 10X, so the system will handle 1200 candidates per week
- With Human in the loop, Expert only has grade those documents which needs it, rest all are autograded by AI using below strategy
- Estimated reduction in number of hours spent by expert in short term - 50% = 4 hours
- Estimated number of additional Experts needed for 10X growth = (10*200) * (0.5) = 1000 (5X growth in resources for short term)
- AI can auto reject very low graded scores for sections to be overall reject, this can save additional 10% of time for expert, so overall ideal number of experts needed for 10X growth is approx ~ 900.

Document Segregator:
--------------------
Once the system receives the submission, it needs a content segregator where the content is segregated into various document types like mentioned above. Once the content is segregated, it is sent to analyzer. 

## **Step 1: Data Preprocessing**  
Before applying AI, prepare the documents:  
✅ **Extract text** from PDFs, Word, and other formats using tools like PyMuPDF, Apache Tika, and Textract.  
✅ **Clean and normalize** the text by removing special characters, stopwords, and redundant spaces.  
✅ **Metadata extraction** to analyze file properties like author, date, or document type.  

---

## **Step 2: Choose an AI-Based Classification Strategy**  

### **1️⃣ NLP + Clustering (For Unstructured Documents with No Labels)**  
- **Use Case:** When there are no predefined categories.  
- **How it Works:** Uses embeddings (like OpenAI, BERT, or SBERT) with clustering algorithms (K-Means, DBSCAN) to group similar documents.  
- **AI Tools:** OpenAI Embeddings, SBERT, Hugging Face Models  

### **2️⃣ Fine-Tuned AI Model (For Industry-Specific Categorization)**  
- **Use Case:** When categories are predefined (e.g., BRD, API Contracts, ADRs).  
- **How it Works:** Fine-tunes a transformer model (like GPT-4, BERT) on labeled datasets to classify documents accurately.  
- **AI Tools:** Hugging Face Transformers, OpenAI Fine-tuning, T5 Model  

### **3️⃣ Retrieval-Augmented Generation (RAG) (For Context-Aware Segregation)**  
- **Use Case:** When segregation requires cross-referencing existing knowledge bases.  
- **How it Works:** Uses a vector database (like Pinecone, FAISS) to store document embeddings and retrieve relevant context dynamically.  
- **AI Tools:** LangChain, Pinecone, ChromaDB  

### **4️⃣ Rule-Based Classification (For Well-Structured Documents)**  
- **Use Case:** When document formats are consistent.  
- **How it Works:** Uses regex and keyword-based classification to assign categories based on predefined rules.  
- **AI Tools:** SpaCy, Regex, NLP Pipelines  

### **5️⃣ Agentic AI (For Autonomous Categorization & Workflow Automation)**  
- **Use Case:** When AI needs to make categorization decisions dynamically and adapt to new patterns.  
- **How it Works:** Uses multi-agent AI to analyze, classify, and refine document categories autonomously.  
- **AI Tools:** OpenAI Agents, AutoGPT, CrewAI  

---

## **Best AI Tool Recommendations for content segregation**
| Strategy        | Best AI Tools |
|----------------|--------------|
| NLP + Clustering | OpenAI Embeddings, SBERT, Hugging Face, K-Means |
| Fine-Tuned AI | Hugging Face Transformers, OpenAI Fine-tuning |
| RAG | Pinecone, LangChain, ChromaDB |
| Rule-Based | SpaCy, Regex, NLP Pipelines |
| Agentic AI | AutoGPT, CrewAI, BabyAGI |

---

### **Final Thoughts**
- **If documents are structured** → Use **rule-based classification**  
- **If categories are unknown** → Use **NLP + clustering**  
- **If documents require domain expertise** → Use **fine-tuned AI models**  
- **If context retrieval is important** → Use **RAG**  
- **If you need an autonomous system** → Use **Agentic AI**  


Document Analyzer:
--------------------
The output from content segregator is processed through various AI analyzers for each content document type. We have used multi model strategy for the same, refere to this [ADR](/ADRs/adr-ai-multi-model-strategy.md). All the interactions to the external foundational LLMs are done through an AI gateway, please refer to this [ADR](/ADRs/adr-using-ai-gateway.md). The Architecture is graded by AI through various benchmarking scores and submitted for manual review (Human in the loop).

# AI Evaluation Strategy for Case Study Documents

Each document in the case study will be evaluated using different AI architecture patterns. The overall architecture follows a multi-model strategy.

## **Business Docs**

### **BRD (Business Requirements Document)**
- **Architecture pattern recommended:** Retrieval-Augmented Generation (RAG)
- **Explanation:** BRDs require retrieval from various business sources, policies, and past documentation to ensure completeness and consistency.
- **Tradeoffs:** Requires high-quality retrieval sources; may generate incorrect responses if sources are weak.
- **Mitigation strategies:** Implement domain-specific document retrieval and fact verification.
- **AI tools:** OpenAI API (RAG implementation), LangChain, Pinecone

### **FRS (Functional Requirements Specification)**
- **Architecture pattern recommended:** Prompt Engineering
- **Explanation:** Well-structured prompts help in extracting functional requirements efficiently by guiding AI to focus on specific system features.
- **Tradeoffs:** Performance depends on prompt quality; may miss edge cases.
- **Mitigation strategies:** Iterative refinement of prompts and human-in-the-loop validation.
- **AI tools:** OpenAI GPT, Anthropic Claude, PromptLayer

### **NFRs (Non-Functional Requirements)**
- **Architecture pattern recommended:** Fine-Tuning
- **Explanation:** Non-functional requirements often require historical performance and compliance data, making a fine-tuned model ideal for consistency and precision.
- **Tradeoffs:** Requires labeled datasets; can be expensive to train.
- **Mitigation strategies:** Use a mix of zero-shot and fine-tuned approaches; leverage synthetic data generation.
- **AI tools:** OpenAI fine-tuning, Hugging Face Transformers

## **Design Docs**

### **ADRs (Architectural Decision Records)**
- **Architecture pattern recommended:** Agentic AI
- **Explanation:** ADRs require AI to evaluate multiple trade-offs and simulate the impact of decisions over time, making autonomous agents useful.
- **Tradeoffs:** Complexity in orchestration; may require multiple agents for different perspectives.
- **Mitigation strategies:** Use modular agents with a clear decision hierarchy.
- **AI tools:** AutoGPT, BabyAGI, CrewAI

### **HLAD / SDD (High-Level Architecture Design / Software Design Document)**
- **Architecture pattern recommended:** RAG
- **Explanation:** Architectural designs must align with best practices and prior designs, requiring retrieval of relevant patterns and documentation.
- **Tradeoffs:** Knowledge base must be well-structured and continuously updated.
- **Mitigation strategies:** Regular updates to the knowledge source and semantic search optimization.
- **AI tools:** LangChain, ChromaDB, Vector Databases

### **C4 Model Diagrams**
- **Architecture pattern recommended:** Fine-Tuning
- **Explanation:** AI needs to generate diagrams based on previous architecture patterns, requiring a fine-tuned model trained on architecture visuals.
- **Tradeoffs:** Model needs large-scale labeled diagram datasets.
- **Mitigation strategies:** Use transfer learning and domain adaptation.
- **AI tools:** Graph Neural Networks, Diagrams.net + AI augmentation

### **DFDs (Data Flow Diagrams)**
- **Architecture pattern recommended:** Prompt Engineering
- **Explanation:** DFDs can be generated using structured prompts that describe entities, flows, and interactions clearly.
- **Tradeoffs:** Complexity increases with larger systems.
- **Mitigation strategies:** Define structured prompts for accuracy.
- **AI tools:** OpenAI GPT, Mermaid.js, PlantUML

### **Sequence Diagrams**
- **Architecture pattern recommended:** Prompt Engineering
- **Explanation:** Sequence diagrams focus on event flows, which can be efficiently created using structured AI-driven prompt-based visualization tools.
- **Tradeoffs:** Difficult to capture intricate dependencies.
- **Mitigation strategies:** Use structured templates for diagram generation.
- **AI tools:** Mermaid.js, PlantUML

### **API Contracts**
- **Architecture pattern recommended:** Agentic AI
- **Explanation:** API contracts require AI to generate, validate, and refine structured documentation autonomously.
- **Tradeoffs:** Needs structured API documentation.
- **Mitigation strategies:** Use specialized agents for API design and testing.
- **AI tools:** Postman AI, Swagger Auto-Doc

### **Infra & Security Docs**
- **Architecture pattern recommended:** Fine-Tuning
- **Explanation:** Security and infrastructure require AI models trained on compliance and infrastructure best practices.
- **Tradeoffs:** Sensitive data handling is required.
- **Mitigation strategies:** Use redacted datasets and controlled access.
- **AI tools:** Hugging Face Transformers, OpenAI fine-tuning

## **Implementation Docs**

### **CI/CD & DevOps Strategy**
- **Architecture pattern recommended:** Agentic AI
- **Explanation:** CI/CD strategies involve complex automation and optimization, which can be handled by AI agents.
- **Tradeoffs:** High dependency on dynamic pipelines.
- **Mitigation strategies:** Implement monitoring agents.
- **AI tools:** GitHub Actions AI, Harness AI

### **Performance Reports**
- **Architecture pattern recommended:** RAG
- **Explanation:** Performance analysis needs retrieval of benchmarking data, logs, and past reports for effective insights.
- **Tradeoffs:** Performance varies with real-time data availability.
- **Mitigation strategies:** Use caching and real-time benchmarking.
- **AI tools:** Datadog AI, Splunk AI

### **DR & BCP (Disaster Recovery & Business Continuity Plan)**
- **Architecture pattern recommended:** Fine-Tuning
- **Explanation:** Disaster recovery scenarios require AI trained on historical outage responses and risk assessments.
- **Tradeoffs:** Requires diverse failure scenarios.
- **Mitigation strategies:** Simulate multiple disaster scenarios.
- **AI tools:** OpenAI fine-tuning, AWS Resilience Hub

### **Migration Plan**
- **Architecture pattern recommended:** Prompt Engineering
- **Explanation:** Migration planning can be guided with AI using structured workflows and predefined rules.
- **Tradeoffs:** Limited flexibility in complex migrations.
- **Mitigation strategies:** Use interactive prompt workflows.
- **AI tools:** OpenAI GPT, Miro AI

### **Knowledge Base**
- **Architecture pattern recommended:** RAG
- **Explanation:** A knowledge base needs real-time retrieval and augmentation for contextual responses.
- **Tradeoffs:** Knowledge must be updated frequently.
- **Mitigation strategies:** Implement real-time knowledge updates.
- **AI tools:** Chatbot AI (e.g., OpenAI Assistants), Confluence AI

---
This structured AI evaluation ensures that each document is assessed using the best-suited AI architecture pattern while accounting for trade-offs and mitigation strategies.

Each document in the case study will be evaluated using different AI architecture patterns. The overall architecture follows a multi-model strategy.


AI Architecture Grading process
--------------------------------

Each candidate must submit the following artifacts as part of Test 2. Each artifact is evaluated based on specific criteria, and justification for assigned scores is provided.

### Functional & Non-Functional Requirements Definition (Weight: 20%)
- **Completeness of functional requirements (40%)**: Are all necessary functional aspects captured?
- **Alignment with business goals (30%)**: Do the requirements support the intended business objectives?
- **Clarity and prioritization of non-functional requirements (20%)**: Are performance, security, scalability, and maintainability considerations explicitly defined?
- **Mapping of non-functional attributes to architectural decisions (10%)**: Are the constraints and trade-offs well-documented?

### Component-Level Architecture & Event Storming Model (Weight: 20%)
- **Clarity in component identification (30%)**: Are system components clearly defined and modular?
- **Correctness of event interactions (30%)**: Are events properly mapped between components?
- **Alignment with system objectives (25%)**: Do the interactions reflect the intended system behavior?
- **Use of event storming best practices (15%)**: Are domain events structured logically and sequentially?

### Architectural Pattern Selection & Justification (Weight: 20%)
- **Suitability for the problem domain (35%)**: Is the chosen architectural pattern appropriate for the case study?
- **Trade-off analysis (30%)**: Does the justification cover key trade-offs (e.g., performance vs. scalability)?
- **Comparison with alternative patterns (20%)**: Are alternatives considered before finalizing a selection?
- **Alignment with non-functional constraints (15%)**: Does the chosen pattern support expected system constraints?

### C2 (Context & Container) Diagram (Weight: 20%)
- **Accuracy of system boundaries (35%)**: Are external and internal components clearly distinguished?
- **Completeness of inter-component communication (30%)**: Do container interactions depict system data flow correctly?
- **Consistency with chosen architecture pattern (20%)**: Does the diagram align with the selected architectural approach?
- **Use of standard notations (15%)**: Is the diagram presented using a structured, industry-standard format?

### Architectural Decision Records (ADRs) (Weight: 20%)
- **Clarity and justification of decisions (40%)**: Are trade-offs clearly documented?
- **Impact analysis (30%)**: Does the ADR explain the long-term impact of decisions?
- **Consideration of future evolution (20%)**: Are flexibility and adaptability addressed?
- **Consistency with functional & non-functional requirements (10%)**: Do ADRs align with system goals?

Architecture Grading Review:
----------------------------
Once the grading is done by AI, software expert reviews the grading in this step instead of manually reviewing, this will save atleast 50-70% of the time spent by them. If the expert wishes to override the grading, they can and the final grading is fed back to AI data pipelines as they continously evolve for more accurate results.

C2 Architecture diagram:
------------------------


![Test2 case study](/assets/test2c2.png "Test2 case study")


Data flow diagram:
------------------------


![Test2 dataflow](/assets/casestudy-flow-diagram.png "Test2 dataflow")

