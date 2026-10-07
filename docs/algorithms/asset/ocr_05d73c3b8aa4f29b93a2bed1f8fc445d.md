Consider any positive $r > 0$. Give each edge $(i, j)$ a weight of $w_{ij} = r^{c_{ij}} - p_j$.

+   (a) Show that if there is a cycle of negative weight, $r < r^*$.

+   (b) Show that if all cycles in the graph have strictly positive weight, then $r > r^*$.

+   (c) Give an efficient algorithm that takes as input a desired accuracy $\epsilon > 0$ and returns a simple cycle $C$ for which $r(C) \geq r^* - \epsilon$. Justify the correctness of your algorithm and analyze its running time in terms of $|V|, \epsilon$, and $R = \max_{(i,j) \in E}(p_j/c_{ij})$.