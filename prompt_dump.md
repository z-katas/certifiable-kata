## Purpose
This document contains the list of all prompts we have used while taking assistance of Gen AI tools to come up with architecture artifacts.

### Narrative Script Structure
- **Purpose:** Creating a compelling story for the final presentation
- Prompt:
```
Now I will give some more additional details about the presentation. It should tell a compelling story start till end. Here is the presentation flow:

1. Start with some undeniable fact about the Gen AI adoption
2. Then drill down into brief context of certifiable inc expansion plan and introduction
3. First we analyzed the challenges in the expansion plan -> about expert hours and cost analysis
4. Frame the key objective -> that talks about why?
5. Here comes the final key outcome achieved along with the final solution -> this talks about what?
6. Then we should talk about how we did:
   - First came up with the usecases (HMWs)
   - Non functional characteristics priority for adoption of LLMs
   - For each HMW, include persona and golden path, mockup, C2 diagram and highlights
7. Highlight fitness functions and common things important for GEN AI systems
8. What are the limitations
9. What should be the roadmap
```

### Understanding Administrative Process
- **Purpose:** To comprehend the administrative workflow before UI creation
- Prompt:
```
You task is to create a UI for administrative process here. Do not generate anything just understand the process.

Administrative Process: In addition to grading short answers and architecture submissions, employed Expert Software Architects are responsible for continually analyzing reports and results for the purposes of modifying existing certification tests. For example, if 95% of all candidates miss the same question, analysis should be done to modify the question or remove it. Also, as new techniques, practices, and patterns emerge in the industry, expert software architects add questions to reflect these advances. Designated employed expert software architects are also responsible for periodically editing and creating new case studies for the second test to prevent case studies and answers from leaking out to the internet.
```

### UI Reference Analysis
- **Purpose:** To analyze an existing UI for design patterns
- Prompt:
```
Understand this UI reference once done I will give the UI instructions later.
[Image of situational awareness dashboard]
```

### UI Requirements Specification
- **Purpose:** To outline specific elements needed in the administrative dashboard
- Prompt:
```
The UI should follow the same design as the reference UI with the admin processes as different tabs:
- Submission insights
- Architecture trends
- Case study relevance
- Architect review bias insights

By default the architecture trends tab should be selected and follow the golden path workflow.
Configured sources and parameters should be shown on a button click.

The screen should focus on:
- Trends with their sources
- Generated list of MCQs, Short answers, and case studies counts for each trend
- Left side: List of cards with trend details (one selected by default)
- Right side: Generated questions
- AI insights in the rightmost panel
- AI copilot button available at all times
```

### UI Refinement 
- **Purpose:** To add specific details to the administrative dashboard
- Prompt:
```
Please make these additions to the UI:
- Sources should have links to the articles in the center
- Change the persona name to "Chris"
- Add progress metrics at the top of the tabs showing this month's stats:
  * How many candidates applied
  * How many pending to submit
  * How many pending for review
  * How many pending to submit test 2
  * How many pending to review test 2
  * Final completed (certified and failed)
```