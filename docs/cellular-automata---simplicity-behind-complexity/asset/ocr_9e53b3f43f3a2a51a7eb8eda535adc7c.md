The concept of motifs isodynamicity was investigated in more details by linear ODE models. Three theorems were proved (Taylor et al., 2010) for classes of motifs sharing this property. The first such class is motifs containing target vertex with maximal in-degree (Fig. 12a):

**Theorem 1.** Consider the family of feed-forward motifs on *n* vertices with a single target vertex. Then all motifs for which the in-degree of the target vertex is (*n*−1) are isodynamic. This theorem is easily extended to motifs having many target nodes (Fig. 12b):

**Theorem 2.** Suppose 1 < *k* < *n* and consider the family of feed-forward motifs on *n* vertices with precisely *k* target vertices. Then all motifs for which the in-degrees of the target vertices are (*n*−*k*) are isodynamic.

Theorem 1 expands the isodynamicity pattern so as to incorporate the class $S(n−1)T1$, while Theorem 2 expands that pattern further to the class of motifs $S(k)T(n−k)$. The third theorem defines isodynamicity in the class of bi-parallel motifs. This class is also of S1T1 type but the single source and single target nodes are connected by two parallel chains of links. Adding in a specific manner links between the two parallel chains does not change the overall motif performance (Fig. 12c).

![](bbox=[0.216, 0.384, 0.782, 0.641])

Fig. 12. A, B, C. Illustration of Theorems 1, 2 and 3, respectively.

**Theorem 3.** Consider the bi-parallel motif on *m* vertices, with the alternating vertex labeling. Suppose we construct a new motif by adding directed edges between vertices *k* and (*k*+1) (regardless of orientation) if *k* has the same parity as *m* and 1 < *k* < (*m*−1). Then this new motif is isodynamic with the bi-parallel motif.

Theorems 1-3 thus identified two large classes of isodynamic feed-forward motifs: such that the target vertices of which have maximal in-degree, and bi-parallel motifs with a variable number of redundant edges not changing the performance rate. An idealized case was used, all reactions in which proceed at the same rate, and the formation of intermediate complexes is not taken into account. Nevertheless, numerical simulations with more realistic nonlinear ODE models have shown time estimates close to those produced by the linear models and the CA ones.