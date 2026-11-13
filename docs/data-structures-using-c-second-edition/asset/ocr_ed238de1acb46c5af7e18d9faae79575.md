![](bbox=[0.09, 0.1, 0.25, 0.19])

A graph can be directed or undirected. In an undirected graph, edges do not have any direction associated with them. That is, if an edge is drawn between nodes a and b, then the nodes can be traversed from A to b as well as from b to a. Figure 13.1 shows an undirected graph because it does not give any information about the direction of the edges. Look at Fig. 13.2 which shows a directed graph. In a directed graph, edges form an ordered pair. If there is an edge from a to b, then there is a path from a to b but not from b to a. The edge (a, b) is said to initiate from node a (also known as initial node) and terminate at node b (terminal node).

# ## 13.2 Graph Terminology

**Adjacent nodes or neighbours** For every edge, e = (u, v) that connects nodes u and v, the nodes u and v are the end-points and are said to be the adjacent nodes or neighbours.

**Degree of a node** Degree of a node u, deg(u), is the total number of edges containing the node u. If deg(u) = 0, it means that u does not belong to any edge and such a node is known as an isolated node.

![](bbox=[0.09, 0.4, 0.45, 0.55])

**Regular graph** It is a graph where each vertex has the same number of neighbours. That is, every node has the same degree. A regular graph with vertices of degree k is called a k-regular graph or a regular graph of degree k. Figure 13.3 shows regular graphs.

**Path** A path p written as P = (v0, v1, v2, ..., vn), of length n from a node u to v is defined as a sequence of (n+1) nodes. Here, u = v0, v = vn, and vi-1 is adjacent to vi for i = 1, 2, 3, ..., n.

**Closed path** A path p is known as a closed path if the edge has the same end-points. That is, if v0 = vn.

**Simple path** A path p is known as a simple path if all the nodes in the path are distinct with an exception that v0 may be equal to vn. If v0 = vn, then the path is called a closed simple path.

**Cycle** A path in which the first and the last vertices are same. A simple cycle has no repeated edges or vertices (except the first and last vertices).

**Connected graph** A graph is said to be connected if for any two vertices (u, v) in v there is a path from u to v. That is to say that there are no isolated nodes in a connected graph. A connected graph that does not have any cycle is called a tree. Therefore, a tree is treated as a special graph (Refer Fig. 13.4(b)).

**Complete graph** A graph g is said to be complete if all its nodes are fully connected. That is, there is a path from one node to every other node in the graph. A complete graph has n(n-1)/2 edges, where n is the number of nodes in g.

**Clique** In an undirected graph g = (V, E), clique is a subset of the vertex set C ⊆ V, such that for every two vertices in C, there is an edge that connects two vertices.

![](bbox=[0.09, 0.82, 0.45, 0.93])