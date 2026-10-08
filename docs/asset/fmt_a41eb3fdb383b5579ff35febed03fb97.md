
To conclude this section, we present a general rule for the search of circulant graphs to determine whether they are critical or not. We can see that Theorem 23 is the following

> Definition 5. Let $n, j \in \mathbb{N}$, define the circulant graph $C_{n,j} = (\{u_0, \dots, u_{n-1}\}, E_{n,j})$ where $E_{n,j} = \{u_i, u_{i+j} \pmod n\} \cup \{u_i, u_{i-j} \pmod n\}$, where for all $i \in \{0, \dots, n-1\}$, it has

$$E_{n,j}^+ = \{u_i, u_{i+j} \pmod n\}, \quad E_{n,j}^- = \{u_i, u_{i-j} \pmod n\}$$

Thus, $C_{n,j} = CirculantGraph(n,L)$ where $L=\{j\}$. Figure 2 illustrates the graph $C_{15,3}$.

- Lemma 1. The minimum vertex cover of graph $C_{n,j}$ is $n-d_j$, a graph is critical if $n \le 2d_j$ or $n-d_j$ is a multiple of $d_j$.

- Theorem 4. $C_{n,j}$ is a critical graph if $n \le 2d_j$ or $n-d_j$ is a multiple of $d_j$.

To obtain a variety of graphs, one needs efficient generation methods and patterns. This section introduces two methods which can produce critical graphs by extending cycles of odd length. They are called the parallel extension (see Figure 3a), and the chain extension (see Figure 3b). Here let us consider the parallel extension

First, let $G = (V,E)$ be an undirected graph and $U \subseteq V$ be a subset of vertices of $G$. $U$ is called a VC-Overlap if for every vertex cover $C$ of $G$, $U \subseteq C$. If for any vertex $u \in U$, there exists a vertex cover $C$ of $G$ such that $u \in C$ and $U \setminus \{u\} \subseteq C$, then $U$ is a 1-VC-Overlap. Let $v$ be a new vertex and $U \subseteq V$. Then, the extension of $G$ as $U$ and $V$ is:

Definition 5.1. Let $G = (V,E)$ be an undirected graph and $U \subseteq V$ be a subset of vertices of $G$. $U$ is called a VC-Overlap if for every vertex cover $C$ of $G$, $U \subseteq C$. If for any vertex $u \in U$, there exists a vertex cover $C$ of $G$ such that $u \in C$ and $U \setminus \{u\} \subseteq C$, then $U$ is a 1-VC-Overlap.

`Gamma(G,U) = {u,v} | u in U, v in V}`

Observation 5.2. If $G = (V,E)$ is a VC-Overlap $U$ and $V$, then the minimum vertex cover of $G \cup U$ is given by the size of a vertex cover of $G$ plus $|U|$.

Observation 5.3. If $G$ is a critical graph $(V,E)$, a 1-VC-Overlap $U$, and a new vertex $v$, then `Gamma(G,U)` is critical.

Theorem 5.4. If a graph $G=(V,E)$, $U \subseteq V$ is a 1-VC-Overlap, and a new vertex $u$ is added, then $G$ is critical if `Gamma(G,U)` is critical.

Definition 5.3 (Parallel Extension): Let $G = (V,E)$ be an undirected graph and $v \in V$ be a vertex of $G$. Define $G' = (V \setminus \{v\}, E \cup \{\{u,v\} \mid u \in U\})$ be the graph without $v$. For an undirected graph $G = (V,E)$ and a vertex $v$, `N_G(v) = {u | {u,v} in E}` denote the degree of $v$ in $G$.

![](img/447fbed58dc921d81e92b3d3f8047037_13_0.png)

Let $e=\{u,v\} \in E$ be an edge of $G$. `N_G(v) \setminus {v} = N_G(u)`. Moreover, let $G$ be family of undirected graphs, then the parallel extension `Gamma_e(G)` of `Gamma(G)` consists of graphs that can be generated from element of $G$ by adding at least $v' \in V$, it holds that $v' \in N(u) \cup \{v\}$. We call the parallel extension of $e$. Define `Gamma_e^0(G) = Gamma(G)` and `Gamma_e^k(G) = Gamma_e^{k-1}(Gamma(G))`.

```
Gamma_e^infty(G) = union_{k=0}^infty Gamma_e^k(G)
```

for transitive closure of $G$. If $G$ is single graph, then we use `Gamma_e^infty(G)` instead of `Gamma_u(G)` and `Gamma_v(G)`. minimum vertex cover for any graph $G$ in `Gamma_e^infty(G)` can be determined from minimum vertex cover of $G'$. Theorem 5.6. Let $G=(V,E)$ be undirected graph and $e=\{u,v\} \in E$ such that $u$ and $v$ are neighbor-equivalent. Let $U$ be minimum vertex cover for $G'$. Then $U \cup \{u\}$ is minimum vertex cover for $G$. Definition 5.7. Let $G$ be family of graphs with minimum vertex cover size $n$, then minimum vertex cover size of graph $G$ in `Gamma_e^infty(G)` is $n+k$.

We show that parallel extension of any critical graph gives a critical graph. Theorem 5.8. If $G$ is critical graph, then all graphs in `Gamma_e^infty(G)` are critical. Observation 5.9. Let $G$ be critical graph. Then, all cliques and all $C$ denote family of all odd length. Let $C$ denote family of three, then we assume that graph consists of only node is in $C$ and in $C'$. Moreover, we assume that graph consists of only two nodes is in $C$. Then, we have: Observation 5.10. Let $C \subset Gamma_e(G)$ and $C' \subset Gamma_e(G_1)$ where $G_1=\{u,v\}, \{u,y\}, \{y,v\} \cup \{e\}$ and if $G_2$ denotes cycle of three, then we have
