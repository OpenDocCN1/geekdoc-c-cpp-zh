![](bbox=[0.18, 0.08, 0.81, 0.38])

FIGURE 15.2 A poset on 8 vertices.

```
    [[{{1, 2, 3}}, {{1}, {2, 3}}, {{1, 3}, {2}}, {{1, 2}, {3}}, {{1}, {2}, {3}}]]
```

Partial orders (posets) on a set of 8 elements, up to isomorphism:

```
    sage: C = Posets(8); C
    Posets containing 8 elements
    sage: C.cardinality()
    16999
```

Let us draw one of these posets (see Figure 15.2):

```
    sage: show(C.unrank(20))
```

One can iterate through all graphs up to isomorphism. For example, there are 34 simple graphs with 5 vertices (Figure 15.3):

```
    sage: len(list(graphs(5)))
    34
```

Here is how to draw all those with at most 4 edges (see Figure 15.3):

```
    sage: for g in graphs(5, lambda G: G.size() <= 4):
    ....:     show(g)
```

However, the set *C* of these graphs is *not yet* available in Sage; as a result, the following commands are not yet implemented:

```
    sage: C = Graphs(5); C.cardinality()
    34
    sage: Graphs(19).cardinality()
```