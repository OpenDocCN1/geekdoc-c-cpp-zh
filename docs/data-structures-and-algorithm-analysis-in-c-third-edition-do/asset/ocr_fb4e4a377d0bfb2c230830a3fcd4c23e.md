![](bbox=[0.218, 0.145, 0.781, 0.323])

**Figure 11.1** Examples of graphs and terminology. (a) A graph. (b) A directed graph (digraph). (c) A labeled (directed) graph with weights associated with the edges. In this example, there is a simple path from Vertex 0 to Vertex 3 containing Vertices 0, 1, and 3. Vertices 0, 1, 3, 2, and 4 also form a path, but not a simple path because Vertex 1 appears twice. Vertices 1, 3, 2, and 4 form a simple cycle.

# # 11.1 Terminology and Representations

A graph $G = (V, E)$ consists of a set of vertices $V$ and a set of edges $E$, such that each edge in $E$ is a connection between a pair of vertices in $V$. The number of vertices is written $|V|$, and the number of edges is written $|E|$. A graph can range from zero to a maximum of $|V|^2$. A graph with relatively few edges is called **sparse**, a graph containing all possible edges with many edges is called **dense**.

A graph with edges directed from one vertex to another (as in Figure 11.1(b)) is a *directed graph* or **digraph**. A graph whose edges are not directed is an *undirected graph* (as illustrated in Figure 11.1(a)). A graph with labels associated with its edges (as in Figure 11.1(c)) is a **labeled graph**. Two vertices are **adjacent** if they are joined by an edge. Two vertices are **neighbors** when connecting Vert $U$ and $V$. Such an edge is said to be **incident** on Vert $U$ and $V$. Associated with each edge may be a cost or **weight**. Graphs with weights (as in Figure 11.1(c)) are said to be **weighted**.

A sequence of vertices $v_1, v_2, \dots v_n$ forms a path of length $n - 1$ if there exists edges from $v_i$ to $v_{i+1}$ for $1 \le i < n$. A path is **simple** if all the vertices on the path are distinct. The **length** of a path is the number of edges it contains. A **cycle** is a path of length three or more that connects some vertex $v_i$ to itself. A cycle is **simple** if the path is simple, except for the first and last vertices being the same.

> Some graph applications require that a given pair of vertices can have multiple or parallel edges connecting them, or that a vertex can have an edge to itself. However, the applications discussed in this book do not require either of these special cases, for simplicity we assume they cannot occur.