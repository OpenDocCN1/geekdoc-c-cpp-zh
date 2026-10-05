# Sec. 11.5 Minimum-Cost Spanning Trees

# 407

![](bbox=[0.273, 0.187, 0.722, 0.401])

**Figure 11.23** Prim's MST proof. The left oval contains that portion of the graph where Prim's MST and the "true" MST agree. The right oval contains the rest of the graph. The two portions of the graph are connected by (at least) $e_j$ (selected by Prim's algorithm to be in the MST) and $e'$ (the "correct" edge to be placed in Prim). Note that the path from $v_w$ to $v_j$ cannot include any marked vertex $v_i, i \le j$, because to do so would form a cycle.

# 11.5.2 Kruskal's Algorithm

Our next algorithm is commonly referred to as Kruskal's algorithm. Kruskal's algorithm is also a simple, greedy algorithm. First partition the set of vertices into $|V|$ equivalence classes (see Section 6.2), each consisting of one vertex. Then process the edges in order of weight. If an edge is added to the MST, and the edge connects two vertices in different equivalence classes, this process is repeated until only one class remains.

**Figure 11.4** 11.24 shows the first three steps of Kruskal's algorithm for the graph 11.20. Edge $(C, D)$ has the least cost, and because $C$ and $D$ are currently in separate MSTs, they are combined. We next select edge $(E, F)$ to process, and combine these vertices into a single MST. The third edge is $(C, F)$, which causes the MST containing vertices $C$ and $D$ to merge with MST containing vertices $E$ and $F$. The next edge to process is $(D, F)$. But because vertices $D$ and $F$ are currently in the same MST, this edge is rejected. The algorithm will continue on to accept edges $(B, C)$ and $(A, C)$ into the MST.

The edges can be processed in order of weight using a min-heap. This is generally faster than sorting the edges first, but in practice we need only a small fraction of the edges before completing the MST. This is an example of finding only a few smallest elements in a list, as discussed in Section 7.6.