
# 266

# Exercises

8.9. In the hitting set problem, we are given a family of sets $\{S_1, S_2, \dots, S_n\}$ and a budget $b$, and we wish to find a set $H$ of size $\le b$ which intersects every $S_i$, if such an $H$ exists. In other words, we want $H \cap S_i \neq \emptyset$ for all $i$.

Show that HITTING SET is NP-complete.

8.10. Proving NP-completeness by generalization. For each of the problems below, prove that it is NP-complete by showing that it is a generalization of some NP-complete problem we have seen in this.

- (a) SUBGRAPH ISOMORPHISM: Given input two undirected graphs $G$ and $H$, determining $G$ is a subgraph of $H$ (that is, by renaming certain vertices and edges of $H$ we obtain a graph that is, up to renaming vertices, $V(G)$ into $V(H)$).
- (b) LONGEST PATH: Given a graph $G$ and an integer $g$, find in $G$ a simple path of length $g$.
- (c) MAX SAT: Given a CNF formula and an integer $g$, find a true assignment that satisfies at least $g$ clauses.
- (d) DENSE SUBGRAPH: Given a graph and two integers $a$ and $b$, find a set of vertices of $G$ such that there are at least $b$ edges between them.
- (e) SPARSE SUBGRAPH: Given a graph and two integers $a$ and $b$, find a set of vertices of $G$ such that there are at most $b$ edges between them. (This problem generalizes two known NP-complete problems).
- (f) SET COVER: We are given two $n \times n$ matrices, a distance matrix $d_{ij}$ and a connectivity requirement $r_{ij}$ as well as a budget $b$; we want to find a graph $G = (\{1, 2, \dots, n\}, E)$ such that (the total cost of all edges is $b$ or less) and (between any two distinct vertices $i$ and $j$ there are $r_{ij}$ vertex-disjoint paths). (Hint: Suppose that all $d_{ij}$ are 1 or 2, $b=n$, and all $r_{ij}$ are 2. Which known NP-complete problem is this?)
- (g) RELIABLE NETWORK: We are given two $n \times n$ matrices, a distance matrix $d_{ij}$ and a connectivity requirement $r_{ij}$ as well as a budget $b$;

8.11. There are many variants of Rudrata's problem, depending on whether the graph is undirected or directed, and whether a cycle or path is sought. Reduce the DIRECTED HAMILTON path to each of the following.

- (a) The (undirected) HAMILTON path.
- (b) The undirected HAMILTON (s, t)-path problem, which is just like HAMILTON except that the endpoints of the path are specified in the input.

8.12. The k-Spanning tree problem is the following.

Input: An undirected graph $G = (V, E)$
Output: A spanning tree of $G$ in which each node has degree $\le k$, if such a tree exists.

Show that for any $k \ge 2$:

- (a) k-SPANNING TREE is a search problem.
- (b) k-SPANNING TREE is NP-complete. (Hint: Start with k = 2 and consider the relation between this problem and HAMILTONIAN PATH.)

8.13. Determine which of the following problems are NP-complete and which are solvable in polynomial time. In each problem you are given an undirected graph $G = (V, E)$, along with:

- (a) A set of nodes $L \subseteq V$, and you must find a spanning tree that its set of leaves includes the set $L$.
- (b) A set of nodes $L \subseteq V$, and you must find a spanning tree that its set of leaves is precisely the set $L$.
- (c) A set of nodes $L \subseteq V$, and you must find a spanning tree that its set of leaves is included in the set $L$.
- (d) An integer $k$, and you must find a spanning tree with $k$ or fewer leaves.
- (e) An integer $k$, and you must find a spanning tree with $k$ or more leaves.
- (f) An integer $k$, and you must find a spanning tree with exactly $k$ leaves.

(Hint: All the NP-completeness proofs are by generalization, except for one).

8.14. Prove that the following problem is NP-complete: given an undirected graph $G = (V, E)$ and an integer $k$, return a clique of size $k$ as well as an independent set of size $k$, provided both exist.

8.15. Show that the following problem is NP-complete.

# MAXIMUM COMMON SUBGRAPH

Input: Two graphs $G1 = (V1, E1)$ and $G2 = (V2, E2)$; a budget $b$. Output: Two sets of nodes $V1 \subseteq V1$ and $V2 \subseteq V2$ whose deletion leaves $b$ nodes in each graph, and makes the two graphs identical.

8.16. We are feeling experimental and want to create a new dish. There are various ingredients we can choose from and we'd like to use as many of them as possible, but some ingredients don't go well with others. If there are $n$ possible ingredients (numbered 1 to $n$), we write down an $n \times n$ matrix giving the discord between any pair of ingredients. This discord is a real number between 0.0 and 1.0, where 0.0 means “they go together perfectly” and 1.0 means “they really don’t go together.” Here’s an example matrix when there are five possible ingredients.

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| 1 | 0.0 | 0.4 | 0.2 | 0.9 | 1.0 |
| 2 | 0.4 | 0.0 | 0.1 | 1.0 | 0.2 |
| 3 | 0.2 | 0.1 | 0.0 | 0.8 | 0.5 |
| 4 | 0.9 | 1.0 | 0.8 | 0.0 | 0.2 |
| 5 | 1.0 | 0.2 | 0.5 | 0.2 | 0.0 |

In this case, ingredients 2 and 3 go together well whereas 1 and 5 clash badly. Notice that this matrix is necessarily symmetric; and that the diagonal entries are all 0.0. Any set of ingredients incurs a penalty which is the sum of all discount values between pairs of ingredients. For instance, the set of ingredients [1, 3, 5] incurs a penalty of 0.2 + 1.0 + 0.5 = 1.7. We want this penalty to be small.

# EXPERIMENTAL CUISINE

Input: $n$, the number of ingredients to choose from; $D$, the $n \times n$ “discord” matrix; some number $p \ge 0$
Output: The maximum number of ingredients we can choose with penalty $\le p$.

Show that if EXPERIMENTAL CUISINE is solvable in polynomial time, then so is SAT.

- 8.17. Show that for any problem $\Pi$ in NP, there is an algorithm that solves $\Pi$ in time $O(2^{p(n)})$, where $n$ is the size of the input and $p(n)$ is a polynomial.
- 8.18. Show that if $P = NP$, then the experimental problem can be solved in polynomial time.
- 8.19. A kite is a graph on $n$ vertices, say $V$, which contains a clique and a path. Given a graph $G$ on n vertices. Prove that KITE is NP-complete.
- 8.20. In an undirected graph $G = (V, E)$, we say $D \subseteq V$ is a dominating set if every $v \in V$ is either in $D$ or adjacent to at least one member of $D$. DOMINATING SET problem, input is an undirected graph $G=(V, E)$ and a budget $b$, find a dominating set of size at most $b$. Prove that this is NP-complete.
- 8.21. In scheduling, it is common to use a directed graph with one edge from task $i$ to $j$ if $i$ is a precondition for $j$. A schedule is possible if and only if the graph is acyclic; if it isn't, we'd like to identify the smallest number of constraints that must be dropped to make it acyclic. NODE-DISJOINT PATH problem, the input is an undirected graph in which vertices have been specially marked: a number of “sources” $s_1, s_2, \dots, s_n$ and number of “destinations” $t_1, t_2, \dots, t_k$. The goal is to find $k$-disjoint paths (that is, paths which have no nodes in common) where the $i$-th path goes from $s_i$ to $t_i$. Show that this problem is NP-complete.

Here is a sequence of progressively stronger hints:
(i) Reduce from 3SAT.

(ii) For a 3SAT formula with m clauses and n variables, use k=m+n sources and destinations. Introduce one source/destination pair (sx, tx) for each variable x, and one source/destination pair (sc, tc) for each clause c.
