![](bbox=[0.26, 0.12, 0.86, 0.52])

# FIGURE 13.8 A tree data structure

# Graphs

> KEY CONCEPT
> A graph is a non-linear data structure that connects nodes using generic edges.

Like a tree, a graph is a non-linear data structure. Unlike a tree, a graph does not have a primary entry point like the tree’s root node. In a graph, a node is linked to another node by a connection called an edge. Generally there are no restrictions on the number of edges that can be made between nodes in a graph. Figure 13.9 presents a graph data structure.

Graphs are useful when representing relationships for which linear paths and strict hierarchies do not suffice. For instance, the highway system connecting cities on a map and airline connections between airports are better represented as graphs than by any other data structure discussed so far.

In a general graph, the edges are bi-directional, meaning that the edge connecting nodes A and B can be followed from A to B and also from B to A. In a directed graph, or digraph, each edge has a specific direction. Figure 13.10 shows a digraph, in which each edge indicates the direction using an arrowhead.

A digraph might be used, for instance, to represent airline flights between airports. Unlike highway systems, which are in almost all cases bi-directional, having a flight from one city to another does not necessarily mean there is a