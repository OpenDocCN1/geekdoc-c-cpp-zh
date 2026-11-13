tree. A minimum spanning tree (MST) is defined as a spanning tree with weight less than or equal to the weight of every other spanning tree. In other words, a minimum spanning tree is a spanning tree that has weights associated with its edges, and the total weight of the tree (the sum of the weights of its edges) is at a minimum.

# An Analogy

Take an analogy of a cable TV company laying cable in a new neighbourhood. If it is restricted to bury the cable only along particular paths, then we can make a graph that represents the points that are connected by those paths. Some paths may be more expensive (due to their length or the depth at which the cable should be buried) than the others. We can represent these paths by edges with larger weights.

Therefore, a spanning tree for such a graph would be a subset of those paths that has no cycles but still connects to every house. Many distinct spanning trees can be obtained from this graph, but a minimum spanning tree would be the one with the lowest total cost.

# Properties

**Possible multiplicity** There can be multiple minimum spanning trees of the same weight. Particularly, if all the weights are the same, then every spanning tree will be minimum.

**Uniqueness** When each edge in the graph is assigned a different weight, then there will be only one unique minimum spanning tree.

**Minimum-cost subgraph** If the edges of a graph are assigned non-negative weights, then a minimum spanning tree is in fact the minimum-cost subgraph or a tree that connects all vertices.

**Cycle property** If there exists a cycle c in the graph G that has a weight larger than that of other edges of c, then this edge cannot belong to an MST.

**Usefulness** Minimum spanning trees can be computed quickly and easily to provide optimal solutions. These trees create a sparse subgraph that reflects a lot about the original graph.

**Simplicity** The minimum spanning tree of a weighted graph is nothing but a spanning tree of the graph which comprises of n-1 edges of minimum total weight. Note that for an unweighted graph, any spanning tree is a minimum spanning tree.

# Example 13.5

Consider an unweighted graph G given below (Fig. 13.28). From G, we can draw many distinct spanning trees. Eight of them are given here. For an unweighted graph, every spanning tree is a minimum spanning tree.

![](bbox=[0.25, 0.705, 0.78, 0.84])

Figure 13.28 Unweighted graph and its spanning trees

# Example 13.6

Consider a weighted graph G shown in Fig. 13.29. From G, we can draw three distinct spanning trees. But only a single minimum spanning tree can be obtained, that is, the one that has the minimum weight (cost) associated with it.