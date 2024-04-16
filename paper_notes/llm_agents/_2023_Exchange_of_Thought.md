### Exchange-of-Thought: Enhancing Large Language Model Capabilities through Cross-Model Communication
---
- [Zotero Select Link](zotero://select/groups/2480461/items/97X3273H)
- [Zotero URI](https://www.zotero.org/groups/2480461/items/97X3273H)
- Authors: [[Zhangyue Yin]] [[Xipeng Qiu]] 
- Topics: [[nlp_agent]] [[nlp_llm]]
- Venue: #arxiv #EMNLP
- Year: #2023

---
### Major Contributions
- we propose Exchange-of-Thought ([[EoT]]), a novel framework that enables cross-model communication during problem-solving
	- EoT integrates four unique communication paradigms: Memory, Report, Relay, and Debate
---
### Secondary Contribution
- Report performs best on MultiArith and AddSub, while Debate achieves optimal performance on SingleEQ and SVAMP. This indicates that various communication paradigms are well-suited for different scenarios.
- majority consensus termination is more suitable for scenarios involving multiple model communication.
- For the majority of samples, consensus on the answer can be reached within three rounds of communication. Wang et al. (2023c) obverse that answer consistency is proportional to accuracy. EoT enables models to engage in a greater number of exchanges and discussions on questions where consensus is challenging to achieve.
---
### Limitations/Future Work
- 
---
### Notes (Try to use backlinks)
- Wang et al. (2023c)’s research suggests that the single reasoning chain generated by CoT limits the model’s reasoning performance. By increasing the temperature to sample diverse reasoning chains and selecting answers through majority voting, the model’s reasoning performance can be further improved.
- [[Self-Consistency]]. This method replaces the greedy decoding strategy with the sampling of multiple reasoning paths and selecting the most consistent answer, resulting in significant performance improvements.
- Although CoT (Wei et al., 2022b) effectively enhances the performance of LLMs in complex reasoning tasks, they remain susceptible to errors during the reasoning process, leading to incorrect answers
	- To mitigate this issue, starting from the model’s own thoughts, Shinn et al. (2023) and Madaan et al. (2023) employ the model’s own feedbacks and past mistakes to refine the reasoning process
- The implementation of EoT encounters three key challenges: 
	1. How to identify the appropriate counterparts for model communication? 
	2. What are the conditions for ceasing communication between models? 
	3. How to minimize the influence of incorrect reasoning during the communication process?
- As illustrated in Figure 3, we propose **Memory, Report, Relay, and Debate** communication paradigms each corresponding to the **Bus, Star, Ring, and Tree network topologies**, respectively.
	- **Memory.** Under the Memory paradigm, all models record their rationale r and answer a in a logbook, which is fully visible from all models.
	- **Report.** Under the Report paradigm, we designate model mA as the central node, which can obtain the rationale and answer from all other models
	- **Relay.** Under the Relay paradigm, we order the models by number and connect them in a circle. Each node is capable of receiving information from the preceding node and transmitting its own information to the subsequent node
	- **Debate**. We have adapted the tree topology to devise the Debate paradigm. This paradigm permits leaf nodes to exchange information with each other, while parent nodes are solely responsible for aggregating information, meaning that information flow is directed upward from child to parent.
- Termination Condition
	- **Consistent Output Termination**. Inspired by Zheng et al. (2023), we implement a consistent output termination in EoT. The termination condition is triggered when the output of model mi in the j-th round is the same as the output in the j − 1-th round, a(j) i = a(j−1) i .
	- **Majority Consensus Termination.** Du et al. (2023) observed that LLMs can converge on a consensus after several rounds of debate, suggesting that LLMs fine-tuned with reinforcement learning from human feedback (RLHF) (Ouyang et al., 2022) are more likely to reach an agreement.
- Tasks
	- (1) Mathematical Reasoning
	- (2) Commonsense Reasoning:
	- (3) Symbolic Reasoning
- ![[2023_Eschange_of_Thought_architecture.png]]
- ![[2023_Exchange_of_Thought_communication.png]]
---