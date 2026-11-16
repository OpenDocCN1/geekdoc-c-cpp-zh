# Table 9.6 Average Results over 30 Replications of 10 Small Problem Instances where Population Size is 100 and the Initial Population is Generated at Random

| Algorithm | Mutation | Dev | Time |
|---|---|---|---|
| NNX | No M | 5.40 | 18.4 |
| | M1 | 1.44 | 26.4 |
| | M2 | 0.35 | 26.2 |

# Table 9.7 Average Results over 10 Replications of 15 Large Problem Instances where Population Size is100 and Initial Population is Generated at Random

| Algorithm | Mutation | Dev | Time |
|---|---|---|---|
| NNX | No M | 7.61 | 25.3 |
| | M1 | 4.94 | 65.0 |
| | M2 | 4.70 | 1063.0 |

of GEX might improve performance. Table 9.5 also shows these results. When, for example, it says 50% NNX and 50% GEX, it means that 50% of the time the next population was generated using NNX and the other 50% of the time it was generated using GEX. Slight improvement over pure NNX was observed in the case of mutation M2 for the higher percentages of NNX usage.

Based on these results, the researchers concluded that using mixtures of the two algorithms was not worth the increased computational time. So further experiments were performed using only NNX by itself.

Using only NNX with random initialization but with a population size of 100, they obtained the results in Table 9.6. Note that for mutation M2, the average percent deviation is 0.35 and the average time is 26.2. Looking again at Table 9.5 we see that using this same combination with a population size of 50, the average percent deviation is 0.55 and the average time is 5.52. This increase in accuracy should be worth the increased time.

Next the researchers investigated larger instances from TSPLIB in which 318 <= n <= 1748. Having concluded that hybrid initialization is also not worth additional time, they ran NNX 10 times on each of these instances with random initialization and a population size of 100. Table 9.7 shows the results. Curiously, on the large problem instances, mutation M2 did not do much better than mutation M2 but required substantially more computation time. Looking again at Table 9.6 we see that in the case of small instances M2 performed much better than M1 with little increased computational cost.

Simply testing a heuristic algorithm on a number of instances does not show if it as an advancement. We need to see how it fares relative to previously existing heuristic algorithms. Stål et al. [2010] compared NNX to the heuristic TSP algorithms Meta-RaPS [DePuy et al., 2005] and ESOM [Leung et al., 2004] using 10 benchmark TSP instances. Table 9.8 shows the results. Either NNX-M1 (mutation M1) or NNX-M2 (mutation M2) performed the best for every problem instance.