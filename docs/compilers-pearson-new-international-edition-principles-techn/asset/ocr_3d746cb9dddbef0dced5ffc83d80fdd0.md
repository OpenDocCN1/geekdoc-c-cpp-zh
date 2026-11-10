# *9.6. LOOPS IN FLOW GRAPHS*

+   a) For what values of *n* is this graph reducible?
+   
+   b) Does your answer to (a) change if you add self-loops *i* → *i* for all nodes *i*?

! **Exercise 9.6.8:** The natural loop of a back edge *n* → *h* was defined to be *h* plus the set of nodes that can reach *n* without going through *h*. Show that *h* dominates all the nodes in the natural loop of *n* → *h*.

!! **Exercise 9.6.9:** We claimed that the flow graph of Fig. 9.45 is nonreducible. If the arcs were replaced by paths of disjoint sets of nodes (except for the endpoints, of course), then the flow graph would still be nonreducible. In fact, node 1 need not be the entry; it can be any node reachable from the entry along a path whose intermediate nodes are not part of any of the four explicitly shown paths. Prove the converse: that every nonreducible flow graph has a subgraph like Fig. 9.45, but with arcs possibly replaced by node-disjoint paths and node 1 being any node reachable from the entry by a path that is node-disjoint from the four other paths.

!! **Exercise 9.6.10:** Show that every depth-first presentation for every nonreducible flow graph has a retreating edge that is not a back edge.

!! **Exercise 9.6.11:** Show that if the following condition

\[
f(a) \land g(a) \land a \leq f(g(a))
\]

holds for all functions *f* and *g*, and value *a*, then the general iterative algorithm, Algorithm 9.25, with iteration following a depth-first ordering, converges within 2-plus-the-depth passes.

! **Exercise 9.6.12:** Find a nonreducible flow graph with two different DFST’s that have different depths.

+   ! **Exercise 9.6.13:** Prove the following:
+   
+   a) If a definition *d* is in IN[*B*], then there is some acyclic path from the block containing *d* to *B* such that *d* is in the IN’s and OUT’s all along that path.
+   
+   b) If an expression *x* + *y* is *not* available at the entrance to block *B*, then there is some acyclic path that demonstrates that fact; either the path is from the entry node and includes no statement that kills or generates *x* + *y*, or the path is from a block that kills *x* + *y* and along the path there is no subsequent generation of *x* + *y*.
+   
+   c) If *x* is live on exit from block *B*, then there is an acyclic path from *B* to a use of *x*, along which there are no definitions of *x*.