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

