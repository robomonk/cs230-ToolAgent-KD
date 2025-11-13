Distilling Agentic Reasoning: A Validation and Extension of the Tool-Llama Agentic AI Model
Raed Al Sabawi (SUNet ID: 06933921)

1 Introduction
This project was initially designed to validate the claims of the TxAgent paper, a state-of-theart medical AI agent.[1] Our primary goal was to test a novel hypothesis: that the paper’s direct fine-tuning method could be surpassed by Knowledge Distillation (KD) [2] to create a more
robust, generalizable model. However, we encountered a critical blocker: the 378,000-sample
TxAgent-Instruct dataset is not publicly available.[1]
Consequently, our initial research was dedicated to identifying a high-fidelity, open-source substitute. We have successfully pivoted to the ToolLLM framework and its associated ToolBench
dataset.[3] This pivot is ideal as ToolLLM is a direct structural and methodological analog to
TxAgent:

1. Structural Proximity: Both are multi-step, tool-augmented agents that use a retriever
model (ToolRAG in TxAgent [1], a neural API retriever in ToolLLM [3]) to select tools, and a
fine-tuned LLM to reason.

2. Hypothesis Alignment (Critical): Our project’s hypothesis hinges on distilling an abstract ”reasoning function”. The TxAgent paper’s own ablation study (Figure 3e) proves
this function is its explicit, natural-language ”Thought” trace (removing it caused a ∼22.3%
accuracy drop).[1] The ToolBench dataset matches this perfectly, as its data is explicitly
structured as (Thought, Action) pairs.[3]

3. Evaluation Alignment: Our proposal required a ”stringent zero-shot generalization test”
on ”unseen” tools. The ToolBench ecosystem is explicitly designed for this, with over 16,000
APIs and evaluation splits for unseen tools and categories.[3]
This pivot allows us to test our exact original hypothesis, now ported to the ToolLLM framework.
Our hypothesis remains:
• Baseline (ToolAgent-FT): Standard fine-tuning on the ToolBench traces teaches the model
to memorize specific ”recipes” (known reasoning paths).[3]
• Stretch Goal (ToolAgent-KD): Our novel Knowledge Distillation approach [2] distills the
”principles of cooking” (the abstract ”reasoning function”) from a large 70B teacher model.
We predict the ToolAgent-KD model will show superior generalization, particularly when evaluated
on the unseen tools provided by the ToolBench ecosystem.[3] This milestone report details our
progress in implementing the baseline model and, most importantly, revising our experimental plan
based on crucial early findings.
