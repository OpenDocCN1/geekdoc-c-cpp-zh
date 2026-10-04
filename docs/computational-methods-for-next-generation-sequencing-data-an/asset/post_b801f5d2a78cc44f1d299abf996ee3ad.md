
## COMPUTATIONAL METHODS FOR NGS DATA ANALYSIS

The basic scheme of the heuristics is described in Algorithm GPDA. At each iteration, Algorithm GPDA finds and adds the solution to the locally optimal pool, that is, the pool consists of compatible vertices and separates the maximal number of nonseparated samples.

```
**Algorithm GPDA:** Greedy Pool Design Algorithm
1: $H \leftarrow$ complete graph on $n$ vertices
2: $\mathcal{P} \leftarrow \emptyset$
3: while $E(H) \neq \emptyset \text{ do}$
4: find a subset $A \subseteq V$ such that the following conditions hold:
(C1) $A$ is a clique of the graph $G$;
(C2) $|A| \leq T$;
(C3) the size of the cut $(A, V \setminus A)$ in the graph $H$ is maximal.
5: $\mathcal{P} \leftarrow \mathcal{P} \cup \{A\}$
6: remove from $H$ all edges $uv$ with $u \in A$ and $v \in V \setminus A$.
7: **end while**
8: **return** $\mathcal{P}$
```

The crucial step of Algorithm GPDA finds locally optimal pool (step 4). It solves the following:

**Optimal Clique Cut Bi-Graph (OCBG) Problem.** Given a graph $G=(V, E)$ and a constant $T$, find a clique in $G$ with the set of vertices $A$ such that $|A| \leq T$ and the size of the cut $(A, V)$ is maximal.

The OCBG problem is a previously undirected optimization problem. It is easy to see that this problem is NP-hard, and it is hard to approximate within a linear factor (29).

**Theorem** OCBG Problem is not approximable within $O(n^{1-\epsilon})$ for any $\epsilon > 0$, unless $P=NP$.

**Proof.** Let an $n$-vertex graph $G'$ be the input of the maximum clique problem $G=G' \cup O'$. Without loss of generality, we assume that $G$ is connected. Consider the instance of LOP problem with $G$ and $H=K_{2n}$, as input. For the value of optimal solution of LOP, we have

```
$f_{opt} = \max[f(\omega)] = \omega(2n-\omega) : \omega = |A|, A \text{ is a clique of } G.$
```

Let us first say that the maximum clique size of $G'$ is $\omega_{opt}$ and $f_{opt} = \omega(2n-\omega_{opt})$. Indeed, by construction $\omega = |A| \leq n$ for every clique $A$ of $G$. The function $\omega(2n-\omega)$ increases monotonically on the segment $[1, n]$, and therefore $f$ reaches its maximum on $\omega_{opt} = |A_{opt}|$, where $A_{opt}$ is the maximum clique of $G$ (and of $G'$).

Let $(A, V(G) \setminus A)$ be a partition of LOP, where a $\omega = |A|$, and $f = \omega(2n-w)$. Suppose that

```
$\frac{f}{f_{opt}} \leq \frac{1}{4}|V(G)|^{1-\epsilon} = \frac{1}{4}(2n)^{1-\epsilon}$
```

## POOLING STRATEGY FOR MASSIVE VIRAL SEQUENCING

for some $\epsilon > 0$. Then.

```
$\frac{1}{2}\omega_{opt} \leq \frac{\omega_{opt}(2n-\omega_{opt})}{\omega(2n-\omega)} \leq \frac{f_{opt}}{f}(2n)^{1-\epsilon}$
```

and therefore

```
$\frac{\omega_{opt}}{\omega} \leq n^{1-\epsilon}$
```

So, if LOP is approximable within $|V(G)|^{1-\epsilon}$ for some $\epsilon > 0$, then Clique is approximable within $|V(G')|^{1-\epsilon}$. The latter is impossible, unless P=NP (34).

In Section 3.2.3, we propose an efficient heuristic to solve the OCBG problem.

### 3.2.3 The Tabu Search Heuristic for the OCBG Problem

In this section, we propose tabu search to solve the OCBG problem. Let $M = |E(H)|+1$. OCBGP can be formulated as the following quadratic programming problem:

```
maximize $f(x) = \frac{1}{2}\sum_{ij\in E(H)}(1-x_ix_j)-\frac{1}{8}\sum_{ij\in E(G)}(x_i+x_j)(x_i+x_j+2)$ (3.5)
```

subject to

```
$\frac{1}{2}\sum_{i\in V}(x_i+1) \leq T;$ (3.6)
```

```
$x_i \in \{-1, 1\}, i \in V.$ (3.7)
```

There is a one-to-one correspondence between solutions $x$ of the problems (3.5)-(3.7) and the pairs of sets $(A_x, B_x)$. $A_x=V$, where $A_x=\{i:x_i=1\}$ and $B_x=\{i:x_i=-1\}$.

The term $\frac{1}{2}\sum_{ij\in E(H)}(1-x_ix_j)$ is equal to the size of the cut $(A_x, B_x)$ in $H$. The term $\frac{1}{8}\sum_{ij\in E(G)}(x_i+x_j)(x_i+x_j+2)$ is equal to the number of nonadjacent pairs of vertices in the induced subgraph $G(A_x)$; in particular, it is equal to 0 if $A_x$ is a clique. Therefore, for any optimal solution of the problems (3.5)-(3.7), the set $A_x$ is a clique. The constraint (3.6) ensures that $|A_x| \leq T$.

We relax the constraint (3.6). Suppose $(A_x, B_x)$ is a feasible solution of (3.5)-(3.7). For a vertex $u \in A_x$, consider the solution $(A_{u'}, B_{u'})$, where $A_{u'} = A_x \setminus \{v\}$, $B_{u'} = B_x \cup \{u\}$.

```
$\Delta_1 = deg_{A_x}^H(v) - deg_{B_x}^H(v) + deg_{A_x}^G,$ (3.8)
```

where $deg_U^H(v)$ denotes the number of vertices from the set $U \subseteq V$ adjacent to vertex $v$ in graph $H$ and $G$ is the complement of $G$. If $v$ is nonadjacent to some vertex $u \in A_s$, then $\Delta_1 > 0$. Analogously, for $v \in B_s$, the solution $(A'_s, B'_s)$ with $A'_s = A_s \cup \{v\}$, $B'_s = B_s \setminus \{v\}$ and $\Delta_2 = f(A'_s, B'_s) - f(A_s, B_s)$, we have

```
$\Delta_2 = deg_{B_s}^H(v) - deg_{A_s}^H(v) - deg_{B_s}^G.$ (3.9)
```

Thus, according to relations (3.8) and (3.9), any initial solution $(A, B)$ is iteratively improved by moving vertices from one part of partition until a local optimum is reached, and the obtained solution cannot be further improved. According to (3.8), local optimum is a clique.

The major drawback of such search strategies is that the value of the objective function in a local optimum may be far from globally optimal solution. Another problem, which is specific to our case, is that it is possible the size of locally optimal cut in $H$ is 0. In this case, the solution found at stage (4) of Algorithm GPDA does not decrease $E(H)$, and therefore Algorithm GPDA will go into infinite loop. To solve these problems, we use variation of tabu strategy (3.5). The basic idea is that after the move of vertex $v$ the algorithm arrives at local optimum, the following actions are taken: the value of local optimum is compared to current best solution, $v$ is placed back, and the move of $v$ is prohibited for the next $k_i$ iterations. This is implemented in following Algorithm OCGBP, which is described in more detail. Let $tabu^i = \{tabu_1^i, \dots, tabu_j^i\}$ be tabu state at iteration $i$, that is, sequence of integers, where $tabu_j$ is number of iterations during it is not allowed to move vertex $v$. Let $optStates^i$ be set of optimal states, that is, set of pairs $((A, B), t_{A,B})$, where $(A, B)$ is local optimum found by the algorithm at some iteration $j < i$ and $t_{A,B}$ is tabu state at that iteration, that is $t_{A,B}=tabu'$. Let $(A^*, B^*)$ be current record cut, that is, cut of best size $c(A^*, B^*)$ found by the algorithm before the $i$th iteration. Let also moveList be sequence of vertices moved by the algorithm from one part of cut to another in order of move. This sequence is easier to implement as stack, and allows the algorithm to return to previous solutions when neighborhoods of solutions are completely explored. Let $k_i$ denote initial number of steps for which move of vertex is prohibited.

### Algorithm OCGBP: Optimal Cut Bi-Graph Problem

```
1: Find solution (X, Y) of 0.5-approximation algorithm for Maximum Cut applied to graph H.
2: Apply to initial solutions $(A^0, B^0) = (X, Y)$ and $(A^0, B^0) = (Y, X)$
3: $i \leftarrow 0$; tabu $\leftarrow (0, \dots, 0)$; optStates $\leftarrow \emptyset$; moveList $\leftarrow \emptyset$
4: while true
5: for $u \in V$ calculate $\delta_u$ using relations (3.8),(3.9):
   $\delta_u \leftarrow 1$, if $u \in A$ and $tabu_u = 0$;
   $\delta_u \leftarrow 2$, if $u \in B$ and $tabu_u = 0$;
   0, if $tabu_u > 0$;
6: end for
7: $\delta^* \leftarrow \max\{\delta_i\}$; $u^* \leftarrow \arg \max_{i=1,\dots,n} \{\delta_i\}$
8: Update the tabu state, that is,
   $tabu \leftarrow tabu-1$, if $tabu>0$;
   0, otherwise;
9: if $\delta^* > 0$ move the vertex $u^*$ to another part of the cut $(A^*, B^*)$
10: Push $u^*$ into the stack moveList
11: end if
12: if $\delta^* = 0$
13: if $c(A^*, B^*) > c(A^*, B^*)$ then $(A^*, B^*) \leftarrow (A^*, B^*)$
14: end if
15: if moveList $\neq \emptyset$ then pop $v$ from moveList and move $v$ back
16: Forbid the vertex $v$ for the next $k$ iterations: $tabu^{i+1} \leftarrow k_r$;
17: end if
18: $s \leftarrow ((A^{i+1}, B^{i+1}), tabu^{i+1})$
19: if $s \in optStates$ then optStates $U[s]$; $i \leftarrow i+1$ continue
20: else
21: while $|A^*| > T$ do $a \leftarrow \argmin[deg_{B^}^*(a) - deg_{A^}^*(a), | a \in A^*]$
22: $(A^*, B^*) \leftarrow (A^* \setminus \{a\}, B^* \cup \{a\})$
23: end while
24: return $(A^*, B^*)$
25: end if
26: end while
```
