(graphs which can be drawn in the plane without edges crossing): by removing an edge from a planar graph, one obtains another planar graph; so planar graphs form a subtree of the previous tree. To generate them, exactly the same algorithm can be used, selecting only the children that are planar:

```
sage: [len(list(graphs(n, property = lambda G: G.is_planar())))
.....:  for n in range(7)]
[1, 1, 2, 4, 11, 33, 142]
```

In a similar fashion, one can generate any family of graphs closed under edge-deletion, and in particular any family characterised by forbidden subgraphs. This includes for example forests (graphs without cycles), bipartite graphs (graphs without odd cycles), etc. This approach can also be applied to generate:

+   - partial orders, via the bijection with Hasse diagrams (directed graphs without cycles and without edges implied by the transitivity of the order relation);
+   - lattices, via the bijection with the meet semi-lattice obtained by deleting the maximal vertex; in this case an augmentation by vertices rather than by edges is used.

**Pólya Enumeration.** We now count graphs on $n$ vertices up to isomorphism, using Pólya enumeration. We remain voluntarily brief and informal; the reader is encouraged to focus on the examples to get an intuition of what is going on. Our purpose is indeed merely to point to this gem of algebraic combinatorics that connects enumerative combinatorics, group theory, symmetric functions, and in fact even some representation theory. For details on the theory behind it, we refer to https://en.wikipedia.org/wiki/Cycle_index.

As above, we fix $V = \{1, 2, \ldots, n\}$ as the set of vertices. In the examples, we take $n = 4$. A labelled graph is now just a subset $E$ of the collection $F$ of the $\binom{n}{2}$ pairs $\{i, j\}$ of vertices:

```
sage: V = [1,2,3,4]
sage: F = Subsets(V, 2); F.list()
[{1, 2}, {1, 3}, {1, 4}, {2, 3}, {2, 4}, {3, 4}]
```

We take the group $S_n$ of all permutations of $V$:

```
sage: S = SymmetricGroup(V)
```

We want to let $S_n$ act on pairs in $F$. We start with a function that lets a single permutation act on a pair:

```
sage: def on_pair(sigma, pair):
.....:     return Set(sigma(i) for i in pair)
sage: def on_pairs(sigma):
.....:     return [on_pair(sigma, e) for e in F]
```

Here it is in action:

```
sage: sigma = S.an_element(); sigma
```