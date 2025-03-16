## Cost Analysis

- A **hybrid approach** (Gen AI + experts for review) is a **cost-effective alternative** .
- Gen AI assisted evaluation is almost 5 times cheaper and 5 times efficiency wise compared to entirely manual evaluation( **$95 vs $470** and **1.88hr per candidate vs 9.4hr per candidate**) 
- The **Human Review Factor** is assumed to be 0.2 for the sake for this calculation, but is expected to come down further because of continous feedback loop that improves existing knowledge base with human graded answers and feedback
- Even at **10x scaling**, LLM costs remain low while expert costs exceed $1M. 
- Even considering the build costs(costs of developing new LLM applications, setup) and run costs(LLM token costs, cloud costs of new services, knowledge base maintenance), the cost incurred per candidate is to be quite low as compared to the cost of the test.
- LLM costs incurred to generate new questions and case studies is expected to be negligible as its load is quite low compared to the load involved in test 1 and test 2 evaluation.


Below analysis was done considering the costs and number of candidates per week

### **Current Costs (200 candidates per week)**

- Test 1:  
  - Requires **600 hours** (200 candidates per week and 3hrs for each short answer).  
- Test 2:  
  - Requires **1280 hours** at 80% test 1 pass rate and 8hrs for each case study evaluation (200 * 0.8 * 8)

| Total Time (hrs) | Expert review Cost ($) | Cost per candidate|
|---------------|----------------| ----------------|
| 1880 hrs       | $94,000       | $470

### **Scaling Up Costs (5x and 10x)**

- Test 1 Scaling:  
  - 5x: 600*5 = 3000 hours  
  - 10x: 600*10 = 6000 hours  
- Test 2 Scaling:  
  - 5x: 1280*5 = 6400 hours  
  - 10x: 1280*10 = 12800 hours  

#### **Total Expert Time and Costs per week**

| Scaling factor | Numer of candidates per week | Total expert review Time (hrs) | Expert review cost ($)  | Cost per candidate|
|---------------|--------------|---------------|----------------|-----------------|
| **5x**       |    1000    | 9400 hrs       | $470,000        | $470
| **10x**      | 2000   | 18800 hrs      | $940,000        | $470

### **Costs with Gen AI assisted evaluation**

Assuming 20% of candidate's submissions involve human evaluation, the hours put in by experts for:

- Test 1 Review: 
  - 5x: 200 * 0.2 * 3 * 5 = 600 hours  
  - 10x: 200 * 0.2 * 3 * 10 = 1200 hours  
- Test 2 Review:  
  - 5x: 200 * 0.2 * 0.8 * 8 * 5 = 1280 hours  
  - 10x:  200 * 0.2 * 0.8 * 8 * 10 = 2560 hours  

#### **Expert Review Time and Costs**

| Scaling Factor | Expert review time (hrs) | Expert review Cost ($) |
|---------------|----------------|-----------------|
| **5x**       | 1880 hrs       | $94,500        |
| **10x**      | 3760 hrs       | $188,000       |

#### **LLM Costs (Automated Evaluation)**

- **Cost formula:**  
  LLM costs = Number of LLM calls per candidate * Number of candidates * (Number of input tokens * Cost per input token +  Number of output tokens * Cost per output token)

  Note: Per token LLM costs are considered to be around the same as the cost of GPT o3-mini model. However, as mentioned in the test 2 evaluation strategy, we will be using different models for grading different sections, so the token cost could vary a little and can come down drastically for self hosted open source LLMs.

- Test 1:
  - 5x: 1 * 1000 * (2000 * 0.000015 + 2000 * 0.00006) = $150
  - 10x: 1 * 2000 * (2000 * 0.000015 + 2000 * 0.00006) = $300
- Test 2: (assuming **10 calls per submission** and **80 percent success rate in test 1** )
  - 5x: 10 * 1000 * 0.8 * (2000 * 0.000015 + 2000 * 0.00006) = $1200 
  - 10x: 10 * 2000 * 0.8 * (2000 * 0.000015 + 2000 * 0.00006) = $2400 

#### **Total costs with Gen AI assited capabilities**  

| Scaling factor | Numer of candidates per week |Expert review cost ($) | LLM cost ($)| Overall cost| Cost per candidate |
|---------------|----------------|----------------|-----------------|-----------------|-----------------|
| **5x**        | 1000| $94,550       | $1350       | 95900 | $95.90
| **10x**       | 2000| $188,000      | $2700         | 190700 | $95.35
