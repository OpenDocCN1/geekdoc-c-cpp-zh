
# Applications of Graphs 619

FIGURE 20-18 A spanning tree for the graph in Figure 20-11

![](img/d0cb86b2f18b2db569968ad7c743510e_645_0.png)

FIGURE 20-19 Connected graphs that each have four vertices and three edges

![](img/d0cb86b2f18b2db569968ad7c743510e_645_1.png)

- 2. A connected undirected graph that has $n$ vertices and $n-1$ edges cannot contain a cycle. To see this, with the previous observation: To be connected, a graph with $n$ vertices must have at least $n-1$ edges. If a connected graph had a cycle, you could remove any edge from cycle and still have a connected graph. Thus, a connected graph with $n$ vertices and $n-1$ edges did contain a cycle, removing the edge from cycle would leave you with a connected graph with only $n-2$ edges, which is impossible according to observation 1.
- 3. A connected graph that has $n$ vertices and more than $n-1$ edges must contain at least one cycle. For example, if you add an edge to any of the graphs in Figure 20-19, you will create a cycle within the graph. This fact is harder to establish and is left as an exercise. (See Exercise 17 at the end of this point.)

Thus, you can determine whether a graph contains a cycle by counting its vertices and edges.
It follows, that a tree, which is a connected undirected graph without cycles, must connect its $n$ nodes with $n-1$ edges. To obtain the spanning tree of a graph of $n$ vertices, you must remove edges until cycles until $n-1$ edges are left.

Two algorithms for determining a spanning tree of a graph are based on the previous algorithms and are presented next. In general, these algorithms will produce different spanning trees for any particular graph.

### The DFS spanning tree. One way to determine a spanning tree for a connected undirected graph is to traverse the graph's vertices by using a depth-first search. As you traverse the graph, mark the edges that you follow. After the traversal is complete, the graph's vertices and marked edges form a spanning tree, which is called the depth-first search (DFS) spanning tree. (Alternatively, you can remove the unversed edges from the graph to form the spanning tree.) Simple modifications to the previous iterative and recursive versions of dfs in algorithms to create a DFS spanning tree. For example, the recursive algorithm follows:

```
// Forms a spanning tree for a connected undirected graph
// beginning at vertex v using depth-first search:
// Recursive version.
dfsTree(v: Vertex)
  Mark v as visited
  for (each unvisited u adjacent to v)
  {
    Mark the edge from u to v
    dfsTree(u)
  }
```

When you apply this algorithm to the graph in Figure 20-11, the DFS spanning tree rooted at vertex a shows the order in which the algorithm visits vertices and marks edges. You should reproduce these results by tracing the algorithm.

# FIGURE 20-20 The DFS spanning tree rooted at vertex a for the graph in Figure 20-11

![](img/d0cb86b2f18b2db569968ad7c743510e_646_0.png)

The DFS spanning tree algorithm visits these vertices in this order: a, b, c, d, g, e, f, h, i. Numbers indicate the order in which the algorithm marks edges.

**The BFS spanning tree.** Another way to determine a spanning tree for a connected undirected graph is to traverse the graph's vertices by a breadth-first search. As you traverse the graph, mark the edges that you follow. After the traversal is complete, the graph's vertices and marked edges form a spanning tree, which is called the **breadth-first search (BFS) spanning tree**. (Alternatively, you can remove the unversed edges from the graph to form the spanning tree.) You can modify the previous iterative version of bfs by marking the edge between w and u before you add u to the queue. The result is the following iterative algorithm to create a BFS spanning tree:

```
// Forms a spanning tree for a connected undirected graph
// beginning at vertex v using breadth-first search:
// Iterative version.
bfsTree(v: Vertex)
  q = a new empty queue
  // Add v to queue and mark it
```

# FIGURE 20-21 The BFS spanning tree rooted at vertex *a* for the graph in Figure 20-11

![](img/d0cb86b2f18b2db569968ad7c743510e_647_0.png)

The BFS spanning tree algorithm visits vertices in this order: a, b, f, i, c, e, d, h. Numbers indicate the order in which the algorithm marks edges.

```
q.enqueue(v)
Mark v as visited
while (!q.isEmpty()) {
  q.dequeue(w)
  // Loop invariant: there is a path from vertex w to
  // every vertex in the queue q
  for (each unvisited vertex adjacent to w) {
    Mark u as visited
    Mark edge between w and u
    q.enqueue(u)
  }
}
```

When you apply this to the graph in Figure 20-11, the BFS spanning tree rooted at vertex *a* shown in Figure 20-21 indicates the order in which the algorithm visits vertices and marks edges. You should reproduce these results by tracing the algorithm.

Count a graph's vertices and edges to determine whether it contains a cycle

## 20.4.3 Minimum Spanning Trees

Imagine that a developing country hires you to design its telephone system so that all the cities can call another. However, as in Figure 20-22 shows, it is impossible to place lines between every pair of cities. The team has determined that due to mountainous terrain, $n-1$ is the minimum number of edges necessary for a graph of $n$ vertices to be connected. Thus, $n-1$ is the minimum number of lines that can connect $n$ cities.

If the cost of installing each line is the same, the problem is reduced to finding any spanning tree—that is, the **cost of the spanning tree**—is the sum of the edges in the spanning tree. Because there may be more than one spanning tree, and because the cost of different trees may vary, you need to solve the problem by selecting a spanning tree with the least cost; that is, you must select a tree for which the sum is minimal. Such a tree is called the **minimum spanning tree**, and it is not unique. There may be several minimum spanning trees for a particular graph, their costs could equal.

A minimum spanning tree of a connected undirected graph has a minimal edge-weight sum

One simple algorithm, Prim's, finds a minimum spanning tree that begins at any vertex. Initially, the tree contains only the starting vertices. At each stage, the algorithm selects a least-cost edge among those that begin with a vertex in the tree and a vertex not in the tree. The latter vertex and least-cost edge are added to the tree. The following pseudocode describes this:

```
// Determines a minimum spanning tree for a weighted,
// connected, undirected graph whose weights are
// nonnegative, beginning with any vertex v.
primAlgorithm(v: Vertex)
  Mark v as visited and include it in the minimum spanning tree
  while (unvisited vertices)
    Find the least-cost edge (v, u) from a visited v to some unvisited vertex u
    Mark u as visited
    Add u to the tree and the edge (u, v) to the minimum spanning tree
```

Minimum spanning tree algorithm

Figure 20-23 traces primAlgorithm in Figure 20-22, beginning at vertex $a$. Edges added to the tree appear as solid lines, while edges under consideration appear as dashed lines.
It is not obvious that the spanning tree primAlgorithm will be minimal. However, the proof that primAlgorithm is correct is beyond the scope of this book.

# 622 CHAPTER 20 Graphs

FIGURE 20-22 A weighted, connected undirected graph

![](img/d0cb86b2f18b2db569968ad7c743510e_648_0.png)
