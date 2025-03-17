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

# **AI Components in the Architecture**  

## **1. AI Case Study Grader**  
- Uses **vector databases** to store and retrieve case study embeddings.  Refer to this [ADR](/ADRs/014-adr-llm-vector-store.md) for vector store and this [ADR](/ADRs/013-adr-llm-vector-search.md) for vector search  
- Evaluates architecture documents using specialized AI graders:  
  - **Content Segregator** (classifies document types)  
  - **ADR Grader** (assesses architectural decisions)  
  - **API Grader** (validates API contracts)  
  - **C4 Grader** (analyzes architecture diagrams)  
  - **DFD Grader** (evaluates data flow diagrams)  
  - **Infra/Security Grader** (checks infrastructure and security compliance)  

## **2. Data Pipeline Workflow**  
- Creates **embeddings** from case study documents for efficient AI processing. please refer to this [ADR](/ADRs/008-adr-llm-embedding-model.md)
- It also retrieves embeddings from reference architecture created while case study creation for better grading.  

## **3. AI Gateway**  
- Provides AI observability, logging, and security.  
- Manages **multi-LLM endpoints** to access different AI models.  
- Implements **prompt caching** and **guardrails** for AI responses.  
- Includes a **prompt firewall** to ensure safe and optimized AI queries.  

## **4. Foundation Models**  
- Integrates multiple AI models (e.g., OpenAI, Anthropic) to process and grade case study submissions.  

## **Purpose**  
The AI components **automate case study evaluation** by classifying, grading, and validating architecture documents using advanced **LLMs, vector databases, and embeddings**. 

- For the deployment of AI components refer to this [ADR](/ADRs/007-adr-llm-deployment.md)
- For the usage of AI Gateway refer to this [ADR](/ADRs/001-adr-using-ai-gateway.md)

### Data flow diagram:

![Test2 dataflow](/assets/casestudy-flow-diagram.png "Test2 dataflow")

- The architecture submissions are directly fed to document segregator, detailed analysis below
- The documents are then sent to document analyzer and AI grading system
- Software expert will act as Human in the loop, reviewing AI given grades 
- Rest of the dataflow remain the same, for email notifications and certification  

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
The output from content segregator is processed through various AI analyzers for each content document type. We have used multi model strategy for the same, refere to this [ADR](/ADRs/002-adr-ai-multi-model-strategy.md). All the interactions to the external foundational LLMs are done through an AI gateway, please refer to this [ADR](/ADRs/001-adr-using-ai-gateway.md). The Architecture is graded by AI through various benchmarking scores and submitted for manual review (Human in the loop).

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

## Case study Judge and Human in the loop

The Case study Judge is responsible for evaluating the quality of the AI-generated grading and provides a confidence score. Expert grader will review the AI generated confidence score and if it's low, expert will review the submission, following are detailed steps :

1. Retrieve a case study submission awaiting confidence score.
2. Use an external LLM to evaluate the confidence score of the case study grade given by other LLMs.
3. If the confidence score is low, human in the loop will kick in, expert grader will take over the submission.
4. Expert grader will flag inappropriate grading if any given by AI, this is then sent to vector store as feedback loop.
5. Once expert verifies all the grading, it is sent for final grade submission and then to certification database.
 

### Prompting strategy

These prompt templates utilize advanced prompting strategies such as role-specific prompting, chain-of-thought reasoning, critique-then-refine, and comparison-based assessment. Each section provides a detailed approach for accurate grading.  

<details>

<summary>Example prompt for evaluating case study(Click to expand)</summary>

## **1. ADRs (Architecture Decision Records) Evaluation**  

### **Prompt Template**  
📌 **Role-Specific Prompting:**  
> *"You are a highly experienced software architect specializing in decision-making frameworks. Your task is to evaluate an Architecture Decision Record (ADR) based on its clarity, completeness, tradeoff analysis, and impact assessment. Provide a structured analysis, scoring each criterion on a scale of 1-10, and justify the score with detailed reasoning."*  

📌 **Evaluation Criteria:**  
1. **Problem Definition (1-10):** Is the problem statement clear, well-defined, and relevant to the architectural context?  
2. **Alternatives Considered (1-10):** Are multiple viable options discussed, with pros and cons clearly stated?  
3. **Decision Justification (1-10):** Does the ADR provide a sound rationale for the decision made?  
4. **Tradeoffs & Consequences (1-10):** Does the document explore tradeoffs, risks, and potential consequences of the decision?  
5. **Alignment with Business & Technical Goals (1-10):** Does the decision align with organizational objectives and best practices?  

📌 **Scoring Example:**  
> *"The ADR presents a well-structured decision but lacks in-depth tradeoff analysis. While the problem is clearly defined (9/10), the alternatives could have been better justified (6/10). Overall, it scores 7.5/10."*  

📌 **Critique-then-Refine:**  
> *"Based on the initial assessment, suggest improvements to enhance the ADR’s clarity and decision-making process."*  

---

## **2. Business Requirement Document (BRD) Evaluation**  

### **Prompt Template**  

📌 **Role-Specific Prompting:**  
> *"As a senior software architect, evaluate the Business Requirement Document (BRD) for completeness, clarity, and feasibility. Your assessment should determine whether it effectively translates business needs into actionable technical requirements. Assign a score (1-10) for each criterion and justify your decision."*  

📌 **Evaluation Criteria:**  
1. **Requirement Clarity (1-10):** Are business requirements unambiguous, well-documented, and specific?  
2. **Functional vs. Non-Functional Requirements (1-10):** Are both clearly differentiated and adequately defined?  
3. **Alignment with Business Goals (1-10):** Does the BRD correctly reflect business objectives?  
4. **Feasibility & Technical Realism (1-10):** Are the requirements practical and achievable within technical constraints?  
5. **Completeness (1-10):** Does the document cover all necessary aspects (scope, risks, assumptions, constraints)?  

📌 **Comparison-Based Assessment:**  
> *"Compare this BRD to industry best practices. Identify areas where it falls short and suggest improvements."*  

📌 **Chain-of-Thought Breakdown:**  
> *"Step by step, analyze how each requirement is defined, its impact on development, and its feasibility."*  

---

## **3. C2 Diagrams (Container-Component Diagrams) Evaluation**  

### **Prompt Template**  
📌 **Role-Specific Prompting:**  
> *"You are evaluating a C2 (Container-Component) diagram for a complex software system. Your goal is to assess the clarity, accuracy, and completeness of the diagram. Provide a detailed breakdown, scoring each category (1-10), and suggest improvements where needed."*  

📌 **Evaluation Criteria:**  
1. **System Representation (1-10):** Does the diagram correctly depict system containers and components?  
2. **Labeling & Notation (1-10):** Are elements labeled correctly and do they follow industry standards?  
3. **Clarity & Readability (1-10):** Can the architecture be understood easily without additional documentation?  
4. **Component Interaction (1-10):** Does the diagram accurately depict interactions between components?  
5. **Alignment with Intended Architecture (1-10):** Does it match the described architecture model?  

📌 **Critique-then-Refine Prompting:**  
> *"What ambiguities exist in the diagram, and how can they be resolved? Suggest improvements to make it more readable and accurate."*  

📌 **Counterfactual Prompting:**  
> *"If a certain component were removed or modified, how would the architecture behave differently?"*  

---

## **4. Security & Infrastructure Evaluation**  

### **Prompt Template**  
📌 **Role-Specific Prompting:**  
> *"Assess the security and infrastructure design of this software system. Evaluate adherence to security best practices, scalability, fault tolerance, and compliance requirements. Provide a security risk assessment and suggest necessary improvements."*  

📌 **Evaluation Criteria:**  
1. **Authentication & Authorization (1-10):** Are robust security measures (RBAC, OAuth, etc.) in place?  
2. **Data Encryption & Privacy (1-10):** Are data protection measures like encryption (TLS, AES) implemented?  
3. **Infrastructure Scalability & Resilience (1-10):** Can the system handle high loads and failures gracefully?  
4. **Compliance with Standards (1-10):** Does it adhere to GDPR, ISO 27001, or other security regulations?  
5. **Logging & Monitoring (1-10):** Are logging, auditing, and alert mechanisms effectively implemented?  

📌 **Comparison-Based Assessment:**  
> *"How does this security model compare to industry benchmarks? Identify vulnerabilities and propose mitigation strategies."*  

📌 **Critique-then-Refine Prompting:**  
> *"Highlight the most critical security gaps and refine the infrastructure to improve resilience."*  

---

## **5. Data Flow Diagrams (DFDs) Evaluation**  

### **Prompt Template**  
📌 **Role-Specific Prompting:**  
> *"You are reviewing a Data Flow Diagram (DFD) for a software system. Evaluate its accuracy, completeness, and security considerations. Ensure that all data sources, transformations, and storage locations are correctly represented."*  

📌 **Evaluation Criteria:**  
1. **Correctness & Completeness (1-10):** Are all key data elements correctly represented?  
2. **Security & Privacy Considerations (1-10):** Does the DFD show how sensitive data is handled securely?  
3. **Clarity & Readability (1-10):** Can stakeholders easily interpret data movements?  
4. **Process-Data Interaction (1-10):** Are all transformations and interactions correctly represented?  
5. **Alignment with Business Logic (1-10):** Does the diagram reflect the actual data requirements of the system?  

📌 **Counterfactual Prompting:**  
> *"If an unauthorized user were to intercept a data flow in this system, what would be the impact? How can this be mitigated?"*  

📌 **Critique-then-Refine Prompting:**  
> *"Where does the DFD fail to illustrate key security aspects? Suggest modifications to enhance clarity and security."*  

---

## **Final Notes on Prompting Strategies**  
To ensure **accurate, unbiased grading**, use:  
✅ **Role-specific prompts** to guide evaluations  
✅ **Explicit scoring rubrics** to provide objective feedback  
✅ **Step-by-step chain-of-thought** reasoning for deeper insights  
✅ **Comparison-based assessment** to benchmark against best practices  
✅ **Critique-then-refine prompting** to iteratively improve evaluation  

These detailed prompt templates will help in **precise, structured, and high-quality** grading of software architecture case studies. Let me know if you need modifications! 🚀  
</details>

## Conclusion
- **Summary of Changes:** 
  - Automated content segregation categorizes different artifacts in candidate submissions.
  - AI-assisted benchmarking provides structured evaluation against predefined grading criteria.
  - Human-in-the-loop (HITL) validation ensures AI-graded scores align with expert expectations.
- **Benefits of the New Architecture:** Increased scalability, faster turnaround, and reduced manual workload.
  - Efficient Case Study Evaluation – Reduces grading workload while maintaining assessment depth.
  - Consistency in Scoring – AI-driven grading mitigates expert subjectivity in evaluations.
  - Scalability – Supports increased candidate volumes without compromising grading accuracy.
- **Potential Risks & Mitigations:**
  - Complexity of Architecture Grading – AI models trained on real-world architectural patterns to ensure comprehensive evaluations.
  - Over-Reliance on Automation – Human experts retain final decision-making authority on ambiguous or complex submissions.
  - Security & Compliance – AI processing ensures data privacy, aligning with regulatory standards like GDPR and ISO 27001.
