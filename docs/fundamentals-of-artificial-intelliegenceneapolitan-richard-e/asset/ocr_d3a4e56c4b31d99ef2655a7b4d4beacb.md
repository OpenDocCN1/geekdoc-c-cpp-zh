# # 14.3 Discussion and Further Reading

Markov Decision Processes (MDP) [Bellman, 1957] were developed to model decision making under uncertainty. Partially Observable Markov Decision Processes (POMDP) [Kaelbling et al., 1998] are a generalization of MDPs. Traditionally, MDPs have been used in machine learning to model reinforcement learning [Meuleau and Bourgine, 1999]. However, it turns out that POMDPs are mathematically equivalent to Dynamic Bayesian networks but do not provide the intuitive graphical framework. Vermorel and Mohri [2005] note that the multi-armed bandit problem is actually a one-state MDP.

# # EXERCISES

# ## Section 14.1

**Exercise 14.1** Either obtain or develop data concerning some entities you wish to classify. For example, the data could concern the spectra of many stars. Download AutoClass at http://directory.fsf.org/project/autoclass/, and use AutoClass to classify the entities.

**Exercise 14.2** Suppose we have five levers and the following sequence of rewards for the levers:

| round | lever 1 | lever 2 | lever 3 | lever 4 | lever 5 |
|---|---|---|---|---|---|
| 1 | 4 | 2 | 8 | 1 | 12 |
| 2 | 3 | 5 | 7 | 10 | 8 |
| 3 | 5 | 7 | 6 | 3 | 15 |
| 4 | 6 | 4 | 8 | 20 | 6 |
| 5 | 2 | 9 | 3 | 6 | 12 |
| 6 | 8 | 8 | 4 | 8 | 14 |
| 7 | 7 | 10 | 3 | 10 | 12 |
| 8 | 3 | 2 | 6 | 4 | 10 |
| 9 | 1 | 14 | 3 | 8 | 9 |
| 10 | 5 | 3 | 5 | 15 | 14 |
| 11 | 3 | 8 | 6 | 8 | 20 |
| 12 | 2 | 5 | 8 | 21 | 8 |
| 13 | 5 | 15 | 3 | 10 | 10 |
| 14 | 6 | 2 | 4 | 7 | 9 |
| 15 | 1 | 4 | 5 | 5 | 15 |

Apply the ε-Greedy Strategy, the ε-First Strategy, the ε-Decreasing Strategy, and the ε-LeastTaken Strategy to these levers and this sequence of rewards. Use ε = .3 for the ε-Greedy, the ε-First, and the ε-LeastTaken Strategies. Use ε = 3 for the ε-Decreasing Strategy.