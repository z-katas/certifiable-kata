# ZAItects - Certifiable, Inc | O'Reilly Architectural Kata (Winter 2025)

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
- [Final thoughts](final-thoughts)  
  

## Team

- **Avinash**, [LinkedIn](https://www.linkedin.com/in/avinashmarepalli/)
- **Saketh Kumar**, [LinkedIn](https://www.linkedin.com/in/saketh-kumar-27b124126/)
- **Srikanth**, [LinkedIn](https://www.linkedin.com/in/koraveni-srikanth/)
- **Shashank**, [LinkedIn](https://www.linkedin.com/in/shashank-sheela-740746b4)


**Check [Glossary](business-requirements/glossary.md) to understand more about certain terms.**


# Introduction

## Background & Context

The **Software Architecture Licensing Board (SALB)** was established in the U.S. to regulate and accredit companies that administer certification exams for software architects. This legislation mandates that IT professionals and existing software architects must obtain official certification, similar to doctors and lawyers. **Certifiable, Inc.** is one of the few accredited companies that offer these certifications, with **200 candidates per week** currently seeking certification. The company employs **300 expert software architects**, of whom **5 are designated experts** with the authority to modify and update certification tests.

## Expansion Plans

Following the success of the U.S. licensing program, **UK, Europe, and Asia have adopted similar laws**, requiring software architecture certification for employment. Rather than establishing independent certification programs, these regions have agreed to **leverage U.S.-based accredited companies** like Certifiable, Inc. to administer exams. The **certification cost remains fixed at $800**, as mandated by the SALB, and is applicable globally.

## Current Certification Process

1. **Test 1: Aptitude Test**
   - Multiple choice questions (**auto-graded**).
   - Short answer questions - Graded manually by experts within **1 week**. Requires 3-hour review per candidate.
   - **80% required** to proceed to Test 2.

2. **Test 2: Architecture Submission**
   - Candidates submit a **case study-based architecture design** (randomly assigned from 5 options).
   - **Graded manually** by expert software architects (requires **8-hour review per candidate**).
   - **80% required** to pass and receive certification.

3. **Certification Database & Verification**
   - Successful candidates' details are **stored in a certification database**.
   - Employers can verify candidates via the **SoftArchCert verification portal**.
   - Candidates that fail either test receive **detailed feedback** from expert software architects and can reapply. Candidates who pass Test 1 only need to retake Test 2.

## Challenges in Expansion Plans

- **Candidate Growth:** Expanding from **200 per week** to **1,000 - 2,000 per week**, with a **21% projected increase over four years**.
- **New Grading Workload:**
  - **Test 1 short answers:** **6,000 expert hours per week**.
  - **Test 2 case study review:** **12,800 expert hours per week** (assuming 80% move forward).
  - **Total workload:** ~**19,000 expert hours per week**, costing **$1M+ per week** at **$50/hour**.
- **Expert Availability:**
  - Existing **300 experts working 15 hours per week** provide **4,500 hours total**.
  - Even with a **20% workload increase per expert** (18 hours per week), capacity reaches only **5,400 hours**, **3.5X lower than required**.
  - One-week turnaround time for each test requires **parallel grading**, posing **operational challenges**.
- **Cost Burden:** Each candidate’s evaluation requires 11 hours of expert review, costing $550 per license (68% of the $800 certification fee). The high cost, limited expert availability, and rising demand pose major scalability, financial, and operational challenges.
- **Other Expert Responsibilities:**
  - Provide detailed feedback to failed candidates via email.
  - Analyze, review, and update certification tests based on candidate performance trends.
  - Incorporate new industry techniques, practices, and patterns into certification content.
  - Modify and create new case studies for Test 2 to maintain exam integrity and prevent leaks.

## Key Objectives

With the anticipated **5-10X increase** in certification requests, Certifiable, Inc. must optimize its processes to sustain growth. The company aims to leverage **Generative AI** to address the challenges highlighted above.

- **Identify AI Opportunities:** Evaluate areas where **Generative AI** can replace or enhance manual grading and assessment processes.
- **Design Solutions:** Design Generative AI services that automate identified manual processes while adhering to established AI architecture patterns and avoiding known anti-patterns.
- **Redesign Architecture for AI Integration:** Seamlessly integrate AI-driven components into the existing system, ensuring **compatibility, scalability, and minimal disruption** to current operations.

### Non-Functional Attributes

Each non-functional requirement aligns with a key business challenge:

- **Scalability:** *As the software architecture industry is projected to grow by 21% globally and certification demand increases 5-10X, the system must scale to accommodate the surge in applicants.*
- **Cost Efficiency:** *AI implementation costs must be optimized to prevent overruns while supporting Certifiable, Inc.'s strategic expansion. AI adoption should not exceed a 30% increase in grading expenses.*
- **Accuracy:** *As a market leader, Certifiable, Inc. must maintain grading precision. Inaccurate evaluations could impact candidate careers and damage the company’s reputation.*
- **Reliability:** *Certification credibility is critical—misleading exams or inconsistent grading can undermine employer trust and industry acceptance.*

# Automation use-cases using Gen AI
  Note - HMW - How Might We
- ### **HMW implement AI-driven grading models for expert architects so that they can evaluate short-answer submissions 4X faster?**
  
  Refer [**detailed design details**](usecases/hmw-ai-grading-short-answers.md) of this usecase

  **Solution approach:** The evaluation of short answers in test1 can be automated using an LLM based system. The system can perform a RAG that uses existing historical correct and incorrect answers along with candidate's answer as context to LLM to output the grade. Evaluations     with confidence score more than a pre-defined threshold are considered final whereas the ones below are further processed by expert architects.
  
  **C2 Diagram:**

  ![ASAS Grader C2 Diagram](/assets/test1-grader-c2.jpg "ASAS Grader C2 Diagram")

  **Benefits of the new architecture:** TBD
 
- ### **HMW implement AI-driven grading models for expert architects so that they can evaluate case study submissions 4X faster?**
  
  Refer [**detailed design details**](usecases/hmw-ai-grading-case-studies.md) of this usecase

  **Solution approach:** The AI-driven grading system for Test 2 is designed to handle the scalability and complexity of evaluating case study submissions. The process begins with automated content segregation, where different artifacts such as requirements, architectural   
   decisions, and diagrams are categorized for structured evaluation. A multi-model AI strategy is employed to assess each artifact using specialized AI analyzers, ensuring grading consistency and accuracy. The system leverages an AI gateway to securely interact with the LLMs.
  
  **C2 Diagram:**

  ![Test2 case study](/assets/test2c2.png "Test2 case study")

  **Benefits of the new architecture:** TBD

- ### **HMW automate the identification of emerging software architecture trends and generate expert-level certification questions to assist architects in updating the certification database efficiently?**
  
  Refer [**detailed design details**](usecases/hmw-ai-content-updates.md) of this usecase
  
  **Solution approach:** The generaton of new questions in test 1 and case studies in test 2 can be automated using a web search + RAG LLM architecture pattern. Latest architecture techniques, patterns and trends are ingested with targeted web search and stored in a vector store     following semantic chunking. The questions can be generated on demand or on schedule by passing pre-configured prompts and retrieved relevant architecture context to LLM to come up the questions. Designated expert architects can review the questions on user interface and include   them in the tests if they are satisfactory.
  
  **C2 Diagram:**

  ![test 1 and test 2 content updates](/assets/new-questions-c2.png "test 1 and test 2 content updates")

  **Benefits of the new architecture:** TBD

**(TBD - Other usecases)**
- HMW generate AI-assisted structured feedback reports for expert architects so that candidates receive detailed insights more efficiently?
- HMW automate test content evaluation for expert architects so that improvements are continuously implemented based on candidate performance trends?
- HMW implement AI-based consistency checks for expert architects so that grading discrepancies are minimized across multiple reviewers?
- HMW develop AI-driven mechanisms for expert architects so that new case studies can be created and rotated periodically to prevent exam content leaks?


## Final thoughts
- (TBD) cost benefit
- (TBD) limitations with Gen AI
- (TBD) ideal next steps


