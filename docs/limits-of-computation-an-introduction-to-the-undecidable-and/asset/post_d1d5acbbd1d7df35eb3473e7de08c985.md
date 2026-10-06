
More NP-Complete Problems ■ 191

![](img/d80067a1fcf4f931f840f447fc7d1650_212_0.png)

$G_1 = (V_1, E)$
Edges = $[v_1, v_2], \{v_2, v_3\}, \{v_2, v_4\}, \{v_3, v_5\}, \{v_4, v_5\}, \{v_6, v_7\}]$

$G_2 = (V_2, A)$
Arrows = $[(v_1, v_2), (v_2, v_1), (v_2, v_4), (v_2, v_3), (v_5, v_3), (v_5, v_4), (v_7, v_6)]$.

Figure 9.1 Example undirected and directed graphs.

# Definition 9.4

Two vertices are **adjacent** if there is an edge between them.

# Definition 9.5

A (simple) **path** in G from $v_i$ to $v_j$ is a sequence of nodes ($v_i = v_{k_1}, \dots, v_{k_m} = v_j$) so that:

- 1. There exists an edge between each pair $(v_{kr}, v_{k(r+1)})$ in E, $1 \le r \le m$.
- 2. No node is repeated ($v_{kr} \neq v_{ks}, r \neq s$) except possibly the first and last ($v_i = v_j$).

Sometimes, paths are allowed to have repeated vertices—be non-simple—but in what follows, we will assume that paths are simple unless stated otherwise.

Figure 9.1 showed a graph with a list of its edges. There is an simple path from $v_1$ to $v_5$; there is no path from $v_2$ to $v_6$. Graph $G_1$ in Figure 9.1 is not connected (two connected subgraphs $\{v_1, v_2, v_3, v_4, v_5\}$ and $\{v_6, v_7\}$), often called its connected components.

A path in a directed graph has arrows between successive nodes, rather than edges. A directed graph is shown in Figure 9.1.

# 192 ■ Limits of Computation

![](img/d80067a1fcf4f931f840f447fc7d1650_213_0.png)

GRAPH 1:

- Hamiltonian Circuit: $v_1, v_6, v_7, v_5, v_4, v_3, v_2$ (and others)
- Hamiltonian Path: $v_1, v_6, v_7, v_4, v_3, v_2$ (and others)

GRAPH 2:

- Hamiltonian Circuit: None
- Hamiltonian Path: $v_1, v_6, v_7, v_4, v_3$ (and others)

Figure 9.2 Examples of Hamiltonian circuits and paths.

A path is a circuit if the first and last nodes are the same. In $G_1, (v_3, v_5, v_0, v_2, v_3)$ is a circuit. **A Hamiltonian circuit** (in a directed or undirected graph) is a circuit that visits every vertex in the graph exactly once. **A Hamiltonian path** is a path from some vertex $v$, to a different vertex $v$, that visits all other vertices on route. See Figure 9.2 for examples.

Note that both graphs in Figure 9.2 are connected; there can never be a Hamiltonian circuit or a Hamiltonian path unless the graph is connected.

We need to consider the encoding of a graph $|G|$, since to show something is in **NP**, we will have to know the length of the encoding and find a certificate that is polynomial in this length $|G|$.

There are at least three (but course related) standard ways to encode $G$, whether directed or undirected:

- 1. An $n \times n$ adjacency matrix, where the $ij^{th}$ entry is 1 if there is an edge from $i$ to $j$, and 0 otherwise. For an undirected graph, the matrix is symmetric and there are no $i, i$ entries, only $n(n-1)/2$ entries need to be stored. For a weighted graph, the $ij^{th}$ entry is the weight on that edge (and either or a very large number if there is no edge).

Size of the encoding: $|G| = n^2$ for directed graphs (or $n^2 - n$ if there can be no arrow from a vertex back to itself), $(n^2 - n)/2$ for undirected graphs.

Example: $G_1$ from Figure 9.2 represented as an adjacency matrix (note that it is symmetric):

| 0 | 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 1 | 1 | 0 | 0 |
| 0 | 1 | 0 | 1 | 1 | 0 |
| 0 | 1 | 1 | 0 | 1 | 0 |
| 1 | 0 | 0 | 0 | 1 | 1 |
| 0 | 0 | 0 | 1 | 1 | 0 |

- 2. An adjacency list: Each vertex $v_i$ has an attached list of all vertices connected to it. In an undirected graph, each edge $e_{i,j}$ will have $v_j$ appear in $v_i$'s list and $v_i$ appear in $v_j$'s list. This is duplication of information, but eliminating the duplication would make algorithms more complicated and would only halve the representation of $|G|$. Elsewhere in the book, two encodings (or two algorithms) whose length differs by a constant factor will be considered the same.

Size of encoding: $|V| + 2|E|$ (each edge appears twice, but only one end is in list).

Example: $G_1$ stored as adjacency lists:

- 1: 2, 6
- 2: 1, 3, 4
- 3: 2, 5
- 4: 2, 5
- 5: 3, 4, 6, 7
- 6: 1, 5, 7
- 7: 5, 6

- 3. A count of the vertices ($n$) followed by a list of the edges. Here, $n$ would not be necessary if every vertex was connected to something, but that is not the case.

Size of encoding: $|G| = n + 2|E|$ (each edge appears once, but with two vertices).

Example: See the edge list for $G_1$ in Figure 9.2.

# 194 ■ Limits of Computation

| Representation | Size Estimate |
| :--- | :--- |
| Adjacency Matrix | $n^2$ |
| Adjacency List | $|V| + 2|E|$ |
| Count + Edge List | $n + 2|E|$ |

![](img/d80067a1fcf4f931f840f447fc7d1650_215_0.png)

A subtle assumption is made, and you should be questioning why one can encode $|V| = n$ in the expression above, not a better (and very close) estimate would be the smallest integer greater than $\log_{10}|V|$. If for example, the graph had $2^{85}$ nodes, and one was using decimal, it would take a length of 4 to encode $|V|$. $\log_{10} n$ is much smaller than $n$, and is essentially treated as a small constant and ignored.

So, was a good estimate for the size of $|G|$ in whatever encoding? Certainly $0 \le |E| \le n(n-1) < n^2$, where $|V| = n$. Any “interesting” graph has more than a few edges. Thus, we will generally take $n^2$ as the size of the encoding of $G$. To prove something is in NP-complete, we will have to show that there is a certificate that is polynomial in $O(n^2)$—or, if we want to use the other characterization, there is an NDTM of polynomial order in $n^2$. Note that a function is polynomial in $n^2$ if and only if it is polynomial in $n$ (a higher order in $n$, of course, but all we care about is a polynomial bound). Thus, we will often look for polynomial in $n = |V|$, although that is not exactly the size of $|G|$.

An example weighted graph (with two possible matrix encodings) is in Figure 9.3.

# 9.4 VERTEX COVER: THE FIRST GRAPH PROBLEM

# Definition 9.6

For $G = (V, E)$, a set $V' \le V$ is a vertex cover of size $k = |V|$ if every edge has at least one end in $V'$.

# 195 More NP-Complete Problems

Clearly, the set $V' = V$ is a vertex cover of size $|V|$ for any graph $G$. Also clearly, no graph (except the graph with no edges) can have a vertex cover of size 0. For other numbers $m$ between 1 and $|V| - 2$, a graph may or not have a vertex cover of size $m$.

Finding vertex covers and determining whether they exist for a given $m$ is easy for small graphs. However, imagine a graph with 100 vertices and thousands of edges. Does it have a vertex cover of, for example, 50? Perhaps yes, perhaps no, but there are a lot of possible vertex covers to try ($100!/(50!50!)$ to be exact), and for each of these possible covers, a lot of edges need to be checked.

The Vertex Cover (VC) problem is the decision problem: Given a graph $G = (V, E)$ and a number $0 \le k < |V|$, does $G$ have a vertex cover of size $k$?

# Theorem 9.7

The VC problem is NP-complete.

# Proof

- 1. Vertex cover is in NP. The certificate $c$ is the list of $m$ vertices that form the vertex cover, that is, it is the set $V'$. It is important that we do not have to find a certificate: we are given the list, and all we do is to check or verify that it is indeed a cover.

VERTEX-COVER-VERIFY (G, m, c):
- Check that each element of $c$ is an element of $V$ in $G$. If not, reject.
- Check that each element of $c$ is distinct. If not, reject.
- Check that $|c| \le m$ (of course, if $|c| = m$, we can easily find the vertex cover of size $m$).
- Check the vertices of $c$ form a vertex cover for $G$. If yes, accept.

The first three steps are simple to compute in a polynomial time. For each of the edges (and there are fewer than $n^2$ edges), the last step of the verifier goes through the list of $m < n$ vertices in the certificate, checking that one end of the edge is in $c$. Since there are at most $n^2$ to check and each requiring a list of length $< n$, the last step is bounded by $O(n^3)$.

- 2. 3-CNF-SAT $\le_P$ VC. This is another proof by component design, it is made more interesting since we are converting Boolean expressions

![](img/d80067a1fcf4f931f840f447fc7d1650_215_0.png)

Weighted Graph $G_3 = (V, E)$

FIGURE 9.3 Weighted graph and two possible representations.
