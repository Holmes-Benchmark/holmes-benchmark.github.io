---
layout: page
title: Insight
subtitle: Holmes' Investigations 🔎
---

The evaluation of various language models yields to serval insights.
Find more details and further discussions in our <a href="todo">paper</a>.
Any questions or wondering about other details? Happy to <a href= "mailto:holmesbenchmark@gmail.com">chat</a>.

# The Linguistic Competence of Language Models
Language models clearly better understand *morphology* and *syntax* than *semantics*, *reasoning*, and *discourse*.
This distinction is evident in morphology and syntax's significantly higher Task Metric (`f1 macro` or `regression`).
Next, it makes sense to differentiate between the phenomena types (like *morphology* or *discourse*).
We find they have balanced *Discriminability* scores, which means that none of them dominates the overall ranking.
*Discriminability* measures the rank correlation of a specific dataset with the overall Holmes🔎 rankings.
Finally, the substantial *Selectivity* underlines the validity of our probing setup.
Compared to training a probe using randomized labels, our probes effectively detect linguistic patterns in the internal representation space of language models.

![Drag Racing](assets/img/overall.jpg)

# Language Model Architecture
The architecture of language models a clear effect on their linguistic competence. 
We compare encoder-only and decoder-only language models of up to 220 million parameters.
The linguistic competence of encoder-only models is clearly more pronounced than of decoder-only ones, across all phenomena types.
We assume that instabilities of the token-level internal representations causing these deficiencies of decoder-only models. 
Diving into the detail confirm this assumption.
We find that even with 70 billion parameters, decoder-only language models do not reach the accuracy of encoder-only one on the top-20 most common tokens for part-of-speech tagging. 

![Drag Racing](assets/img/architecture.jpg)

# Scaling Language Model Size
The linguistic competence of LMs scales with their model size, independent of their architecture, when exceeding 500 million (Pythia) or 1 billion parameters (T5).
We find that this trend is in particular prominent for *morphology* and *syntax* but less pronounced for *semantics*, *reasoning*, and *discourse*. 
![Drag Racing](assets/img/scaling.jpg)

# Instruction Tuning
Apart from the alignment with human interaction, instruction tuning has a prominent effect on the linguistic competence of LMs. 
We find a particular pronounced postive effect for *morphology*, *syntax*, and *resoning* - especially for larger language models, like FLAN-UL2 
In contrast, we find mixed effects for *discourse* and *semantics*.
Further, we analyze the role of instruction tuning data.
We find that quality has more positive effects on the linguistic competence of LMs than quantity, as Tülu (high quantity) underperforms and Vicuna (high quality) outperforms.

| Model          (params) | Morphology | Syntax    | Semantics | Reasoning | Discourse | Overall   |
|-------------------------|------------|-----------|-----------|-----------|-----------|-----------|
| Llama-2-Chat (7B)       | -8\%       | +3\%      | -5\%      | -9\%      | -3\%      | -2\%      |
| FLAN-T5     (11B)       | +10\%      | +2\%      | -2\%      | +6\%      | -2\%      | +1\%      |
| Dolly-v2      (12B)     | +4\%       | -3\%      | -9\%      | -3\%      | +4\%      | -4\%      |
| Tülu-2     (13B)             | +5\%       | +2\%      | -15\%     | 0\%       | -30\%     | -8\%      |
| Orca-2     (13B)             | -1\%       | -3\%      | -4\%      | +4\%      | -5\%      | -2\%      |
| Llama-2-chat (13B)      | +3\%       | +1\%      | -6\%      | +3\%      | -1\%      | -1\%      |
| Vicuna-v1.5   (13B)     | +23\%      | +7\%      | -3\%      | +6\%      | -6\%      | +4\%      |
| FLAN-UL2     (20B)      | **+40\%**  | **+16\%** | **+7\%**  | **+13\%** | +1\%      | **+13\%** |
| Mixtral-Instruct (47B)  | +4\%       | +3\%      | 0\%       | +6\%      | -2\%      | +2\%      |
| Tülu-2      (70B)       | +15\%      | 0\%       | -11\%     | -3\%      | 0\%       | -2\%      |
| Llama-2-Chat    (70B)   | +23\%      | +14\%     | +2\%      | +4\%      | **+17\%** | +10\%     |
| *Average*               | *+10\%*    | *+4\%*    | *-3\%*    | *+4\%*    | *-2\%*    | *+1\%*   |
*Mean winning rate improvement in percentage compared to their pre-trained base model.*
