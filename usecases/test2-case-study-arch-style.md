
Automating the case study in test 2 using involves multi step architectural approach.

Assumptions:
------------
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

Document Segregator:
--------------------
Once the system receives the submission, it needs a content segregator where the content is segregated into various document types like mentioned above. Once the content is segregated,

Document Analyzer:
--------------------
The output from content segregator is processed through various AI analyzers for each content document type. We have used multi model strategy for the same, refere to this [ADR](/ADRs/adr-ai-multi-model-strategy.md). All the interactions to the external foundational LLMs are done through an AI gateway, please refer to this [ADR](/ADRs/adr-using-ai-gateway.md). The Architecture is graded by AI through various benchmarking scores and submitted for manual review (Human in the loop).

Architecture Grading Review:
----------------------------
Once the grading is done by AI, software expert reviews the grading in this step instead of manually reviewing, this will save atleast 50-70% of the time spent by them. If the expert wishes to override the grading, they can and the final grading is fed back to AI data pipelines as they continously evolve for more accurate results.

C2 Architecture diagram:
------------------------


![Test2 case study](/assets/test2c2.png "Test2 case study")


Data flow diagram:
------------------------


![Test2 dataflow](/assets/casestudy-flow-diagram.png "Test2 dataflow")

