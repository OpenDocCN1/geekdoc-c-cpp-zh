# FIGURE 20-21 The BFS spanning tree rooted at vertex $\alpha$ for the graph in Figure 20-11

![](bbox=[0.06, 0.14, 0.5, 0.34])

The BFS spanning tree algorithm visits vertices in this order: a, b, f, i, c, e, g, d, h. Numbers indicate the order in which the algorithm marks edges.

```
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

When you apply this algorithm to the graph in Figure 20-11, you get the BFS spanning tree rooted at vertex $\alpha$ shown in Figure 20-21. The figure indicates the order in which the algorithm visits vertices and marks edges. You should reproduce these results by tracing the algorithm.

# 20.4.3 Minimum Spanning Trees

Imagine that a developing country hires you to design its telephone system so that all the cities in the country can call one another. Obviously, has one solution is to place telephone lines between every pair of cities. However, your engineering team has determined that due to the country's mountainous terrain, it is impossible to put lines between certain pairs of cities. The team's report contains the weighted undirected graph in Figure 20-22. The vertices in the graph represent n cities. An edge between two vertices indicates that it is feasible to place a telephone line between the cities that the vertices represent, and each edge's weight represents the installation cost of the telephone line. Note that if this graph is not connected, you will be unable to link all of the cities with a network of telephone lines. The graph in Figure 20-22 is connected, however, making the problem feasible. If you install a telephone line between each pair of cities that is connected by an edge in the graph, you will certainly solve the problem. However, this solution may be too costly. From observation 1 in