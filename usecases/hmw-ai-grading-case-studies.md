# Grading case studies

## Primary Goal

**HMW implement AI-driven grading models for expert architects so that they can evaluate case study submissions 4X faster?**

## Challenges in Expansion Plans

- The current **manual grading process** for Test 2 case study submissions is **slow, expensive, and unscalable**.
- Each submission requires **8 hours** of expert evaluation. With the planned **5-10X expansion** ( 2000 new candidates per week), the number of Test 2 evaluations is expected to reach **1,200-1,500 candidates per week** on average. This would result in a **grading workload of 9,600-12,000 hours per week**, far exceeding the capacity of available experts.
- The **$960K-$1.2M per week** cost of manual grading makes scaling financially unsustainable.
- Grading inconsistencies, including negative bias (grading lower than deserved) that may harm candidates and positive bias (grading higher than deserved) that may impact Certifiable, Inc., contribute to scoring variability and delays in feedback, ultimately affecting the candidate experience.

## Problem Statement & Scope

- The current manual grading process for Test 2 is unsustainable, requiring **8 hours per candidate**, making it infeasible to support the projected **5-10X growth in applicants**.
- **Generative AI** will automate grading while ensuring **scalability, accuracy, cost-effectiveness, and efficiency**, maintaining expert-level evaluation quality as mentioned in the main readme.md.
- **Cost-effectiveness** – AI-driven grading must be **less than the current $960K-$1.2M per week manual grading budget**.
- **Productivity** – The solution must **improve grading efficiency by at least 4X** to meet scaling demands and expert workload constraints.

### Requirements for AI-Driven Grading System:

- **Automated Grading Pipeline** – AI models must evaluate case study responses based on predefined scoring criteria.
- **Human-in-the-loop (HITL) validation** – Experts must oversee AI grading and refine models for continuous improvement.
- **Structured Feedback Generation** – AI must provide **detailed explanations and justifications** for grading decisions.
- **Confidence-Based Expert Review** – AI must flag low-confidence evaluations for expert validation.
- **Adaptive Learning Mechanism** – AI models must continuously improve based on expert corrections and evolving certification criteria.
- **Security & Compliance** – AI must handle grading data with strict **privacy and security protocols**.

## Assumptions

### Business Assumptions

- The **evaluation process and scoring criteria** are linked to the detailed [Test 2 Requirements Document](/business-requirements/test2-grading-process.md).
- AI-driven automation **must not impact certification credibility**, ensuring continued recognition across industry standards.

### Technical Assumptions

- **Grading data is structured**, with predefined evaluation criteria used by human experts.
- **Current workflows include manual review interfaces** used by expert architects to evaluate responses and provide feedback.
- **Historical grading records are available**, which can be used for AI model training.
- The **existing certification system operates under strict security and compliance standards** such as **GDPR and ISO 27001**.
- The **architecture must allow AI-driven grading to integrate as a modular service** without disrupting existing workflows.
- **Response evaluation logic is well-documented**, ensuring AI implementation aligns with established grading methodologies.

## New User Journey / Golden Path using Jobs to be Done Framework

**Persona:** [Alex, Expert Architect](/business-requirements/exper-architect-persona.md)

**Main Job:** Evaluate and grade case study submissions efficiently across multiple artifacts.

**Backstory:** After completing their primary architectural work, Alex is assigned to evaluate Test 2 case study submissions for **4-5 candidates per week**. With limited time available, Alex relies on AI-assisted grading to enhance efficiency and ensure consistency in evaluations across five key submission artifacts.

**End Goal of the Main Job:** Ensure fair, structured, and expert-level grading of case study submissions while reducing the grading workload and maintaining high evaluation standards.

**Job Steps (using universal job map):**
1. **View candidate submissions** – Access all case study artifacts.
2. **Review system-generated scoring for each artifact** – Ensure AI-assigned scores align with grading criteria.
3. **Assess system-generated reasoning** – Verify AI explanations for grading decisions.
4. **Modify the system-generated assessment** – Adjust AI evaluations where necessary.
5. **Adjust final score if required** – Confirm that scores reflect accurate assessment.
6. **Generate structured feedback reports** – Provide candidates with AI-assisted, expert-reviewed feedback for each artifact.
7. **Modify feedback reports if necessary** – Ensure clarity and relevance before submission.
8. **Submit final evaluation results** – Confirm scores and update certification records for candidate progression.


**High-Level User Flow:** [UI Mockup](https://claude.site/artifacts/f0f8e1fc-f904-4f28-9466-125f77e69127?fullscreen=true)

![Test2 grading UI screen](/assets/Test2-grading.png)


  
## Architecture Grading Review:
Once the grading is done by AI, software expert reviews the grading in this step instead of manually reviewing, this will save atleast 50-70% of the time spent by them. If the expert wishes to override the grading, they can and the final grading is fed back to AI data pipelines as they continously evolve for more accurate results.

### C2 Architecture diagram:

![Test2 case study](/assets/test2c2.png "Test2 case study")


### Data flow diagram:

![Test2 dataflow](/assets/casestudy-flow-diagram.png "Test2 dataflow")

## Architectural Decision Records (ADRs)
- **ADR 1 - Title:**
  - **Context:**
  - **Decision:**
  - **Consequences:**

- **ADR 2 - Title:**
  - **Context:**
  - **Decision:**
  - **Consequences:**

## Implementation Details

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

## Conclusion
- **Summary of Changes:** AI-driven automation for grading, feedback, and certification content updates.
- **Benefits of the New Architecture:** Increased scalability, faster turnaround, and reduced manual workload.
- **Potential Risks & Mitigations:** AI bias monitoring, human oversight mechanisms, and periodic model retraining.
- **Next Steps:** Pilot AI grading system, evaluate AI explainability, and refine model accuracy based on real-world data.
