
For instance, the binary relation "has the same birthday as" is an equivalence relation, whereas "is the father of" is not, since it violates all three properties.

Show that an equivalence relation partitions $S$ into disjoint $S_1, S_2, \dots, S_k$ (in words, $S = S_1 \cup S_2 \cup \dots \cup S_k$ and $S_i \cap S_j = \emptyset$ for all $i \neq j$) such that:

- Two members of a group are related, that is, $(x, y) \in R$ for any $x, y \in S_i$, and for $i$.
- Members of different groups are not related, that is, for all $i \neq j$, for all $x \in S_i$ and $y \in S_j$, we have $(x, y) \notin R$.

(Hint: Represent an equivalence relation by an undirected graph.)

3.30. On page 91, we defined the binary relation "connected" on the set of vertices of a directed graph. Show that this is an equivalence relation (see Exercise 3.29), and conclude that it partitions the vertices into disjoint strongly connected components.

3.31. Biconnected components. Let $G=(V, E)$ be an undirected graph. For any two edges $e, e' \in E$, we say $e \sim e'$ if $e=e'$ or there is a (simple) cycle containing both $e$ and $e'$.

- (a) Show that $\sim$ is an equivalence relation (recall Exercise 3.29) on the edges.

The equivalence classes into which this relation partitions the edges are called the biconnected components of $G$. A bridge is an edge which is in a biconnected component by itself.

*A separating vertex* is a vertex whose removal disconnects the graph.

- (b) Partition the edges of the graph below into biconnected components, and identify the bridges and separating vertices.

![](img/3dd1f1364df8f87b80683fc32a15b999_112_0.png)

Not only do biconnected components partition the edges of the graph, they also almost partition the vertices in the following sense.

- (c) Associate with each biconnected component all the vertices are endpoints of its edges. Show that the vertices corresponding to different biconnected components are either disjoint or intersect in a single separating vertex.

- (d) Collapse each biconnected component into a single meta-node, and retain individual nodes for each separating vertex. (So there are edges between each component-node and its separating vertices.) Show that the resulting graph is a tree.

DFS can be used to identify the biconnected components, bridges, and separating vertices of a graph in linear time.

- (e) Show that the root of the DFS tree is a separating vertex if and only if it has more than one child in the tree.

- (f) Show that a non-root vertex $v$ of the DFS tree is a separating vertex if and only if it has a child $v'$ whose descendants (including itself) has a backedge to a proper ancestor of $v$.

- (g) For each vertex $u$ define:

```
$low(u) = \min \begin{cases} pre(u) \ pre(w) & \text{where } (v, w) \text{ is a backedge for some descendant } v \text{ of } u \end{cases}$
```

Show that the entire array of $low$ values can be computed in linear time.

- (h) Show how to compute all separating vertices, bridges, and biconnected components of a graph in linear time. (Hint: Use $low$ to identify separating vertices, and run another DFS with an extra stack of edges to remove biconnected components one at a time.)

# Chapter 4

# Paths in graphs

## 4.1 Distances

Depth-first search readily identifies the vertices of a graph that can be reached from a designated starting point. It also finds explicit paths to these vertices, summarized in its search tree (Figure 4.1). However, these paths might not be the most economical ones. In the figure, vertex C is reachable from S by traversing just one edge, while the DFS tree shows a path of length 3. This chapter is about algorithms for finding shortest paths in graphs.

Path lengths allow us to talk quantitatively the extent to which different vertices of a graph are separated from each other:

> The distance between two nodes is the length of the shortest path between them. To get a concrete feel for this notion, consider a physical realization of a graph that has a ball for each vertex and a piece of string for each edge. If you lift the ball for vertex s enough, the other balls that get pulled along with it are precisely the vertices reachable from s. In Figure 4.2, for example, vertex B is at distance 2 from S, and there are two paths to it. When S is held up, the strings along each of these paths become taut.

Figure 4.1 (a) A simple graph and (b) its depth-first search tree![](img/3dd1f1364df8f87b80683fc32a15b999_14_0.png)

## 4.2 Breadth-first search

In Figure 4.2, the lifting of $s$ partitions the graph into layers: $s$ itself, the nodes at distance 1 from it, the nodes at distance 2 from it, and so on. A convenient to compute distances from $s$ to the other vertices is to proceed by layer. Once we have picked the nodes at distance $0, 1, 2, \dots$, the nodes at $d+1$ are easily determined: they are precisely the as-yet-seen nodes adjacent to the layer at distance $d$. This suggests an iterative algorithm in which two nodes are active at any time: some layer $d$, which has been fully identified, and $d+1$, which is being discovered by scanning the neighbors of layer $d$.

Breadth-first search (BFS) directly implements this simple reasoning (Figure 4.3). The initial $Q$ consists only of $s$, the node at distance 0. And for each distance $d=1, 2, \dots$, there is a point in time at which $Q$ contains all nodes at distance $d$ and nothing else. As nodes are processed (ejected from the front of the queue), their as-yet-seen neighbors are injected into the end of the queue.

Let's try this algorithm on our earlier example (Figure 4.1) to confirm it does the right thing. If $S$ is the starting point and the nodes are ordered alphabetically, they get visited in the sequence shown in Figure 4.4. The breadth-first search tree, on the right, contains the edges through which each node is initially discovered. Unlike the DFS tree we saw earlier, it has the property that all its paths from $S$ are the shortest possible. It is therefore a *shortest-path tree*.

### Correctness and efficiency

We have developed the basic intuition behind breadth-first search. In order to check that the algorithm works correctly, we need to make sure that it faithfully executes this intuition. What we expect, precisely, is that

- For each $d=0, 1, 2, \dots$, there is a moment at which (1) all nodes at distance $\le d$ from $s$ have their distances correctly set; (2) all other nodes have their distances set to $\infty$; and (3) the queue contains exactly the nodes at distance $d$.

Figure 4.3 Bread-first search.

```procedure bfs(G,s)
Input: Graph G=(V,E), directed or undirected; vertex s ∈ V
Output: For all vertices u reachable from s, dist(u) is set to the distance from s to u.
```

```
for all u ∈ V:
  dist(u) = ∞
```

```
dist(s) = 0
Q=[s] (queue containing just s)
while Q is not empty:
  u = eject(Q)
  for all edges (u, v) ∈ E:
    if dist(v) = ∞:
      inject(Q,v)
    dist(v) = dist(u) + 1
```

Figure 4.4 The result of breadth-first search on the graph of Figure 4.1.

| Order of visitation | Queue after processing node |
|---|---|
| S | [A C D E] |
| A | [C D B] |
| C | [D E B] |
| D | [E B] |
| E | [B] |
| B | [] |

![](img/3dd1f1364df8f87b80683fc32a15b999_116_0.png)

This has been phrased with an inductive argument in mind. We have already discussed both the base case and the inductive step. Can you fill in the details?

The running time of this algorithm is linear, O(|V|+|E|), for exactly the same reasons as depth-search. Each vertex is on the queue exactly once, when it is encountered, there are 2|V| queue operations. The rest of the work is done in the algorithm's innermost loop. Over the course of execution, this loop looks at each edge once (in directed graphs) or twice (in undirected graphs), and takes O(|E|) time.

Figure 4.2 A physical model of a graph![](img/3dd1f1364df8f87b80683fc32a15b999_15_0.png)

On the other hand, edge $(D, E)$ plays no role in any shortest path and therefore remains slack.
