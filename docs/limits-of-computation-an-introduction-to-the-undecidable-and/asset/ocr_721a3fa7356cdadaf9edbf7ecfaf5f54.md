# Problem

Given a directed graph G and an integer m, does G contain a feedback vertex set (FVS) of size m?

# Definition 9.10

A k-clique in a graph G is a complete graph on k vertices that is a subgraph of G.

# Problem

Given a graph G and an integer k, does G contain a k-clique?

# Definition 9.11

A dominating set of size m in a graph G is a set of vertices V’ such that every vertex of G is connected by an edge to some vertex in V’.

> Aside: How is this definition different from a vertex cover? In a triangle graph, what is the smallest vertex cover? What is the smallest dominating set?

# Problem

Given a graph G and an integer m, does G contain a dominating set of size m?

# Definition 9.12

A graph G = (V, E) can be colored with m colors c₁, c₂, ..., cm (1 ≤ m ≤ |V|) if there is a way to assign the colors cj to the vertices vj such that no two adjacent vertices have the same color. Such an assignment of m colors to V is called an m-coloring.