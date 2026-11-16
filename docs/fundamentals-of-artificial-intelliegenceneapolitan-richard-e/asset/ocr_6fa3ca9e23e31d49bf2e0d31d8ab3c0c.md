# Table 14.1 Comparisons of Performance of Several Bandit Strategies

| Strategy | R-100 | R-1000 | R-10,000 | N-130 | BN-1300 |
|---|---|---|---|---|---|
| POKER | .787 | .885 | .942 | 203 | 132 |
| | | | | | |
| ε-Greedy, .05 | .712 | .855 | .936 | 733 | 431 |
| ε-Greedy, .10 | .740 | .858 | .916 | 731 | 453 |
| ε-Greedy, .15 | .746 | .842 | .891 | 715 | 474 |
| | | | | | |
| ε-First, .05 | .732 | .906 | .951 | 735 | 414 |
| ε-First, .10 | .802 | .893 | .926 | 733 | 421 |
| ε-First, .15 | .809 | .869 | .901 | 725 | 411 |
| | | | | | |
| ε-Decreasing, 1 | .755 | .805 | .851 | 738 | 411 |
| ε-Decreasing, 5 | .785 | .895 | .934 | 715 | 413 |
| ε-Decreasing, 10 | .736 | .901 | .949 | 733 | 417 |
| | | | | | |
| ε-LeastTaken, .05 | .750 | .782 | .932 | 747 | 420 |
| ε-LeastTaken, .10 | .750 | .791 | .912 | 738 | 432 |
| ε-LeastTaken, .15 | .757 | .784 | .892 | 734 | 441 |

For the R-experiment, bigger numbers are better (rewards), and for the N-experiments, smaller numbers are better (punishments).

In the first experiment, they simulated 1000 levers, where the reward associated with each lever was normally distributed. The means and standard deviations were drawn uniformly from the interval (0,1). They then generated a data set containing 10,000 rounds, and they evaluated the strategies using 100 rounds, 1000 rounds, and all 10,000 of the rounds. They computed the average reward per round for each strategy. This process was repeated 10,000 times and the averages over all 10,000 trials was computed.

The second experiment concerns the real-world problem known as the Content Distribution Network Problem (CDN) [Krishnamurthy et al., 2001]. The problem is to retrieve data through a network with several redundant sources available. For each retrieval, one source is selected, and the algorithm then waits until the data are retrieved. The objective is to minimize the sum of the delays over all retrievals. To simulate this problem, they used the home pages of over 700 universities as sources. The universities represent the levers. The home page for each university was retrieved every 10 minutes for 10 days, resulting in 1300 rounds. For each retrieval, the retrieval latency in milliseconds was recorded. This latency was the punishment. The strategies were evaluated using 130 rounds and all 1300 rounds. They computed the average latency (punishment) per round for each strategy.

For both experiments, the process was repeated 10,000 times and the averages over all 10,000 trials was computed. Table 14.1 shows the results for POKER and the four strategies presented here. For the R-experiments, big-