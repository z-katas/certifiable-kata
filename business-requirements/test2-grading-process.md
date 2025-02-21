# Test 2: Case Study Evaluation - Process & Requirements

## Reference to ISAQB Certification

As the details of the certification process are not explicitly provided, we are referring to the **iSAQB Certified Professional for Software Architecture (CPSA-A)** framework as the baseline for defining the test structure, evaluation criteria, and competencies. We took the help of ChatGPT to help us create the requirements of the evaluation process. We have referred to the [advanced-level curriculum](/business-requirements/references/isaqb-advanced-level-curriculum-en.pdf). Additionally, we reference the [**Building Evolutionary Architectures** framework](https://on24static.akamaized.net/event/21/83/36/0/rt/1/documents/resourceList1590605895255/softwarearchitecturebyexamplev202006231592919688383.pdf) to ensure the evaluation criteria align with evolving architectural practices.

## Overview

Test 2 evaluates a candidate’s **ability to architect a case study solution** by demonstrating practical application of software architecture principles. Candidates must submit structured artifacts that justify their architectural decisions while adhering to **functional and non-functional requirements**.

### **Core Objectives**

- Assess practical application of architectural concepts in a real-world case study.
- Evaluate the candidate's ability to design scalable, maintainable, and resilient systems.
- Validate architectural decisions based on industry best practices and trade-off analysis.
- Ensure candidates effectively communicate and document their architectural approach.

## Test Content

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


### **Scoring Formula**

Each artifact is graded based on a weighted scoring system. The final score is computed as follows:

**Final Score = (Σ (Artifact Score * Artifact Weight)) / 100**

Where each artifact's score is determined based on individual evaluation criteria, as detailed below.

### **Evaluation Criteria, and Weightage**

Each artifact category is evaluated based on **specific criteria**, and **justification for assigned scores** is provided.

1. **Functional & Non-Functional Requirements Definition** *(Weight: 20%)*

   - **Completeness of functional requirements** *(40%)*: Are all necessary functional aspects captured?
   - **Alignment with business goals** *(30%)*: Do the requirements support the intended business objectives?
   - **Clarity and prioritization of non-functional requirements** *(20%)*: Are performance, security, scalability, and maintainability considerations explicitly defined?
   - **Mapping of non-functional attributes to architectural decisions** *(10%)*: Are the constraints and trade-offs well-documented?

2. **Component-Level Architecture & Event Storming Model** *(Weight: 20%)*

   - **Clarity in component identification** *(30%)*: Are system components clearly defined and modular?
   - **Correctness of event interactions** *(30%)*: Are events properly mapped between components?
   - **Alignment with system objectives** *(25%)*: Do the interactions reflect the intended system behavior?
   - **Use of event storming best practices** *(15%)*: Are domain events structured logically and sequentially?

3. **Architectural Pattern Selection & Justification** *(Weight: 20%)*

   - **Suitability for the problem domain** *(35%)*: Is the chosen architectural pattern appropriate for the case study?
   - **Trade-off analysis** *(30%)*: Does the justification cover key trade-offs (e.g., performance vs. scalability)?
   - **Comparison with alternative patterns** *(20%)*: Are alternatives considered before finalizing a selection?
   - **Alignment with non-functional constraints** *(15%)*: Does the chosen pattern support expected system constraints?

4. **C2 (Context & Container) Diagram** *(Weight: 20%)*

   - **Accuracy of system boundaries** *(35%)*: Are external and internal components clearly distinguished?
   - **Completeness of inter-component communication** *(30%)*: Do container interactions depict system data flow correctly?
   - **Consistency with chosen architecture pattern** *(20%)*: Does the diagram align with the selected architectural approach?
   - **Use of standard notations** *(15%)*: Is the diagram presented using a structured, industry-standard format?

5. **Architectural Decision Records (ADRs)** *(Weight: 20%)*

   - **Clarity and justification of decisions** *(40%)*: Are trade-offs clearly documented?
   - **Impact analysis** *(30%)*: Does the ADR explain the long-term impact of decisions?
   - **Consideration of future evolution** *(20%)*: Are flexibility and adaptability addressed?
   - **Consistency with functional & non-functional requirements** *(10%)*: Do ADRs align with system goals?
