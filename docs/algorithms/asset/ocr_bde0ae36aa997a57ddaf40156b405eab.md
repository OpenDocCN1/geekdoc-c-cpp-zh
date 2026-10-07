# Chapter 3

# Algorithms 87

Thus depth-first search is trivially adapted to check if a graph is connected, and more generally, to assign each node v an integer cnum[v] identifying the connected component to which it belongs. All it takes is

```
procedure revisit(v)
  ccnum[v] = cc
```

where cc needs to be initialized to zero and to be incremented each time the DFS calls explore.

# 3.2.4 Previsit and postvisit orderings

We have seen how depth-first search—a few unassuming lines of code—is able to uncover the connectivity structure of an undirected graph in linear time. But it is far more versatile than this. In order to stretch it further, we will collect a list more information during the exploration process: for each node, we will note down the times of two important events, the moment of first discovery (previsit) and that of final departure (postvisit). Figure 3.6 shows these numbers for our earlier example, in which there are 24 events. The fifth event is the discovery of I. The 21st event consists of leaving D for good.

One way to generate arrays pre and post with these numbers is to define a simple counter clock, initially set to 1, which gets updated as follows.

```
procedure revisit(v)
pre[v] = clock
clock = clock + 1
```

```
procedure postvisit(v)
post[v] = clock
clock = clock + 1
```

These timings will soon take on larger significance. Meanwhile, you might have noticed from Figure 3.4 that:

Property For all nodes u and v, the two intervals [pre(u), post(u)] and [pre(v), post(v)] are disjoint or one is contained within the other.

Why? Because [pre(u), post(u)] is essentially the time during which vertex was on the stack. The last-first-out behavior of a stack explains the rest.

# 3.3 Depth-first search in directed graphs

# 3.3.1 Types of edges

Our depth-first search algorithm can run verbatim on directed graphs, taking care to traverse edges only in their prescribed directions. Figure 3.7 shows an example of the search tree that results when vertices are considered in lexicographic order.