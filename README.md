# Research Papers

A place to read, take notes, log and apply / do experiments based on the research to see how useful it is.

A tinkering research place if you will. 

______









## Paper: Oxford — “Semantic Uncertainty; Linguistic Invariances for Uncertainty Estimation in Natural Language Generation” 
Read: Sep 2023

### Problem 
Hard to evaluate LLM models due to “semantic equivalence”. It’s Paris and Paris is not the same for regular LLMs = entropy is still the same. 

### Solution
Proposes Deals with measuring uncertainty using their proposed “semantic entropy”, incorporate liugnustic invariances created to shared meanings. So basically: It's Paris and Paris = same, lower entropy in the dataset.

### How can it be applied to my current work/research
This feels very generally useful for most applications, but still need to understand the implementation of the code better to see how complex this is to apply for production environments. 














## Paper: Oxford — “CLAM: Selective Clarification for Ambiguous Questions” 
Read: Sep 2023

### Problem 
Users give ambiguous questions that are hard for LLMs to answer with certianty as they don’t know what is being asked, so the give the most likely answer instead of asking a question back (humans asking vague questions such as “when did he land on the moon?” When meaning to ask “when did Alan Bean land on the moon?)

### Solution
A LLM framework to ask clarifying questions for ambigous questions. 

### How can it be applied to my current work/research
In applied operations you want something to be able to handle this possible ambiguity in the user input, especially in a production environment. 








## Paper: ReAct - Synergizing Reasoning and Acting in Language Models
Read: Oct 2023

### Problem

Improve the concept of "Chain of Thought"-prompting for outputs from LLMs, as its not grounded in external world and uses its own internal representation to generate reasoning. This limits the ability to reactively explore and reason or update its knowledge.

### Solution
Basically gives a prompt template to the LLM to show a pattern of Reasoning first, then Actioning it. **It also helps with interpretability** as you can see how the model is reasoning through to the answer. 

### How can it be applied to my current work/reserach
* Together with LangChain, this is useful for more reasoning is of high priority/importance.
* It helps to make sure the model picks up the reasoning and aligns it with a more similar way to how we humans solve problems: by reasoning "hmm should I 









## Paper: Chain of Thought (CoT)
Read: Oct 2023

### Problem

**Main goal**: Improving outputs from LLMs

Two concepts as baseline:
1. Few-shot learning = Give a few examples in the prompt of what it should look like. in-context few-shot learning via prompting. That is, instead of finetuning a separate language model checkpoint for each new task, one can simply “prompt” the model with a few input–output exemplars demonstrating the task → but this doesn’t work that well when it requires a bit of reasoning. 
2. Arithemtic reasoning = Spell out the logic of thinking of how to solve the problem. It has shown that arithmetic reasoning can benefit from natural language rationale (He had 4 apples, now he has 2, how many did he loose? Well it was 4 and now it’s 2, so he lost 4-2 = 2.) → but this is costly to develop these high quality rationales. 



### Solution
- **CoT**: Combines the two of showing some examples of the thought process. 

### How can it be applied to my current work/reserach
- Give hand holding to the LLM by giving it examples of both reasoning and examples of how it would look in different scenarios.



## Paper:  
Read: 

### Problem 


### Solution


### How can it be applied to my current work/research
