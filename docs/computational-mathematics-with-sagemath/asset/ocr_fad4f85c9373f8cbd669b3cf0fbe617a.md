![](bbox=[0.257, 0.082, 0.745, 0.287])

Figure 17.3 – A possible solution of the inexact formulation.

+   - to each vertex $v$ of the graph, we associate an integer $i_v$ representing the stage at which the cycle $C$ is visiting it, with $i_{v_0}=0$ for a fixed vertex $v_0$;
+   - to each edge $uv$ of $G$ we associate two binary variables $b_{uv}$ and $b_{vu}$ indicating if the edge belongs to the cycle $C$ (and to know in which direction this edge is being used);
+   - we impose that each vertex should have an outgoing and incoming edge in $C$;
+   - an edge $uv$ belongs to $C$ only if $i_u < i_v$ (the edges go in the increasing sense with respect to the order in which they are visited).

We can rewrite this algorithm in terms of linear equations in a few lines:

max: no objective function

such that:

$$\forall v \in V(G),\quad \sum_{uv\in E(G)} b_{uv}=1$$

$$\forall v \in V(G),\quad \sum_{uv\in E(G)} b_{vu}=1$$

$$\forall uv \in E(G)\setminus\{v_0\},\quad i_u-i_v+|V(G)|b_{uv}\leq |V(G)|-1$$

$$i_v-i_u+|V(G)|b_{vu}\leq |V(G)|-1$$

$$\forall v \in V(G),\quad i_v\leq |V(G)|-1$$

$b_{uv}$ is a binary variable

$i_v$ is an integer variable.

In this formulation, there is a coefficient $|V(G)|$, which often indicates that the solver will not be able to efficiently solve the linear program. Therefore, we will use an alternative modelling approach for the Hamiltonian cycle. Consider the following simple observation: if there exists a Hamiltonian cycle $C$ in our graph, then there exists for every proper subset $S$ of vertices at least two edges