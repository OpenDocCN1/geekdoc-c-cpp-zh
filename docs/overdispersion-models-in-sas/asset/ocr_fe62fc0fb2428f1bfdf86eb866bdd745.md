multinomial distribution was applied to model overdispersed. The data, which can be found in Table 7.4, consisted of n = 73 sets, each representing the counts on the frequency of occurrence of the four fossil pollen grains made at a certain depth of a core. The pollen was counted until a total of m_j = 100 grains were reached. As in Mosiman's analysis, we will regard the data from different sets as independent. For the j-th set (j = 1, 2, ..., 73)

$t_j = (t_{j1}, t_{j2}, t_{j3})$ is the observed vector of counts for the types "pine", "fir" and "oak", with the usual constraint $t_{j1} + t_{j2} + t_{j3} \le 100$. Assume that $t_j$ is a realization of $T_j$. We will find the MLE of $	heta = (\pi, r')$ when $T_j$ is modeled as an

Dirichlet-multinomial($\pi,r;m_j$) or as a Random-clumped Multinomial($\pi,r;m_j$). Note that $\pi = (\pi_1,\pi_2,\pi_3)$, where $\pi_1, \pi_2$ and $\pi_3$ represent the proportion of pollen grains of pine, fir and oak falling in the core during a particular time, respectively. Also note that $\pi_1+\pi_2+\pi_3 < 1$, and that the proportion of pollen grains of alder is $\pi_4 = 1-(\pi_1+\pi_2+\pi_3)$.

# Table 7.4: Forest Pollen Count Data

| t1 | t2 | t3 | t1 | t2 | t3 | t1 | t2 | t3 | t1 | t2 | t3 |
| 94 | 0 | 5 | 85 | 1 | 84 | 1 | 12 | 88 | 0 | 0 | 9 |
| 75 | 2 | 1 | 91 | 1 | 4 | 97 | 0 | 3 | 94 | 0 | 4 |
| 81 | 2 | 3 | 99 | 1 | 0 | 83 | 0 | 13 | 69 | 7 | 18 |
| 95 | 2 | 3 | 90 | 2 | 8 | 81 | 1 | 15 | 90 | 0 | 8 |
| 89 | 3 | 1 | 91 | 0 | 8 | 81 | 1 | 16 | 86 | 1 | 8 |
| 84 | 5 | 1 | 79 | 1 | 19 | 76 | 2 | 18 | 90 | 0 | 7 |
| 81 | 3 | 10 | 89 | 0 | 7 | 87 | 3 | 7 | 74 | 5 | 16 |
| 97 | 0 | 2 | 95 | 2 | 1 | 91 | 1 | 5 | 82 | 2 | 11 |
| 86 | 1 | 8 | 90 | 3 | 5 | 94 | 0 | 5 | 87 | 3 | 9 |
| 86 | 2 | 1 | 93 | 1 | 6 | 88 | 1 | 11 | 68 | 3 | 26 |
| 82 | 2 | 1 | 90 | 2 | 7 | 93 | 4 | 2 | 77 | 3 | 11 |
| 72 | 1 | 6 | 89 | 2 | 9 | 84 | 0 | 8 | 86 | 2 | 7 |
| 89 | 0 | 8 | 88 | 1 | 9 | 87 | 1 | 12 | 79 | 1 | 11 |
| 93 | 4 | 2 | 99 | 0 | 1 | 89 | 1 | 6 | 87 | 0 | 11 |
| 87 | 1 | 1 | 86 | 1 | 10 | 73 | 0 | 13 | 79 | 1 | 17 |
| 85 | 0 | 12 | 88 | 0 | 7 | 87 | 3 | 8 | 74 | 0 | 19 |
| 91 | 0 | 7 | 91 | 1 | 94 | 1 | 3 | 80 | 0 | 14 |
| 95 | 1 | 3 | 84 | 0 | 14 | 81 | 2 | 9 | 85 | 3 | 9 |
| 94 | 3 | 3 | | | | | | | | | |

$t_1, t_2$ and $t_i$ are respectively, totals counts of pollen grains of pine, fir and oak