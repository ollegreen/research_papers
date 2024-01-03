# Research Papers

Thoughts, summaries and notes on recently read research papers. A research _tinkering_ place, if you will.

Summaries below in the readme, and the notes for reach paper are in the respective categorical directories.

![banner](https://imageupload.io/ib/r9SBL4OyMajfrDK_1698921485.jpeg)

______

## Paper:
Read: 
Institution: 
Mental Reference: 

### Problem


### Solution


### Applicability: How can it be applied to my current work & research







_______


## Paper: "Orca 2: Teaching Small Language Models How to Reason"
Read: -
Institution: Microsoft Research
Mental Reference: 
Link: https://arxiv.org/pdf/2311.11045.pdf

### Problem
Task Diversity and Data Scaling, it often captures the style of models being trained on Chat-GPT data, but it’s less on logic/reasoning and more on imitation. 

### Solution 
The key contributions of the paper are:

1. **Explanation Tuning**: they basically do the same {query, response} style, but make GPT-4 to give detailed explinations of the logic/reasoning as well. For instance: “explain like I’m five, think step by step and justify your response”. Quote: "We augment ⟨query, response⟩ pairs with detailed responses from GPT-4 that explain the reasoning process of the teacher as it generates the response. These provide the student with additional signals for learning. We leverage system instructions (e.g.., explain like I’m five, think step-by-step and justify your response, etc.) to elicit such explanations. This is in contrast to vanilla instruction tuning, which only uses the prompt and the LFM response for learning, providing little opportunity for mimicking the LFM’s “thought” process.

2. **Scaling and Task instructions**: they use Flan FLAN-v2 collection (paper link) and pick out out of 10s of millions instructions → use a sample from the task collection to form a diverse mix of tasks. 5 million ChatGPT responses used → sample 1 million of them to acquire GPT-4 responses. → demonstrate how ChatGPT as a teacher assistant helps in progressive learning. Quote: We utilize the Flan 2022 Collection [19] as it provides an extensive public assortment of tasks and instructions. Particularly, we use FLAN-v2, supplemented with high-quality templates, advanced formatting patterns, and data augmentations. Even though FLAN holds tens of millions of instructions, we selectively sample from the task collection to form a diverse mixture of tasks, which we then further sub-sample to generate complex prompts. These prompts are used to query LFMs like ChatGPT and GPT-4, thus creating a rich and diverse training set. We collect 5 million ChatGPT responses, from which 1 million is further sampled to acquire GPT-4 responses. We demonstrate how ChatGPT as a teacher assistant helps in progressive learning.

### Applicability: How can it be applied to my current work & research
Not applicable directly, as we're not dealing with Small Language Models (SLMs) at the moment. But, good for future reference on when developing SLMs further.





______

## Paper: "ZEPHYR: DIRECT DISTILLATION OF LM ALIGNMENT"
Read: Nov 2023
Mental Reference: HuggingFace making smaller but more efficient model.

### Problem
distilled Supervised Fine-Tuning (dSFT) do not respond well to "natural prompts". So this refers to that dSFT models (like Alpaca and Vicuna) are trained on instructions based datasets. But since they've been trained/fine-tuned on instruction based data, it isn't as promising to give them "natural" prompts. For instance it would be rare that we ask ChatGPT in a instruction-based way such as: ", instead we would simply ask it: "How do I select the 5th column in a pandas dataframe?"

link to Alpaca data: [link](https://github.com/tatsu-lab/stanford_alpaca/blob/main/alpaca_data.json)

Vicuna example fine-tuning data:
```
{
        "instruction": "Give three tips for staying healthy.",
        "input": "",
        "output": "1.Eat a balanced diet and make sure to include plenty of fruits and vegetables. \n2. Exercise regularly to keep your body active and strong. \n3. Get enough sleep and maintain a consistent sleep schedule."
    }
```


### Solution
Use preference data from AI Feedback to improve dSFT.
* **What does this actually mean/do**:

* The main step is to utilize AI Feedback (AIF) from an ensemble of teacher models as preference
data, and apply distilled direct preference optimization as the learning objective (Rafailov et al.,
2023). We refer to this approach as dDPO. Notably, it requires no human annotation and no sampling
compared to using other approaches like proximal preference optimization (PPO) (Schulman et al.,
2017). Moreover, by utilizing a small base LM, the resulting chat model can be trained in a matter
of hours on 16 A100s (80GB) = ~10k per gpu

### Applicability: How can it be applied to my current work & research
Know how to apply (direct) distilled Supervised Fine-Tuning and fine-tune w. preference data from AI feedback. 





______

## Paper: “Semantic Uncertainty; Linguistic Invariances for Uncertainty Estimation in Natural Language Generation” 
Read: Sep 2023
Institution: Oxford OATML
Mental Reference: Oxford making it easier to make sure that semantically similar words make the entropy look lower. As "Sweden" is the same meaning as "It's Sweden".

### Problem 
Hard to evaluate LLM models due to “semantic equivalence”. It’s Paris and Paris is not the same for regular LLMs = entropy is still the same. 

### Solution
Proposes Deals with measuring uncertainty using their proposed “semantic entropy”, incorporate liugnustic invariances created to shared meanings. So basically: It's Paris and Paris = same, lower entropy in the dataset.

### Applicability: How can it be applied to my current work & research
This feels very generally useful for most applications, but still need to understand the implementation of the code better to see how complex this is to apply for production environments. 












______

## Paper: Oxford — “CLAM: Selective Clarification for Ambiguous Questions” 
Read: Sep 2023

### Problem 
Users give ambiguous questions that are hard for LLMs to answer with certianty as they don’t know what is being asked, so the give the most likely answer instead of asking a question back (humans asking vague questions such as “when did he land on the moon?” When meaning to ask “when did Alan Bean land on the moon?)

### Solution
A LLM framework to ask clarifying questions for ambigous questions. 

### Applicability: How can it be applied to my current work & research
In applied operations you want something to be able to handle this possible ambiguity in the user input, especially in a production environment. 






__________

## Paper: ReAct - Synergizing Reasoning and Acting in Language Models
Read: Oct 2023

### Problem

Improve the concept of "Chain of Thought"-prompting for outputs from LLMs, as its not grounded in external world and uses its own internal representation to generate reasoning. This limits the ability to reactively explore and reason or update its knowledge.

### Solution
Basically gives a prompt template to the LLM to show a pattern of Reasoning first, then Actioning it. **It also helps with interpretability** as you can see how the model is reasoning through to the answer. 

### Applicability: How can it be applied to my current work & research
* Together with LangChain, this is useful for more reasoning is of high priority/importance.
* It helps to make sure the model picks up the reasoning and aligns it with a more similar way to how we humans solve problems: by reasoning "hmm should I 







________

## Paper: Chain of Thought (CoT)
Read: Oct 2023

### Problem

**Main goal**: Improving outputs from LLMs

Two concepts as baseline:
1. Few-shot learning = Give a few examples in the prompt of what it should look like. in-context few-shot learning via prompting. That is, instead of finetuning a separate language model checkpoint for each new task, one can simply “prompt” the model with a few input–output exemplars demonstrating the task → but this doesn’t work that well when it requires a bit of reasoning. 
2. Arithemtic reasoning = Spell out the logic of thinking of how to solve the problem. It has shown that arithmetic reasoning can benefit from natural language rationale (He had 4 apples, now he has 2, how many did he loose? Well it was 4 and now it’s 2, so he lost 4-2 = 2.) → but this is costly to develop these high quality rationales. 



### Solution
- **CoT**: Combines the two of showing some examples of the thought process. 

### Applicability: How can it be applied to my current work & research
- Give hand holding to the LLM by giving it examples of both reasoning and examples of how it would look in different scenarios.



______

Template:

## Paper:
Read: 
Institution: 
Mental Reference: 

### Problem


### Solution


### Applicability: How can it be applied to my current work & research
