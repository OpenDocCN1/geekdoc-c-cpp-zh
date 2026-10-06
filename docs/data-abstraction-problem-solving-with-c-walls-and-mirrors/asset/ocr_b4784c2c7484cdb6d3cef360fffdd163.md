# FIGURE 20-20 The DFS spanning tree rooted at vertex a for the graph in Figure 20-11

![](bbox=[0.198, 0.143, 0.613, 0.335])

The DFS spanning tree algorithm visits these vertices in this order: a, b, c, d, g, e, f, h, i. Numbers indicate the order in which the algorithm marks edges.

tree, which is called the depth-first search (DFS) spanning tree. (Alternatively, you can remove the unversed edges from the graph to form the spanning tree.) Simple modifications to the previous iterative and recursive versions of dfs in algorithms to create a DFS spanning tree. For example, the recursive algorithm follows:

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

**The BFS spanning tree.** Another way to determine a spanning tree for a connected undirected graph is to traverse the graph's vertices by a breadth-first search. As you traverse the graph, mark the edges that you follow. After the traversal is complete, the graph's vertices and marked edges form a spanning tree, which is called the **breadth-first search (BFS) spanning tree**. (Alternatively, you can remove the unversed edges from the graph to form the spanning tree.) You can modify the previous iterative version of bfs by marking the edge between w and u before you add u to the queue. The result is the following iterative algorithm to create a BFS spanning tree:

```
// Forms a spanning tree for a connected undirected graph
// beginning at vertex v using breadth-first search:
// Iterative version.
bfsTree(v: Vertex)
q = a new empty queue
  // Add v to queue and mark it
```