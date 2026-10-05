Sec.6.2 The Parent Pointer Implementation

209

![](bbox=[0.368, 0.183, 0.722, 0.298])

| Parent Index | 0 | 0 | 1 | 1 | 2 | 7 | 7 | 7 |
|---|---|---|---|---|---|---|---|---|n| Label | R | A | B | C | D | E | F | W | X | Z |
| Node Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |

**Figure 6.5** The parent pointer implementation. Each node corresponds to a position in the node array, which stores its value and a pointer to it. The parent pointers are represented by the position in the array of the parent. The root of any two trees stores ROOT, represented graphically by a slash in the “Parent’s Index” box. This figure shows two trees stored in the same parent pointer array, one rooted at R, and the other rooted at W.

![](bbox=[0.361, 0.501, 0.637, 0.606])

**Figure 6.6** A graph with two connected components.

A, H, and E would be equivalent in 6.6, but J is not equivalent to any other. A subset of equivalent (connected) edges in a graph is a connected component. The goal is to quickly classify the objects into disjoint sets that correspond to the connected components. Another application for UNION/FIND occurs in Kruskal’s algorithm for computing the minimum spanning tree for a graph (Section 11.5.2).

The input to the UNION/FIND algorithm is typically a series of equivalence pairs. In the case of the connected components example, the equivalence pairs would simply be the set of edges in the graph. An equivalence pair might say that object C is equivalent to object A. If so, C and A are placed in the same subset. If a later equivalence relates A and B, then by implication C is also equivalent to B. Thus, an equivalence pair may cause two subsets to merge, each of which contains several objects.