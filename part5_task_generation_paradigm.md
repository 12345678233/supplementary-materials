# Autonomous Task Generation: A Concrete Experimental Paradigm

A concrete way to test autonomous task generation is to let an embodied agent generate evaluation tasks through its own interaction with an environment, rather than relying only on fixed, human-written benchmarks.

This can be implemented as a closed-loop pipeline with four steps:

## (1) Open-ended exploration

The agent is placed in a simulated or real environment and allowed to explore through observation, navigation, and manipulation. Early exploration can be random or only minimally guided, so task generation does not require a pre-defined task list.

## (2) Environment-to-task translation

The data collected during exploration—such as images, object identities, spatial relations, trajectories, contact events, and state changes—are automatically converted into candidate tasks. For example, object-label pairs can yield classification tasks, relative positions can yield spatial reasoning tasks, and action sequences can yield planning or navigation tasks.

## (3) Task filtering and diversification

Because exploration may generate many redundant tasks, candidate tasks are filtered by similarity and clustered to retain diverse representatives. This ensures that the system produces not only more tasks, but also a broader task distribution.

## (4) Task evolution

Existing tasks are further expanded through structured transformations, including reuse (turning a substructure of a complex task into a simpler new task) and recombination (swapping or recombining elements from different tasks to create new variants).

## Closed-loop formulation

The resulting loop is:

**explore → collect data → generate tasks → filter/evolve tasks → solve new tasks → generate further tasks**

Under this paradigm, autonomy is evaluated not only by whether a system can solve given tasks, but also by whether it can continually produce, diversify, and extend its own task distribution through interaction with the environment.

## Relation to the household example

The household tasks shown in the supplementary page can be interpreted as one concrete instantiation of this paradigm. They illustrate how interaction with a structured environment can yield families of tasks involving object understanding, spatial reasoning, and daily activity completion.