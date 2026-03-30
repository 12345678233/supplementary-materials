# Anonymous Supplementary Material

This repository contains supplementary materials related to the paper rebuttal.  
It is organized into three parts:

1. [Part 1. A concrete example of GSA-style evaluation](#part-1-a-concrete-example-of-gsa-style-evaluation)  
2. [Part 2. An anonymous example of interpretable task decomposition and difficulty analysis](#part-2-an-anonymous-example-of-interpretable-task-decomposition-and-difficulty-analysis)  
3. [Part 3. Results on the original eight household tasks](#part-3-results-on-the-original-eight-household-tasks)  

---

## Part 1. A concrete example of GSA-style evaluation

This part presents a more detailed worked example of how a GSA-style evaluation pipeline can be instantiated in an embodied setting.

Importantly, this example is intended to show **one possible operationalization** of the GSA framework, rather than the only valid pathway for evaluation.  
Its purpose is not to prescribe a universal benchmark or a fixed testing recipe, but to make the stage logic more explicit and easier to inspect in practical experimental terms.

In this example, the key idea is that **G, S, and A are distinguished by the type of evidence required**, not simply by task difficulty.  
A harder benchmark does not automatically imply a higher stage.  
Instead, each stage asks a different question about the system:

- **G (General)** asks whether the system shows foundational capacities such as cross-family generalization and the ability to generate or adapt tasks beyond a fixed benchmark list.
- **S (Specialized)** asks whether those capacities can be consolidated into stable, high-level competence within a structured domain.
- **A (Applicable)** asks whether the system can sustain reliable, safe, and value-consistent performance under realistic deployment conditions.

For implementation details, generated-task examples, and quantitative statistics, see:

- [task_generation_results.md](task_generation_results.md)

### Why stage boundaries should be defined by evidence profiles

A central motivation of the GSA framework is that strong performance on a fixed task suite does not by itself tell us what kind of capability has been demonstrated.

For example:

- a system may perform well on a structured benchmark through narrow specialization, without showing robust generalization beyond that benchmark;
- a system may solve many specialized tasks in a controlled setting, yet still fail when deployed in an open environment with disturbances, safety constraints, and long-horizon interaction;
- a system may execute assigned tasks well, but still lack the ability to autonomously generate relevant goals or useful task variations.

For this reason, the three stages are defined here as **different evidence profiles** rather than as a single continuous score.

### An illustrative GSA-style testing logic

### G stage: General evidence

The goal of the G stage is to test whether the system demonstrates broad and robust generalization across structurally diverse task families, rather than only competence on a fixed benchmark list.

In this worked example, **task families** are defined as sets of tasks that share an underlying structure while differing in objects, layouts, contexts, or environmental conditions.  
The key question is not whether the system memorizes a particular task template, but whether it can transfer its competence across variations that preserve task structure while changing surface form.

#### What is evaluated

The G stage focuses on two kinds of evidence:

1. **Task generalization capability**
   - Can the system maintain competent performance across both seen and unseen tasks?
   - Does its performance remain robust under task-family variation and environmental variation?
   - Can it handle new instances without additional training or fine-tuning?

2. **Autonomous task generation capability**
   - Can the system generate tasks on its own rather than only execute externally assigned ones?
   - Are the generated tasks relevant to actual household needs?
   - Do the generated tasks cover a sufficiently broad range of household task categories?

#### Operationalization

- **Task families**: groups of tasks with shared task structure.
- **Evaluation protocol**: test the system on both **seen** and **unseen** tasks under the same conditions, without additional training or fine-tuning.

#### Passing logic

A system is treated as reaching the G stage only when all of the following are supported by evidence:

- **Task Generalization Capability (T)**: performance remains consistent across seen and unseen tasks.
- **Autonomous Task Generation Capability (A)**:
  - **Relevance (R)**: generated tasks align with actual household needs.
  - **Task Coverage (TC)**: generated tasks cover a diverse set of household task categories.
![Task decomposition and difficulty analysis pipeline](figures/image.png)
In simple terms, the G stage is meant to show that the system can both **generalize beyond previously encountered task instances** and **produce meaningful and sufficiently diverse tasks of its own**.  
This is why G is not defined as “doing well on many tasks,” but as showing evidence of foundational cross-task transfer and autonomy.

### S stage: Specialized evidence

The goal of the S stage is to test whether the system, after satisfying the G-stage prerequisites, can achieve stable and strong competence within a defined structured domain.

Here the emphasis is no longer on breadth across diverse task families, but on **depth, stability, and repeatability** within a more clearly bounded task domain.  
Typical examples include a structured household task portfolio or a domain such as object search in a 3D environment.

#### What is evaluated

The S stage focuses on whether the system can:

- repeatedly solve a curated set of structured tasks with high success;
- maintain performance across repeated sessions rather than succeeding only once;
- exhibit stable competence under controlled conditions where the success criteria are clearly defined.

#### Operationalization

- **Task portfolio**: a curated set of specialized tasks with clear criteria such as success rate, completion time, and number of resets.
- **Evaluation environment**: controlled lab or testbed settings with consistent lighting, object placement, and task initialization.

#### Passing logic

A system is treated as reaching the S stage only when all of the following are supported by evidence:

- **Success Rate >= 90%** across the specialized task portfolio, averaged over at least **100 trials per task**.
- **Performance Degradation <= 5%** when tasks are repeated across multiple sessions.

In simple terms, the S stage is meant to show that the system’s general capacities can be consolidated into **stable, reusable, and high-performance domain competence**.  
This is why S is not merely “doing some hard tasks,” but demonstrating reliable specialization within a structured evaluation scope.

### A stage: Applicable evidence

The goal of the A stage is to test whether the system, after satisfying the G and S prerequisites, can operate reliably in realistic real-world environments over time.

The key distinction of the A stage is that the question is no longer whether the system can solve tasks in principle, but whether it can remain **robust, safe, recoverable, and useful under deployment conditions**.  
This includes environmental variability, long-horizon execution, partial failures, human interaction, and real costs of error.

#### What is evaluated

The A stage focuses on whether the system can:

- complete realistic tasks, including cases not covered during S-stage testing;
- operate with a high degree of autonomy;
- recover from partial failures without external rescue;
- avoid critical safety violations;
- maintain acceptable user experience and value-consistent behavior;
- sustain these properties over an extended deployment period.

#### Operationalization

- **Deployment setting**: real-world environments such as homes, warehouses, or hospitals, with natural variability in lighting, clutter, and human activity.
- **Evaluation duration**: extended continuous operation (for example, one month).
- **Human-in-the-loop assessment**: end users or supervisors provide ratings on usability, reliability, and safety.

#### Passing logic

A system is treated as reaching the A stage only when all of the following are supported by evidence:

- **Task Completion Rate >= 85%** across realistic use cases, including novel scenarios not seen during S-stage testing.
- **Autonomy Ratio >= 90%**, where autonomy ratio is the proportion of task attempts that succeed without human intervention.
- **Recovery Rate >= 70%**, where recovery rate is the proportion of partial failures from which the system autonomously recovers and continues execution.
- **Critical Safety Incidents <= 1%**, including failures such as causing injury or property damage.
- **User Experience Score >= 4.0 / 5.0** on post-deployment surveys covering safety, reliability, and value-consistent behavior.
- **Sustained Performance**: all of the above metrics must hold over at least **1 month**, with weekly performance not dropping below **80%** of the initial level.

In simple terms, the A stage is meant to show **deployment readiness**, not just stronger benchmark performance.  
This is why A is not defined as “more difficult tasks,” but as evidence that competence remains reliable, safe, and useful under realistic operating conditions.

### How to interpret the stage transition

This worked example implies the following decision logic:

- A system belongs to **G** if it shows foundational evidence of cross-family generalization and autonomous task generation.
- A system belongs to **S** if it first satisfies the G prerequisites and then demonstrates stable, high-performance competence in a structured task domain.
- A system belongs to **A** if it first satisfies the G and S prerequisites and then demonstrates sustained, safe, and robust deployment performance in realistic environments.

In this sense, the stages are **cumulative but non-interchangeable**.  
Strong S-stage evidence does not replace G-stage evidence, and strong benchmark performance alone does not establish A-stage applicability.

### Interpretation

This part should be read as a **worked example**, not as a universal standard.  
Its purpose is to show that the distinction between G, S, and A can be made explicit through different kinds of evidence rather than through a single aggregate benchmark score.

---

## Part 2. An anonymous example of interpretable task decomposition and difficulty analysis

This part provides an anonymized example of a method for decomposing visual tasks into underlying ability components and estimating their difficulty levels.

Its role here is limited but useful.  
It is **not** meant to directly test whether a black-box system contains a particular internal module or architectural mechanism.  
Instead, it supports a narrower point: evaluation can be made more interpretable by clarifying **what a task requires** and **how difficult the task is**.

In other words, this part focuses on the **task side** of evaluation rather than the **system side**.

### Core idea

Many realistic tasks are composite rather than atomic.  
For example, a visually grounded task may require object recognition, spatial understanding, temporal interpretation, and reasoning over visual context.

Instead of treating such a task as a single opaque benchmark item, this method maps each task to a set of required abilities and then estimates task difficulty from that composition.

### Method overview

The pipeline has three stages:

1. **Ability decomposition**  
   Each task is mapped to a predefined ability set.

2. **Human-referenced difficulty estimation**  
   Human pairwise comparisons are used to determine which tasks are perceived as more difficult.

3. **Difficulty modeling**  
   Task difficulty is estimated from ability composition and aligned with the human-referenced ordering.

### Why this part is included

This part is included to support a simple methodological point:

- a benchmark score alone does not tell us much about what a task is actually testing;
- task decomposition helps clarify which abilities are involved;
- difficulty analysis helps clarify how demanding a task is relative to others.

So this section should be read as an example of **interpretable evaluation design**, not as a direct test of internal architecture.

### Illustrative figures

A simple way to read this part is:
it asks two questions — **what abilities does a task require, and how difficult is that task relative to others?**

#### 1. Pipeline overview

![Task decomposition and difficulty analysis pipeline](figures/fig_part2_pipeline.png)

**Figure 1.** Overview of the anonymous task decomposition and difficulty analysis pipeline.

From left to right:

- the task is decomposed into required abilities,
- human participants compare task pairs by difficulty,
- and the method estimates task difficulty so that the predicted ordering matches human judgments as closely as possible.

The key point is that task difficulty is grounded in both **ability composition** and **human comparison data**.

#### 2. Comparison between automated and human ability annotation

![Comparison between automated and human ability annotation](figures/fig_part2_human_model_agreement.png)

**Figure 2.** Comparison between automated ability annotation and human judgments.

This figure asks whether automatic task–ability labeling is broadly consistent with human judgment.

- **(a)** shows that the automated annotation is relatively close to the aggregated human result, while individual human annotators also differ from one another.
- **(b)** shows that the overall pattern of automated annotations is similar to the pattern of aggregated human annotations.
- **(c)** shows that human annotators themselves are variable, so exact agreement should not be expected.

The main takeaway is that the automated annotation is not arbitrary: it broadly follows the same task–ability structure captured by human judgment, while being more scalable for large-scale evaluation.

#### 3. Explainable outputs and benchmark analysis

![Explainable outputs and benchmark analysis](figures/fig_part2_explainable_results.png)

**Figure 3.** Example outputs of the anonymous framework after task decomposition and difficulty analysis.

This figure shows what the framework can provide beyond a single task score:

- **(a)** shows which ability dimensions are assigned greater weight in the final difficulty estimation.
- **(b)** shows that these abilities can still be organized in an intuitive and interpretable way.
- **(c)** compares which abilities are covered by different benchmark sets.
- **(d)** compares how wide the difficulty range is in different benchmark sets.

The main takeaway is that the framework does not only say whether a system performs well or poorly.  
It also helps explain what kinds of abilities are being tested and how challenging the benchmark is overall.

### Suggested source mapping for the figures

If you are exporting figures from the anonymous paper, the following mapping is recommended:

- `figures/fig_part2_pipeline.png`  
  → original Figure 2

- `figures/fig_part2_human_model_agreement.png`  
  → original Figure 3

- `figures/fig_part2_explainable_results.png`  
  → original Figure 6

### Takeaway

This part is included as an anonymized example of:

- interpretable task decomposition,
- structured difficulty analysis,
- and clearer analysis of what a benchmark is actually testing.

It should not be read as direct evidence that a particular internal architectural component exists in a black-box system.

---

## Part 3. Results on the original eight household tasks

This part contains the original fixed eight-task household evaluation results, which serve as a worked embodied benchmark example.

### Benchmark scope

We construct eight daily embodied task categories in simulated home environments:

- Counting Objects  
- Building Blocks  
- Jigsaw Puzzle  
- Understanding Buttons  
- Setting Tables  
- Tidying Up Rooms  
- Preparing Baggage  
- Selecting Gifts  

These categories cover a range of embodied capabilities, including object understanding, spatial reasoning, and activity completion.

![Benchmark overview](figures/fig2_task_overview.png)

**Figure 4.** Overview of the eight household task categories and representative subtasks.

### Evaluation framework

The evaluation is conducted in a simulated home arena through a perception–decision–action loop.  
The system connects multimodal LLMs with the embodied environment through a perception module and an action module.

![System framework](figures/fig3_framework.png)

**Figure 5.** System framework for evaluating MLLM-based embodied agents.

### Task-level performance

The following figure shows model performance across the eight task categories.

![Performance on eight tasks](figures/fig4_results_8_tasks.png)

**Figure 6.** Performance of evaluated MLLM agents across the eight task categories.

### Model family comparison

The following figure summarizes the performance profiles of major model families across task categories.

![Model family comparison across task categories](figures/fig6_model_family_distribution.png)

**Figure 7.** Performance profiles of major model families across the benchmark.

### Interpretation

This part functions as an embodied worked example of structured task-family evaluation.  
It shows that application-oriented and autonomy-relevant evaluation can be implemented in a simulated yet realistic environment.

---

## Overall interpretation

Taken together, these three parts serve different roles:

1. **Part 1** gives a concrete example of how GSA-style evaluation can be organized.  
2. **Part 2** provides a task-side analysis tool for understanding what benchmark items require and how difficult they are.  
3. **Part 3** provides the original household benchmark results as an embodied worked example.

This repository is therefore best read as a compact supplement showing several complementary components of a broader evaluation perspective.

---

## Note

This repository is intentionally limited to a compact visual supplement for peer review.

## Anonymity statement

This repository is provided in anonymized form for review purposes only.
