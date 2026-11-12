# FIGURE 20-22 A weighted, connected, undirected graph

![](bbox=[0.35, 0.14, 0.8, 0.34])

the previous section, you know that n - 1 is the minimum number of edges necessary for a graph of n vertices to be connected. Thus, n - 1 is the minimum number of lines that can connect n cities.

If the cost of installing each line is the same, the problem is reduced to one of finding any spanning tree of the graph. The total installation cost—that is, the cost of the spanning tree—is the sum of the costs of the edges in the spanning tree. However, as the graph in Figure 20-22 shows, the cost of installing each line varies. Because there may be more than one spanning tree, and because the cost of different trees may vary, you need to solve the problem by selecting a spanning tree with the least cost; that is, you must select a spanning tree for which the sum of the edge weights (costs) is minimal. Such a tree is called the minimum spanning tree, and it need not be unique. Although there may be several minimum spanning trees for a particular graph, their costs are equal.

A minimum spanning tree of a connected undirected graph has a minimal edge-weight sum

Minimum spanning tree algorithm

```
// Determines a minimum spanning tree for a weighted,
connected, undirected graph whose weights are
nonnegative, beginning at any vertex v.
primsAlgorithm(v: Vertex)
Mark vertex v as visited and include it in the minimum spanning tree
while (there are unvisited vertices)
    { Find the least-cost edge (v, w) from a visited vertex v to some unvisited vertex u
      Mark u as visited
      Add the vertex u and the edge (v, w) to the minimum spanning tree
    }
```

Figure 20-23 traces primsAlgorithm for the graph in Figure 20-22, beginning at vertex a. Edges added to the tree appear as solid lines, while edges under consideration appear as dashed lines.

It is not obvious that the spanning tree that primsAlgorithm determines will be minimal. However, the proof that primsAlgorithm is correct is beyond the scope of this book.