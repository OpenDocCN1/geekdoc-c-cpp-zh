# Efficient Join Query Processing on the Cloud ■ 203

**DEFINITION 3**: A join-path graph $G_{\mathfrak{G}} = (\mathcal{V}, \mathcal{E}, \mathcal{L})$ is a complete weighted graph with edge labels, where each edge is associated with a weight and scheduling information. Specifically, $\mathcal{V} = \cup \mathcal{V}\{\mathcal{R}_1, \dots, \mathcal{R}_n\}$, $\mathcal{E} = \{(v_i, v_j)\}$ represents a unique no-edge-repeating path $p$ between $v_i$ and $v_j$, in $G_{ij}$. $L \in \mathcal{L}[\mathcal{E}_{ij}] = \cup \{(v_i, v_j), w_{ij}\}$ is the minimum cost to evaluate $e_{ij}$, and $S = \{s|s=w(e)\}$ is the scheduling to evaluate $e'$ at the cost of $w(e')$.

In the definition, the scheduling information on the edge refers to user-specified parameters to run an MRJ such that the job is expected to be accomplished as fast as possible. In this work, we consider the number of Reduce tasks assigned to an MRJ as $R_k(MRJ)$, which is the only parameter users needs to specify in their programs. The reason we take this parameter into consideration is based on two observations from extensive experiments: (1) It is not guaranteed that the more computing units involved in Reduce tasks, the sooner the MRJ job is accomplished; and (2) given limiting units, there is resource contention among multiple MRJs.

Intuitively, we enumerate all the possible join combinations in $G_{\mathfrak{G}}$. Note that in the context of join processing, $R_i owtie R_k owtie R_j$ is the same as $R_j owtie R_k owtie R_i$; therefore, $G_{\mathfrak{G}}$ is an undirected graph. We elaborate Definition 3 with the following example. In Figure 9.3a, a corresponding join-path graph $G_{\mathfrak{G}}$ is generated, which is presented in an adjacent matrix format on a path. For instance, in the cell enclosed in braces is identified $n$ functions on a path. The corresponding to $R_1$ and $R_2$, $\{3, 4, 6, 5, 2\}$ represents a no-edge-repeating

![](bbox=[0.132, 0.663, 0.375, 0.863])

| $R_1$ | $R_2$ | $R_3$ | $R_4$ | $R_5$ |
|---|---|---|---||}{
| | (1,2,3) | (1) (3,2) | (3,4) (3,5,6) | (3) (1,2) | (1,2,5) (2,4,6) (3,5) |
| | $e(G_{12})$ | (3,4,6,5,2) | | (1,2,4,6) (3,5,6) | |
| $R_2$ | | (1,3,2) | (2,4) (2,5,6) | (2) (3) (2,4,6) | (2,5) (2,4) (1,3,5) (1,3,4,6) |
| | | $e(G_{23})$ | (1,3,4) (1,3,5,6) | (1,3,4,6,6) |
| $R_3$ | | | | (4) (6) | (6,4) (4,5) (6,3,1,2) |
| | | | | (4,5,6) (6,3,1,2) | (5) (4,6) (3,1,2,5) (3,1,2,4,6) |
| $R_4$ | | | | | |
| | | | | | $e(G_{34})$ | |
| $R_5$ | | | | | |
| | | | | | (4,5) $e(G_{45})$ |

FIGURE 9.3 Example join graph $G_c$ (a) and its corresponding join-path graph $G_{\mathfrak{G}}$ presented in an adjacent matrix.