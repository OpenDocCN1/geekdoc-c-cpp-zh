# 8.5.4 Biconnected Components

Depth-first search traversal of a graph, one of the most important techniques used for solving a variety of problems is described in Section 8.4.1. DFS can be used to find the connected components of an undirected graph. There are a few non-trivial graph algorithmic problems to be considered.

Consider a graph modelling a communication network problem. We expect the network to be robust under failures of any of the nodes. Even if a node fails, the remaining network should still remain connected. A graph is said to be biconnected if this condition is satisfied.

Often, we need to test whether a given undirected graph is biconnected or not. A biconnected component is a maximal biconnected sub-graph of the graph G = (V, E). Edges and non-separation vertices belong to exactly one component, whereas separation vertices belong to at least two. Biconnected components contain no separation vertices or edges. A separation vertex or edge is one whose removal disconnects G. Between any two vertices, there exists at least two disjoint paths, and G has a simple cycle containing them. Any connected graph can be decomposed into a tree of biconnected components called the block tree of the graph. The blocks are attached to each other at shared vertices called cut vertices or articulation points. Specifically, a cut vertex is any vertex, which, when removed increases the number of connected components. In Fig. 8.29, the separation edge e1 is between A and B, and the separation vertex is E.

![](bbox=[0.335, 0.525, 0.765, 0.865])

Fig. 8.29 Sample graph with biconnected components