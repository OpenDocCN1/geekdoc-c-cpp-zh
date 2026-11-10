**OUTPUT:** The set loop consisting of all nodes in the natural loop of *n* → *d*.

**METHOD:** Let *loop* be {*n*, *d*}. Mark *d* as “visited,” so that the search does not reach beyond *d*. Perform a depth-first search on the reverse control-flow graph starting with node *n*. Insert all the nodes visited in this search into *loop*. This procedure finds all the nodes that reach *n* without going through *d*.

**Example 9.47:** In Fig. 9.38, there are five back edges, those whose heads dominate their tails: 10 → 7, 7 → 4, 4 → 3, 8 → 3 and 9 → 1. Note that these are exactly the edges that are not shown in the flow graph.

Back edge 10 → 7 has natural loop {7, 8, 10}, since 8 and 10 are the only nodes that can reach 10 without going through 7. Back edge 7 → 4 has a natural loop consisting of {4, 5, 6, 7, 8, 10} and therefore contains the loop of 10 → 7. We thus assume the latter is an inner loop contained inside the former.

The natural loops of back edges 4 → 3 and 8 → 3 have the same header, node 3, and they also happen to have the same set of nodes: {3, 4, 5, 6, 7, 8, 10}. We shall therefore combine these two loops as one. This loop contains the two smaller loops discovered earlier.

Finally, the edge 9 → 1 has as its natural loop the entire flow graph, and therefore is the outermost loop. In this example, the four loops are nested within one another. It is typical, however, to have two loops, neither of which is a subset of the other. □

In reducible flow graphs, since all retreating edges are back edges, we can associate a natural loop with each retreating edge. That statement does not hold for nonreducible graphs. For instance, the nonreducible flow graph in Fig. 9.45 has a cycle consisting of nodes 2 and 3. Neither of the edges in the cycle is a back edge, so this cycle does not fit the definition of a natural loop. We do not identify the cycle as a natural loop, and it is not optimized as such. This situation is acceptable, because our loop analyses can be made simpler by assuming that all loops have single-entry nodes, and nonreducible programs are rare in practice anyway.

By considering only natural loops as “loops,” we have the useful property that unless two loops have the same header, they are either disjoint or one is nested within the other. Thus, we have a natural notion of innermost loops: loops that contain no other loops.

When two natural loops have the same header, as in Fig. 9.46, it is hard to tell which is the inner loop. Thus, we shall assume that when two natural loops have the same header, and neither is properly contained within the other, they are combined and treated as a single loop.

**Example 9.48:** The natural loops of the back edges 3 → 1 and 4 → 1 in Fig. 9.46 are {1, 2, 3} and {1, 2, 4}, respectively. We shall combine them into a single loop, {1, 2, 3, 4}.

However, there are another back edge 2 → 1 in Fig. 9.46, its natural loop would be {1, 2}, a third loop with header 1. This set of nodes is properly