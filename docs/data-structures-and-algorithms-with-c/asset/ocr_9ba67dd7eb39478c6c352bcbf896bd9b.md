# Table 9.3: Breadth First Search

| Operation | Queue(q) | Print |
|---|---|---|
| ENQUEUE A | A | - |
| DEQUEUE A | B, C, D | A |
| ENQUEUE B, C, D | | |
| DEQUEUE B | C, D, G | A, B |
| ENQUEUE G | | |
| DEQUEUE C | D, G, F | A, B, C |
| ENQUEUE F | | |
| DEQUEUE D | G, F, E | A, B, C, D |
| ENQUEUE E | | |
| DEQUEUE G | F, E | A, B, C, D, G |
| DEQUEUE F | E | A, B, C, D, G, F |
| DEQUEUE E | - | A, B, C, D, G, F, E |

# Spanning Tree of Breadth First Search

![](bbox=[0.2, 0.43, 0.8, 0.62])

# Figure 9.26: Spanning tree for Breadth First Search for a Directed Graph (G)

Lemma 4: The length of the shortest path from S to V is denoted by $\delta(S, V)$. Then, on completion of BFS dist[V] = $\delta(S, V)$
Proof: The proof is based on induction taking the length of the shortest path.
Consider the shortest path from S
to V, u be the predecessor of V and BFS processes it first among all such vertices.
Thus, $\delta(S, V) = \delta(S, u) + 1$ (i)
When u is processed, then by induction we have dist[u] = $\delta(S, u)$ (ii)
Since V is a neighbour of u we set
dist[V] = dist[u] + 1 (iii)
thus from equation (ii)
dist[V] = $\delta(S, u) + 1$ (iv)
from equation (i) we have
dist[V] = $\delta(S, V)$