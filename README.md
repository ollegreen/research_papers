# Research Papers

Thoughts, summaries and notes on recently read research papers. A research _tinkering_ place, if you will. Summaries below in the readme, and the notes for reach paper are in the papers directory.

_______



## Paper: AI capabilities can be significantly improved without expensive retraining
* **Read**: Jan 2023
* **Institution**: UC Berkeley, Open Philantropy
* **Mental Reference**: Summary of current post-training enhancements to improve LLM performance (such as CoT), quantified on a compute to performance basis.
* **Link**: https://arxiv.org/pdf/2312.07413.pdf

### Problem
It is difficult to compare how a 8% improvement in GSM8K means to other domains outside of this benchmark. As the author says: "It is hard to meaningfully compare the benefits of post-training enhancements that apply to different domains. For example, how does 10% greater accuracy on the MATH benchmark (Hendrycks et al., 2021) compare to 10% greater accuracy in a multiple choice knowledge test, or to 10% lower perplexity in a language modeling task?"

### Solution
They translate performance gains from different benchmarks into a "common currency": **Common Compute Gain**: *"how much additional training compute would have been needed to improve benchmark performance by as much as the post-training enhancement"*.

* Great visualisation of how different approaches shows more cost-efficient solutions and how they compare. 
* Helps to show that current methodologies that shows improved results might have a significant compute cost, which might not be worth the gain in performance depending on budget and performance requirements. 

### Applicability: How can it be applied to my current work & research
* Look and verify if you can apply and ensemble some cost-efficient solutions together in the LLM production projects and reserach.
* Few-shot, LATS and CoT are great in terms of no additional compute cost. However what is important to notice is the additional runtime cost goes up 10-100 times = for production environments this might not be the optimal long-term solutions.
* Majority voting is both high in added compute as well as additional runtime cost compared to performance improvements. Need to deep dive why.
* Look at Category 3 for Agent enhancements to verify your Agent projects and the current methodologies: 

1. Tool enhancements: teaching an AI system to use new tools, like a web browser.
2. Prompting enhancements: changing the text-based input to the model to steer its behavior and reasoning, e.g. including an example response to a similar question.
3. Scaffolding enhancements: programs that structure the model’s reasoning and the flow of information between different copies of the model (e.g. producing AI agents).
4. Solution choice enhancements: techniques for generating and then choosing between multiple candidate solutions to a problem.
5. Data enhancements: techniques for generating more, higher-quality data for fine-tuning.


### Problems
* On the 2nd page they mention they have not conducted these experiements themselves but instead relied on the results from other reserach papers -> **they don't have high confidence in this metric that they have created**. Quote: *"we don’t have high confidence in each individual CEG estimate, but we think that in aggregate they are informative about the typical benefit produced by an enhancement."* -> Take these with a pinch of salt, as some might not have accurate compute estimates. 




_______


## Paper: "Large Language Models as Optimizers"
* **Read**: Jan 2024
* **Institution**: Google Deepmind
* **Summary**: Using LLMs to figure out what the optimal prompt is > prompt engineering.

### Problem
People today have to figure out themselves what the optimal prompt is by doing prompt engineering for a specific task, which is time consuming and slightly random.

### Solution
Intuitive example for prompt optimization, quote: "the initial instruction is “Let’s solve the problem” with a (approximated, and same below) training accuracy of 60.5. We observe that the optimization curve shows an overall upward trend with several leaps throughout the optimization process, for example:
* “Let’s think carefully about the problem and solve it together.” at Step 2 with the training accuracy 63.2;
* “Let’s break it down!” at Step 4 with training accuracy 71.3;
* “Let’s calculate our way to the solution!” at Step 5 with training accuracy 73.9;
* “Let’s do the math!” at Step 6 with training accuracy 78.2.

**Prompt Optimization experimentation setup and eval on GSM8K**: sample 3.5% random questions of the GSM8K training set, and evaluate on full test set.

### Applicability: How can it be applied to my current work & research
- Semantic Optimsation Paper: Smart that they first try on travelling salesman before testing on prompt optimisation, to see it's real optimisation capabilities. Consider adding this to paper.
- **Production environments**: if it's a repetitive task that will occur >10M times a week, finding the most optimal prompt by itself could potentially be really helpful and reduce time on prompt engineering.
- tested on GSM8K, 8% improvement can be a benchmark to our approach of how well it should improve the score.
- Improvement: the generated prompts feels a bit lackluster (*Take a deep breath and work on this problem step-by-step.*) compared to their benchmark being the classic *Let's think step by step.*) Needs to be tested on more unique problems to see the benefit. 

### Personal Questions
- Was there any prompt that was "novel" at any point? Or was it simply their best optimisation generating: "Take a deep breath and work on this problem step-by-step.", which doesn't feel to novel compared to simply giving this directly to the model?
- In section 5.1 for models, why did they pick specifically these models for the optimizer and scorer? Reference: "• Optimizer LLM: Pre-trained PaLM 2-L (Anil et al., 2023), instruction-tuned PaLM 2-L (denoted PaLM 2-L-IT), text-bison, gpt-3.5-turbo, and gpt-4. • Scorer LLM: Pre-trained PaLM 2-L and text-bison. With pre-trained PaLM 2-L as the scorer, the optimizer LLM generates A_begin instructions. Since text-bison has been instruction-tuned, the optimizer LLM generates Q_begin and Q_end instructions when text-bison is used as the scorer.








_______


## Paper: "Orca 2: Teaching Small Language Models How to Reason"
* Read: Oct 2023
* Institution: Microsoft Research
* Summary: How to create Small Language Models (SLMs) efficiently with high quality data generated by LLMs.
* Link: https://arxiv.org/pdf/2311.11045.pdf

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
* Read: Nov 2023
* Mental Reference: HuggingFace making smaller but more efficient model.

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
* **Read**: Sep 2023
* **Institution**: Oxford OATML
* **Summary**: Oxford making it easier to make sure that semantically similar words make the entropy look lower. As "Sweden" is the same meaning as "It's Sweden".

### Problem 
Hard to evaluate LLM models due to “semantic equivalence”. It’s Paris and Paris is not the same for regular LLMs = entropy is still the same. 

### Solution
Proposes Deals with measuring uncertainty using their proposed “semantic entropy”, incorporate liugnustic invariances created to shared meanings. So basically: It's Paris and Paris = same, lower entropy in the dataset.

### Applicability: How can it be applied to my current work & research
This feels very generally useful for most applications, but still need to understand the implementation of the code better to see how complex this is to apply for production environments. 












______

## Paper: “CLAM: Selective Clarification for Ambiguous Questions” 
* **Read**: Sep 2023
* **Institution**: Oxford OATML

### Problem 
Users give ambiguous questions that are hard for LLMs to answer with certianty as they don’t know what is being asked, so the give the most likely answer instead of asking a question back (humans asking vague questions such as “when did he land on the moon?” When meaning to ask “when did Alan Bean land on the moon?)

### Solution
A LLM framework to ask clarifying questions for ambigous questions. 

### Applicability: How can it be applied to my current work & research
In applied operations you want something to be able to handle this possible ambiguity in the user input, especially in a production environment. 






__________

## Paper: ReAct - Synergizing Reasoning and Acting in Language Models
* Read: Oct 2023

### Problem

Improve the concept of "Chain of Thought"-prompting for outputs from LLMs, as its not grounded in external world and uses its own internal representation to generate reasoning. This limits the ability to reactively explore and reason or update its knowledge.

### Solution
Basically gives a prompt template to the LLM to show a pattern of Reasoning first, then Actioning it. **It also helps with interpretability** as you can see how the model is reasoning through to the answer. 

### Applicability: How can it be applied to my current work & research
* Together with LangChain, this is useful for more reasoning is of high priority/importance.
* It helps to make sure the model picks up the reasoning and aligns it with a more similar way to how we humans solve problems: by reasoning "hmm should I 







________

## Paper: Chain of Thought (CoT)
* Read: Oct 2023

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
* **Read**: 
* **Institution**: 
* **Mental Reference**: 
* **Link**: 

### Problem


### Solution


### Applicability: How can it be applied to my current work & research
