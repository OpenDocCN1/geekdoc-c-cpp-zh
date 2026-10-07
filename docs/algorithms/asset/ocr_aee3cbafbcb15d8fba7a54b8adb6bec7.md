different biconnected components are either disjoint or intersect in a single separating vertex.

+   (d) Collapse each biconnected component into a single meta-node, and retain individual nodes for each separating vertex. (So there are edges between each component-node and its separating vertices.) Show that the resulting graph is a tree.

DFS can be used to identify the biconnected components, bridges, and separating vertices of a graph in linear time.

+   (e) Show that the root of the DFS tree is a separating vertex if and only if it has more than one child in the tree.

+   (f) Show that a non-root vertex $v$ of the DFS tree is a separating vertex if and only if it has a child $v'$ whose descendants (including itself) has a backedge to a proper ancestor of $v$.

+   (g) For each vertex $u$ define:

```
$low(u) = \min \begin{cases} pre(u) \ pre(w) & \text{where } (v, w) \text{ is a backedge for some descendant } v \text{ of } u \end{cases}$
```

Show that the entire array of $low$ values can be computed in linear time.

+   (h) Show how to compute all separating vertices, bridges, and biconnected components of a graph in linear time. (Hint: Use $low$ to identify separating vertices, and run another DFS with an extra stack of edges to remove biconnected components one at a time.)