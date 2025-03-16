 ![Cover picture](/assets/readme-cover-picture-latest.svg "cover picture")

# ZAItects - Certifiable, Inc | O'Reilly Architectural Katas (Winter 2025)

A structured approach to the **O'Reilly Winter 2025 Architectural Kata Challenge**.

## Table of Contents
- [Team](#team)
- [Problem definition](#problem-definition)
  - [Context](#context)
  - [Current Certification Process](#current-certification-process)
  - [Challenges in Expansion Plans](#challenges-in-expansion-plans)
  - [Key Objective](#key-objective)
  - [Business Constraints](#business-constraints)
- [Solution](#solution)
  - [Business outcomes achieved](#business-outcomes-achieved)
  - [Automation use-cases using Gen AI](#automation-use-cases-using-gen-ai)
  - [Architecture characteristics](#architecture-characteristics)
  - [Detailed architecture designs](#detailed-architecture-designs)
  - [Limitations with adoption of Gen AI](#limitations-with-adoption-of-gen-ai)
  - [Productionizing an LLM-Powered System](#productionizing-an-llm-powered-system)
- [Final thoughts](#final-thoughts)
  - [Anti Patterns](#anti-patterns)
  - [Glossary](#glossary)
  - [Roadmap](#roadmap)
  - [Our learnings](#our-learnings)  

## Team
 ![Team](/assets/team.png "team")
- [**Avinash**](https://www.linkedin.com/in/avinashmarepalli/) , Senior Tech Lead
- [**Saketh Kumar**](https://www.linkedin.com/in/saketh-kumar-27b124126/) , Senior Tech Lead
- [**Srikanth**](https://www.linkedin.com/in/koraveni-srikanth/) , Senior Tech Lead
- [**Shashank**](https://www.linkedin.com/in/shashank-sheela-740746b4) , Technical Product Manager
- [**Vijayakumaran**](https://www.linkedin.com/in/vijayakumaran-c-v/) , UX designer

# Problem definition

## Context

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
  - Each candidate’s evaluation requires 11 hours of expert review, costing **$470 per license on average (58% of the $800 certification fee)**
- **Grading inconsistencies & Fraud detection:**
  - Inconsistent manual grading can lead to **negative bias (unfair penalties)** or **positive bias (unqualified certifications)**, impacting **credibility**.
  - Lack of automated **fraud detection** increases the risk of impersonation, answer manipulation, and certification fraud, threatening **exam integrity**.
- **Other manual processes:**
  - Provide detailed feedback to failed candidates via email.
  - Analyze, review, and update certification tests based on candidate performance trends.
  - Incorporate new industry techniques, practices, and patterns into certification content.
  - Modify and create new case studies for Test 2 to maintain exam integrity and prevent leaks.

## Key Objective

“How might we **adopt Generative AI** to automate manual processes for expert architects so that their **productivity** is increased, **operational costs** are reduced, and **overall efficiency** is significantly improved to confidently handle a 10X growth in candidate demand?”

## Business Constraints
These are some constraints explicitly mentioned in the requirements.

- **Seamless Integration:** *Seamlessly integrate AI-driven components into the existing system, ensuring compatibility, scalability, and minimal disruption to current operations.*
- **Scalability:** *As the software architecture industry is projected to grow by 21% globally and certification demand increases 5-10X, the system must scale to accommodate the surge in applicants.*
- **Cost Efficiency:** *AI implementation costs must be optimized to prevent overruns while supporting Certifiable, Inc.'s strategic expansion. AI adoption should not exceed a 30% increase in grading expenses.*
- **Accuracy:** *As a market leader, Certifiable, Inc. must maintain grading precision. Inaccurate evaluations could impact candidate careers and damage the company’s reputation.* 
- **Credibility:** *Certification credibility is critical—misleading exams or inconsistent grading can undermine employer trust and industry acceptance.*

# Solution

## Business outcomes achieved
Refer [detailed cost & efficiency](/other_design_docs/cost-analysis.md) analysis 
### Productivity - 5x increase (19K to 3.7K avg expert hrs/week)
### Cost - 80% lower ($940K to $190K grading costs/ week)
### Efficiency - 4X improvement in overall efficiency

## Automation use-cases using Gen AI 
   We priortized 3 use-cases for this excercise

  ![HMW](/assets/how-might-we.jpg "HMW")

## Architecture characteristics
   **Existing system**
   ![Existing architectural characteristics](/assets/existing-architectural-characteristics.png "Existing architectural characteristics")

   **Additional characteristics with Gen AI adoption**
   ![Gen AI assisted system architectural characteristics](/assets/genai-assisted-system.png "Gen AI assisted system architectural characteristics")

   Refer [detailed architectural characteristics analysis](/other_design_docs/architecture-characteristics.md)

## Detailed architecture designs
  
### **HMW implement AI-driven grading models for expert architects so that they can evaluate short-answer submissions 4X faster?**
  
Refer [**detailed design details**](usecases/hmw-ai-grading-short-answers.md) of this usecase

**Solution approach:** The evaluation of short answers in test1 can be automated using an LLM based system. The system can perform **a RAG that uses existing historical correct** and incorrect answers along with candidate's answer as **context to LLM to output the grade**. Evaluations with confidence score more than a pre-defined threshold are considered final whereas the ones below are further processed by expert architects. The new approach allows for the output of the platform to scale to meet the expected growth while ensuring the results closely mimic manual grading. **Splitting the Grader and Judge into separate components allows us to improve/test one component while keeping the other component constant.**

**Data flow:**
 
![ASAS Grader dataflow diagram](/assets/short-answer-grading-dataflow.gif "ASAS Grader dataflow diagram")

**ASAS Grader Preliminary C3 Diagram:**

![ASAS Grader C3 Diagram](/assets/test1-grader-c3.jpg "ASAS Grader Partial C3 Diagram")


### **HMW implement AI-driven grading models for expert architects so that they can evaluate case study submissions 4X faster?**
  
Refer [**detailed design details**](usecases/hmw-ai-grading-case-studies.md) of this usecase

**Solution approach:** The AI-driven grading system for Test 2 is designed to handle the scalability and complexity of evaluating case study submissions. The process begins with **automated content segregation**, where different artifacts such as requirements, architectural   
   decisions, and diagrams are categorized for structured evaluation. **A multi-model AI strategy**([**ADR**](/ADRs/adr-ai-multi-model-strategy.md)) is employed to assess each artifact using **specialized AI analyzers**, ensuring grading consistency and accuracy. The system leverages an **AI gateway**([**ADR**](/ADRs/adr-using-ai-gateway.md)) to securely interact with the LLMs.

**Data flow:**
 
![Casestudy Grader dataflow diagram](/assets/casestudy-grading-dataflow.gif "Casestudy Grader dataflow diagram")
  
**C2 Diagram:**

![Test2 case study](/assets/test2c2.png "Test2 case study")

### **HMW automate the identification of emerging software architecture trends and generate expert-level certification questions to assist architects in updating the certification database efficiently?**
  
Refer [**detailed design details**](usecases/hmw-ai-content-updates.md) of this usecase
  
**Solution approach:** The generaton of new questions in test 1 and case studies in test 2 can be automated using a **web search + RAG LLM architecture pattern** ([**ADR**](/ADRs/adr-new-questions-and-case-studies-strategy.md)). Latest architecture techniques, patterns and trends are ingested with targeted web search and stored in a vector store following **semantic chunking**([**ADR**](/ADRs/adr-architecture-knowledge-chunking-strategy.md)). The questions can be generated on demand or on schedule by passing pre-configured prompts and retrieved relevant architecture context to LLM to come up the questions. Designated expert architects can review the questions on user interface and include them in the tests if they are satisfactory.
  
**Data flow:**
 
![Content monitoring dataflow diagram](/assets/content-monitoring-dataflow.gif "Content monitoring dataflow diagram")

**C2 Diagram:**

![test 1 and test 2 content updates](/assets/new-questions-c2.png "test 1 and test 2 content updates")

## Limitations with adoption of Gen AI
- **Scalability of Manual Review** – The system relies on human reviewers for low-confidence cases, which can become a bottleneck as submission volume grows.
- **LLM Hallucinations and Biases** – Despite using RAG, LLMs may still generate inaccurate or biased grading decisions, requiring ongoing monitoring and corrections.
- **Contextual Understanding Gaps** – While AI can process structured evaluation criteria, it may struggle with nuanced architectural decisions, making human oversight essential for complex cases.
- **Productionization** - LLM-based application deployment is still evolving, with new cost-effective methodologies emerging rapidly, requiring continuous adaptation to ensure scalability and efficiency.

## Productionizing an LLM-Powered System
Building a scalable, reliable, and secure LLM-powered system requires carefully aligned elements, here’s how we designed them for production readiness.
![llm-app-stack](/assets/Emerging-LLM-App-Stack.png "llm-app-stack")
- **LLM app stack:** This reference architecture outlines key systems, tools, and design patterns for effectively building LLM-powered applications.
  - Implemented a new pattern([**ADR-001: AI Gateway**](/ADRs/001-adr-using-ai-gateway.md)) that includes governance,observability etc
  - **Prompt orchestrator([ADR-005](/ADRs/005-adr-prompt-orchestrator.md)) : LangChain**
  - **Guardrails([ADR-010](/ADRs/010-adr-llm-guardrails.md)) : hybrid approach with the rule based filters**
  - **LLM Observability([ADR-011](/ADRs/011-adr-llm-observability.md)) - Langwatch**
- **LLM Evals([ADR-009](/ADRs/009-adr-llm-evaluation.md)):** Implement a Hybrid Evaluation Strategy, combining Automated Metrics for efficiency, Rubric-Based LLM Evaluation for consistency, LLM as a Judge for deep analysis, and Human-in-the-Loop Review for fairness and quality control.
- [**Fitness functions**](/other_design_docs/fitness-functions.md) - Identified and created strategy for few fitness functions such as accuracy,efficiency,credibility etc
- **LLM Security ([ADR-016](ADRs/016-adr-llm-security-owasp.md))** - The OWASP Top 10 vulnerabilities for LLM security highlight key risks  such as prompt injection, model poisoning, and data leakage.
- Governance
- **LLM Deployment Model ([ADR-007](ADRs/007-adr-llm-deployment.md))** - Adopt a Hybrid Deployment Model, processing sensitive candidate data on-premises for privacy while leveraging cloud-based LLMs for scalable, cost-efficient NLP tasks, ensuring security and compliance."


# Final thoughts

## Anti patterns
**Agentic AI**, while powerful, is not always the best choice. For our solution for the 3 use cases identified, we deliberately avoided this approach due to the following reasons:
- **Well-Defined Workflows:** Our system follows structured, predictable steps where deterministic AI models are more efficient and reliable.
- **Low Error Tolerance:** Agents, being probabilistic, can occasionally make incorrect decisions—unacceptable in a high-stakes certification process.
- **Cost & Performance Constraints:** Running an agent-based system demands high computational resources, increasing costs and latency without clear benefits.
- **Ensuring Accuracy & Compliance:** Instead of relying on autonomous AI agents, we integrated structured AI models with human-in-the-loop oversight, ensuring fairness, precision, and regulatory compliance.
- Agentic pattern will be best suitable for the analytics use case - HMW automate test content evaluation for expert architects so that improvements are continuously implemented based on candidate performance trends?


## Glossary
[Glossary](business-requirements/glossary.md) to understand more about certain terms.
 
## Roadmap
Approach: Phased Rollout Strategy
- **MVP:** Run AI and human grading in parallel to compare accuracy, refine AI models, and track grading consistency.
- **Growth:** AI handles primary grading, with human validation for low-confidence cases and structured feedback improvements.
- **Matured:** Achieve high-accuracy AI grading, with minimal human involvement focused on oversight.

## Our Learnings
Through this journey of productionizing an LLM-powered certification system, we gained critical insights that shaped our solution and align directly with our AI adoption goals

🛠️ **New AI Architectural Patterns & Design Approaches:**
  - We recognized that Agentic AI is not suitable for structured, high-accuracy workflows like certification grading, as it introduces unnecessary complexity, cost, and potential inaccuracies
  - Implemented AI Gateway, LLM as a Judge, and Human-in-the-Loop to ensure accuracy, validation, and seamless integration.
  - Explored how non-core functionalities (e.g., content generation, fraud detection) can be solved differently using AI.

🎯 **Gen AI Fitness Functions & Risk Mitigation:**
  - Understood the importance of fitness functions in LLM-based applications to handle risks like bias, hallucinations, and inconsistencies.
  - Learned that Evals (AI evaluation methods) are crucial and require multiple approaches based on accuracy, fairness, and usability needs.

📐 **Gen AI’s Impact on System Architecture & Scalability:**
  - Redesigned workflows to integrate AI seamlessly, ensuring scalability, observability, and compliance without disrupting existing processes.
  - Developed a Hybrid Deployment Model—on-premises for privacy-sensitive data, cloud for scalable AI processing.


