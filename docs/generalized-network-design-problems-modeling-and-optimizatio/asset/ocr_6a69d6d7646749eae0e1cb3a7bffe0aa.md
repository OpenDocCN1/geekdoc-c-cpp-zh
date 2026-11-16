![](bbox=[0.16, 0.1, 0.86, 0.29])

Figure 4.5. Transforming the original station $\sigma$ into the station $\sigma'$ in the antisymmetric TSP. The gray path marks the travel route from $d_x$ to $a_y$ in the original station $\sigma$ and in the transformed station $\sigma'$.

# ## Transformation of the RTSP to the symmetric TSP

Since the previous transformation results in an asymmetric TSP, Hu et al. [78] proposed an alternative procedure for generating a symmetric TSP, defined on the graph $G' = (V', E')$. Their approach follows the same basic ideas as the previous transformation with the observation that the number of nodes must be doubled during the process.

Let $a'_1, ..., a'_k \in \sigma'$ again be exact copies of the arrival-nodes $a_1, ..., a_k \in \sigma$, ordered according to their arrival times. These nodes are duplicated once more, thus producing the nodes $a''_1, ..., a''_k$. Then, these nodes are connected to a cycle by edges $(a'_2, a''_1), (a'_3, a''_2), ..., (a'_k, a''_{k-1}), (a'_1, a''_k)$ with zero costs and the edges $(a'_i, a''_i), i = 1, ..., k$ with high costs $M$. High costs on edges $(a'_i, a''_i)$ cause few of them as possible to be present in the solution.

For example, in Figure 4.6, when a travel-edge leads to $a_1$ there are two possible routes to go through $(a'_1, a'_2, a'_3) \cup \{a''_1, a''_2, a''_3\}$, one ending in $a''_3$ and one ending at $a'_1$. The latter one is cheaper, since the edge $(a'_1, a''_1)$ with high costs is ignored.

The same procedure is applied to the nodes $d''_1, ..., d''_l$ and their duplicates $d''_1, ..., d''_l$. Then, all nodes $a''_i, i = 1, ..., k$ are connected to nodes $d''_j, j = 1, ..., l$ and the cost of the edges $(a''_i, d''_j)$ are set to

$c(d''_i, d''_j) = [1440 + t_{d'_j} - t_{a''_i} - f_B(\sigma)] \mod 1440 + f_B(\sigma)$.

Similar to the previous transformation, the costs of the original stay-edges are implicitly included in these edges.

Finally, for each original travel-edge $(d_j, v)$ a new edge $(d''_j, v)$ is added, with the cost given by

$c(d''_j, v) = c(d_j, v) + M'$.