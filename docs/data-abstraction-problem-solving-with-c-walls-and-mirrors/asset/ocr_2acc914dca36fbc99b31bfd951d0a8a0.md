# FIGURE 20-21 The BFS spanning tree rooted at vertex *a* for the graph in Figure 20-11

![](bbox=[0.068, 0.146, 0.513, 0.335])

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

When you apply this to the graph in Figure 20-11, you get the BFS spanning tree rooted at vertex *a* shown in Figure 20-21. The figure indicates the order in which the algorithm visits vertices and marks edges. You should reproduce these results by tracing the algorithm.

# 20.4.3 Minimum Spanning Trees

Imagine that a developing country hires you to design its telephone system so that all the cities in the country can call one another. Obviously, one solution is to place lines between every pair of cities. However, your engineering team has determined that due to the mountainous terrain, it is impossible to put lines between pairs of cities. The team's report contains the weighted undirected graph in Figure 20-22. The vertices in the graph represent n cities. An edge between two vertices indicates that it is feasible to place a telephone line between the vertices, and each edge weight represents the installation cost of the telephone line. Note that if the graph is not connected, you will be unable to link all of the cities with a network of telephone lines. The graph in Figure 20-22 is connected, however, making the problem feasible.

If you install a telephone line between each pair of cities that is connected by an edge in the graph, you will certainly solve the problem. However, this solution may be too costly. From observation 1 in