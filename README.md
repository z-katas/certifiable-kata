 ![Cover picture](/assets/readme-cover-picture-latest.svg "cover picture")

# ZAItects - Certifiable, Inc | O'Reilly Architectural Katas (Winter 2025)

A structured approach to the **O'Reilly Winter 2025 Architectural Kata Challenge**.

## Table of Contents
- [Team](#team)
- [Introduction](#introduction)
  - [Background & Context](#background--context)
  - [Expansion Plans](#expansion-plans)
  - [Current Certification Process](#current-certification-process)
  - [Challenges in Expansion Plans](#challenges-in-expansion-plans)
  - [Key Objectives](#key-objectives)
    - [Non-Functional Attributes](#non-functional-attributes)
- [Automation use-cases using Gen AI](#automation-use-cases-using-gen-ai)
- [Architecture characteristics](#architecture-characteristics) 
- [Final thoughts](#final-thoughts)  

 

## Team
 ![Team](/assets/team.png "team")
- [**Avinash**](https://www.linkedin.com/in/avinashmarepalli/) , Senior Tech lead
- [**Saketh Kumar**](https://www.linkedin.com/in/saketh-kumar-27b124126/) , Associate Architect
- [**Srikanth**](https://www.linkedin.com/in/koraveni-srikanth/) , Senior Tech lead
- [**Shashank**](https://www.linkedin.com/in/shashank-sheela-740746b4) , Technical Product Manager
- [**Vijayakumaran**](https://www.linkedin.com/in/vijayakumaran-c-v/) , UX designer

**Check [Glossary](business-requirements/glossary.md) to understand more about certain terms.**


# Problem defintion

## Introduction

The **Software Architecture Licensing Board (SALB)** was formed in the U.S. to regulate and accredit software architecture certification providers. Like doctors and lawyers, IT professionals must obtain official certifications to practice as software architects.

Certifiable Inc., a leading accredited provider in the US, certifies **200 candidates** per week with **300 expert architects** grading the tests."

With new legislation requiring certifications in the UK, Europe, and Asia, demand is set to **surge by 5-10X**. These regions will rely on U.S.-based companies, like Certifiable Inc., to manage certifications, each priced globally at **$800**, as standardized by SALB


## Current Certification Process

Certifiable Inc.'s certification process includes two tests. **Test 1 (Aptitude Test)** consists of auto-graded multiple-choice questions and **manually graded short answers**, **taking 3 hours per candidate** and completed within a week. 

Candidates scoring 80% or higher advance to **Test 2 (Architecture Submission)**, where they submit a case study **manually graded by expert architects** that takes **8 hours per candidate**.

Failed candidates receive detailed feedback, while successful ones are added to the certification database, allowing employers to verify credentials via the SoftArchCert portal.

## Challenges in Expansion Plans
 
- **New demand estimates:**
  - Expanding from **200 per week** to **1,000 - 2,000 per week**, with a **21% projected increase over four years**.
  - **Test 1 short answers:** **6,000 expert hours per week** & **Test 2 case study review:** **12,800 expert hours per week** (assuming 80% move forward).
  - **Total workload:** ~**19,000 expert hours per week**
- **Expert workload:**
  - Even if current experts work **18 hours/week**, capacity reaches 5,400 hrs/week, **still 3.5X lower than** required.
  - Need at least **550 experts** who can work **35 hrs average per week** on to meet the new demand.
  - 1-week TAT for each test requires parallel grading, posing operational challenges.
  
  ![New workload](/assets/demand-chart.png "new workload")
  
- **Cost Burden:**
  - Manual grading would cost over **$1M+ per week ($50/hour X 19,000+ hours)**
  - Each candidate’s evaluation requires 11 hours of expert review, costing **$550 per license (68% of the $800 certification fee)**
- **Grading inconsistencies & Fraud detection:**
  - Inconsistent manual grading can lead to **negative bias (unfair penalties)** or **positive bias (unqualified certifications)**, impacting **credibility**.
  - Lack of automated **fraud detection** increases the risk of impersonation, answer manipulation, and certification fraud, threatening **exam integrity**.
- **Other manual processes:**
  - Provide detailed feedback to failed candidates via email.
  - Analyze, review, and update certification tests based on candidate performance trends.
  - Incorporate new industry techniques, practices, and patterns into certification content.
  - Modify and create new case studies for Test 2 to maintain exam integrity and prevent leaks.

## Key Objectives

“How might we **adopt Generative AI** to automate manual processes for expert architects so that their **productivity** is increased, **operational costs** are reduced, and **overall efficiency** is significantly improved to confidently handle a 10X growth in candidate demand?”

### Constraints
These are some constraints explicitly mentioned in the requirement.

- **Seamless Integration:** *Seamlessly integrate AI-driven components into the existing system, ensuring compatibility, scalability, and minimal disruption to current operations.*
- **Scalability:** *As the software architecture industry is projected to grow by 21% globally and certification demand increases 5-10X, the system must scale to accommodate the surge in applicants.*
- **Cost Efficiency:** *AI implementation costs must be optimized to prevent overruns while supporting Certifiable, Inc.'s strategic expansion. AI adoption should not exceed a 30% increase in grading expenses.*
- **Accuracy:** *As a market leader, Certifiable, Inc. must maintain grading precision. Inaccurate evaluations could impact candidate careers and damage the company’s reputation.* 
- **Credibility:** *Certification credibility is critical—misleading exams or inconsistent grading can undermine employer trust and industry acceptance.*

# Solution

## Business outcomes achieved
- 5.5x Increase in expert process capacity
- 68% Lower cost per certification
- 85% Reduction in manual review requirements

## Automation use-cases using Gen AI 
   We priortized 3 use-cases for this excercise

  ![HMW](/assets/how-might-we.jpg "HMW")

## Non-functional characteristics
   <IMAGE>

## Detailed designs of usecases
  
- ### **HMW implement AI-driven grading models for expert architects so that they can evaluate short-answer submissions 4X faster?**
  
  Refer [**detailed design details**](usecases/hmw-ai-grading-short-answers.md) of this usecase

  **Solution approach:** The evaluation of short answers in test1 can be automated using an LLM based system. The system can perform **a RAG that uses existing historical correct** and incorrect answers along with candidate's answer as **context to LLM to output the grade**. Evaluations with confidence score more than a pre-defined threshold are considered final whereas the ones below are further processed by expert architects. The new approach allows for the output of the platform to scale to meet the expected growth while ensuring the results closely mimic manual grading. **Splitting the Grader and Judge into separate components**([**ADR**](/ADRs/adr-llm-based-short-answer-evalaution-strategy.md)) allows us to improve/test one component while keeping the other component constant.



  **C2 Diagram:**

  ![ASAS Grader C2 Diagram](/assets/test1-grader-c2.jpg "ASAS Grader C2 Diagram")

- ### **HMW implement AI-driven grading models for expert architects so that they can evaluate case study submissions 4X faster?**
  
  Refer [**detailed design details**](usecases/hmw-ai-grading-case-studies.md) of this usecase

  **Solution approach:** The AI-driven grading system for Test 2 is designed to handle the scalability and complexity of evaluating case study submissions. The process begins with **automated content segregation**, where different artifacts such as requirements, architectural   
   decisions, and diagrams are categorized for structured evaluation. **A multi-model AI strategy**([**ADR**](/ADRs/adr-ai-multi-model-strategy.md)) is employed to assess each artifact using **specialized AI analyzers**, ensuring grading consistency and accuracy. The system leverages an **AI gateway**([**ADR**](/ADRs/adr-using-ai-gateway.md)) to securely interact with the LLMs.
  
  **C2 Diagram:**

  ![Test2 case study](/assets/test2c2.png "Test2 case study")

- ### **HMW automate the identification of emerging software architecture trends and generate expert-level certification questions to assist architects in updating the certification database efficiently?**
  
  Refer [**detailed design details**](usecases/hmw-ai-content-updates.md) of this usecase
  
  **Solution approach:** The generaton of new questions in test 1 and case studies in test 2 can be automated using a **web search + RAG LLM architecture pattern** ([**ADR**](/ADRs/adr-new-questions-and-case-studies-strategy.md)). Latest architecture techniques, patterns and trends are ingested with targeted web search and stored in a vector store following **semantic chunking**([**ADR**](/ADRs/adr-architecture-knowledge-chunking-strategy.md)). The questions can be generated on demand or on schedule by passing pre-configured prompts and retrieved relevant architecture context to LLM to come up the questions. Designated expert architects can review the questions on user interface and include them in the tests if they are satisfactory.
  
  **C2 Diagram:**

  ![test 1 and test 2 content updates](/assets/new-questions-c2.png "test 1 and test 2 content updates")


**(TBD - Other usecases)**
- HMW generate AI-assisted structured feedback reports for expert architects so that candidates receive detailed insights more efficiently?
- HMW automate test content evaluation for expert architects so that improvements are continuously implemented based on candidate performance trends?
- HMW implement AI-based consistency checks for expert architects so that grading discrepancies are minimized across multiple reviewers?
- HMW develop AI-driven mechanisms for expert architects so that new case studies can be created and rotated periodically to prevent exam content leaks?

## Architecture characteristics

### Existing architecture characteristics

- **Data integrity** - Ensures that test questions, candidate submissions, and grades are securely stored without integrity issues or data loss.
- **Accuracy** - Guarantees precise grading for MCQs, short-answer aptitude questions, and case study submissions, maintaining evaluation reliability.
- **Interoperability** - Enables seamless communication across different systems and components, ensuring smooth integration between the certification platform and expert evaluators.

### New architecture characteristics(in addition to existing)

- **Scalability** - The LLM-based architecture is designed to handle a 5-10X increase in demand while maintaining grading accuracy and performance. Auto-scaling cloud-based LLMs and vector stores ensure efficient resource utilization.
- **Cost Efficiency** - AI-driven grading significantly reduces manual evaluation hours, cutting down expert workload and associated costs. A detailed cost analysis is yet to be finalized.
- **Accuracy** -  Retrieval-Augmented Generation (RAG) leverages a continuously updated vector store of manually graded answers to provide contextual references, improving grading consistency.
- **Credibility** - Human-in-the-loop validation ensures that low-confidence AI predictions are manually reviewed, refining grading accuracy over time.
- **Observability** -  AI systems introduce challenges such as bias, hallucinations, and relevance issues. LLM observability tools within the AI gateway actively monitor inputs and outputs, ensuring reliable system performance.
- **Explainability** - LLM-generated grading scoring & feedback must be transparent and justifiable, allowing expert architects to understand AI-driven grading decisions, enhancing overall productivity.
- **Evolvability** - The architecture supports continuous updates to grading models, question formats, and evaluation criteria, ensuring adaptability as educational standards and AI capabilities evolve.

## Final thoughts
**Limitations**
- **Scalability of Manual Review** – The system relies on human reviewers for low-confidence cases, which can become a bottleneck as submission volume grows.
- **LLM Hallucinations and Biases** – Despite using RAG, LLMs may still generate inaccurate or biased grading decisions, requiring ongoing monitoring and corrections.
- **Contextual Understanding Gaps** – While AI can process structured evaluation criteria, it may struggle with nuanced architectural decisions, making human oversight essential for complex cases.
- **Productionization** - LLM-based application deployment is still evolving, with new cost-effective methodologies emerging rapidly, requiring continuous adaptation to ensure scalability and efficiency.
 
**Next Steps: Phased Rollout Strategy**
- **Pilot & A/B Testing:** Run AI and human grading in parallel to compare accuracy, refine AI models, and track grading consistency.
- **AI-First with Expert Oversight:** AI handles primary grading, with human validation for low-confidence cases and structured feedback improvements.


