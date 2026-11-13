requires, on the average (|E| / |V|) time, which may result in cubic complexity for dense graphs to add all edges.

+   ii) The adjacency list does not allow us to make an efficient implementation if a dynamic change of vertex number is required. Adding a new vertex can be done in O (V), but removal results in O (E) complexity.

# Orthogonal List

Alternatively, one could adopt a simplified version of the list structure called orthogonal list used for sparse matrix representation. Each vertex would now have four fields and would represent one edge.

The vertex structure would be

```
struct vertex
{
    int head, tail;
    struct vertex *hp, *tp;
};
```

# Example:

![](bbox=[0.203, 0.383, 0.852, 0.542])

# Figure 9.21: Orthogonal list representation for a Directed Graph (G)

# Adjacency Multi-lists

Adjacency multi-lists are an edge based, rather than vertex based in the graph representation. In the adjacency list representation of an undirected graph, each edge (v1, v2) is represented by two entries. One on the list for v, and the other on the list vs. As it is observed in some situation, it is necessary to be able to determine the second entry for a particular edge and mark that edge as already having been examined. This can be accomplished easily if the adjacency lists are actually maintained as multi-list.

For each edge, there will be exactly one vertex, but this vertex will be in two lists. The vertex structure is

```
struct vertex
{
    int m;
    int v1, v2;
    struct vertex *p1, *p2;
};
```

| Mark(m) | 1st vertex(v1) | 2nd vertex(v2) | 1st path(p1) | 2nd path(p2) |
|---|---|---|---|---|