

**FIGURE 20-18 A spanning tree for the graph in Figure 20-11**

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_645_0.png)

**FIGURE 20-19 Connected graphs that each have four vertices and three edges**

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_645_1.png)

- **2. A connected undirected graph that has** $n$ **vertices and exactly** $n-1$ **edges cannot contain a cycle.** To see this, begin with the previous observation: To be connected, a graph with $n$ vertices must have at least $n-1$ edges. If a connected graph did have a cycle, you could remove any edge along that cycle and still have a connected graph. Thus, if a connected graph with $n$ vertices and $n-1$ edges did contain a cycle, removing an edge along the cycle would leave you with a connected graph with only $n-2$ edges, which is impossible according to observation 1.

- **3. A connected undirected graph that has** $n$ **vertices and more than** $n-1$ **edges must contain at least one cycle.** For example, if you add an edge to any of the graphs in Figure 20-19, you will create a cycle within the graph. This fact is harder to establish and is left as an exercise. (See Exercise 17 at the end of this chapter.)

Thus, you can determine whether a connected graph contains a cycle simply by counting its vertices and edges.

It follows, then, that a tree, which is a connected undirected graph without cycles, must connect its $n$ nodes with $n-1$ edges. Thus, to obtain the spanning tree of a connected graph of $n$ vertices, you must remove edges along cycles until $n-1$ edges are left.

Two algorithms for determining a spanning tree of a graph are based on the previous traversal algorithms and are presented next. In general, these algorithms will produce different spanning trees for any particular graph.

**The DFS spanning tree.** One way to determine a spanning tree for a connected undirected graph is to traverse the graph's vertices by using a depth-first search. As you traverse the graph, mark the edges that you follow. After the traversal is complete, the graph's vertices and marked edges form a spanning

**FIGURE 20-20 The DFS spanning tree rooted at vertex a for the graph in Figure 20-11**

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_646_0.png)

The DFS spanning tree algorithm visits vertices in this order: a, b, c, d, e, f, g, h, i. Numbers indicate the order in which the algorithm marks edges.

tree, which is called the depth-first search (DFS) spanning tree. (Alternatively, you can remove the unmarked edges from the graph to form the spanning tree.) Simple modifications to the previous iterative and recursive versions of dfs result in algorithms to create a DFS spanning tree. For example, the recursive algorithm follows:

DFS spanning tree algorithm

```
```
// Forms a spanning tree for a connected undirected graph
// beginning at vertex v by using depth-first search.
// Recursive version.
dfsTree(v: Vertex)
  Mark v as visited
  for (each unvisited vertex u adjacent to v)
    Mark the edge from u to v
    dfsTree(u)
  }
```
```

When you apply this algorithm to the graph in Figure 20-11, you get the DFS spanning tree rooted at vertex a shown in Figure 20-20. The figure indicates the order in which the algorithm visits vertices and marks edges. You should trace these results by tracing the algorithm.

**The BFS spanning tree.** Another way to determine a spanning tree for a connected undirected graph is to traverse the graph's vertices by using a breadth-first search. As you traverse the graph, mark the edges that you follow. After the traversal is complete, the graph's vertices and marked edges form a spanning tree, which is called the breadth-first search (BFS) spanning tree. (Alternatively, you can remove the unmarked edges from the graph to form the spanning tree.) You can modify the previous iterative version of bfs by marking the edge between w and u before you add u to the queue. The result is the following iterative algorithm to create a BFS spanning tree.

```
```
// Forms a spanning tree for a connected undirected graph
// beginning at vertex v by using breadth-first search.
// Iterative version.
bfsTree(v: Vertex)
  q = a new empty queue
  // Add v to queue and mark it
  q.enqueue(v)
  Mark v as visited
  while (!q.isEmpty())
  {
    q.dequeue(w)
    // Loop invariant: there is a path from vertex w to
    // every vertex in the queue q
    for (each unvisited vertex u adjacent to w)
    {
      Mark u as visited
      Mark edge between w and u
      q.enqueue(u)
    }
  }
```
```

**FIGURE 20-21 The BFS spanning tree rooted at vertex a for the graph in Figure 20-11**

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_647_0.png)

The BFS spanning tree algorithm visits vertices in this order: a, b, f, i, c, e, g, d, h. Numbers indicate the order in which the algorithm marks edges.

When you apply this algorithm to the graph in Figure 20-11, you get the BFS spanning tree rooted at vertex a shown in Figure 20-21. The figure indicates the order in which the algorithm visits vertices and marks edges. You should reproduce these results by tracing the algorithm.

## 20.4.3 Minimum Spanning Trees

Imagine that a developing country hires you to design its telephone system so that all the cities in the country can call one another. Obviously, one solution is to place telephone lines between every pair of cities. However, your engineering team has determined that due to the country's mountainous terrain, it is impossible to put lines between certain pairs of cities. The team's report contains the weighted undirected graph in Figure 20-22. The vertices in the graph represent n cities. An edge between two vertices indicates that it is feasible to place a telephone line between the cities that the vertices represent, and each edge's weight represents the installation cost of the telephone line. Note that if this graph is not connected, you will be unable to link all of the cities with a network of telephone lines. The graph in Figure 20-22 is connected, however, making the problem feasible. If you install a telephone line between each pair of cities that is connected by an edge in the graph, you will certainly solve the problem. However, this solution may be too costly. From observation 1 in the previous section, you know that n - 1 is the minimum number of edges necessary for a graph of n vertices to be connected. Thus, n - 1 is the minimum number of lines that can connect n cities.

**FIGURE 20-22 A weighted, connected, undirected graph**

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_648_0.png)

If the cost of installing each line is the same, the problem is reduced to one of finding any spanning tree of the graph. The total installation cost—that is, the cost of the spanning tree—is the sum of the costs of the edges in the spanning tree. However, as the graph in Figure 20-22 shows, the cost of installing each line varies. Because there may be more than one spanning tree, and because the cost of different trees may vary, you need to solve the problem by selecting a spanning tree with the least cost; that is, you must select a spanning tree for which the sum of the edge weights (costs) is minimal. Such a tree is called the minimum spanning tree, and it need not be unique. Although there may be several minimum spanning trees for a particular graph, their costs are equal.

A minimum spanning tree of a connected undirected graph has a minimal edge-weight sum

Minimum spanning tree algorithm

```
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
```

Figure 20-23 traces primsAlgorithm for the graph in Figure 20-22, beginning at vertex a. Edges added to the tree appear as solid lines, while edges under consideration appear as dashed lines.

It is not obvious that the spanning tree that primsAlgorithm determines will be minimal. However, the proof that primsAlgorithm is correct is beyond the scope of this book.

