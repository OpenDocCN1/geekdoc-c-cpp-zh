
# Figure 4.16 Operations on a binary heap.

```
procedure insert(h, x)
bubbleup(h, x, |h| + 1)
```

```
procedure decrease_key(h, x)
bubbleup(h, x, h^{-1}(x))
```

```
function deletemin(h)
if |h| = 0:
  return null
else:
  x = h(1)
  siftdown(h, |h|, 1)
  return x
```

```
function makeheap(S)
h = empty array of size |S|
for x ∈ S:
  h(|h|+1) = x
for i = |S| downto 1:
  siftdown(h, h(i), i)
return h
```

```
procedure bubbleup(h, x, i)
(place element x in position i of h, and let it bubble up)
p = [i/2]
while i ≠ 1 and key(h(p)) > key(x):
  h(i) = h(p); i = p; p = [i/2]
h(i) = x
```

```
procedure siftdown(h, x, i)
(place element x in position i of h, and let it sift down)
c = minchild(h, i)
while c ≠ 0 and key(h(c)) < key(x):
  h(i) = h(c); i = c; c = minchild(h, i)
h(i) = x
```

```
function minchild(h)
(return the index of the smallest child of h)
if 2i > |h|:
  return 0 (no children)
else:
  return argmin(key(h(j)): 2i ≤ j ≤ min(|h|, 2i+1)
```

## 124

4.17. Suppose to run Dijkstra's algorithm on a graph whose edge weights are integers in the range 0, 1, ..., W, where W is a relatively small number.

- (a) Show Dijkstra's algorithm can be made to run in time $O(|V| + |E|)$.
- (b) Show an alternative implementation that takes just $O(|V| + |E| \log W)$.

4.18. In cases where there are several shortest paths between two nodes (and edges having lengths), the most convenient of these paths is *the one* with fewest edges. For instance, if nodes represent cities and edge lengths represent of flying between cities, there might be many ways to get city s to city t which all have the same cost. The most convenient of these alternatives is the one which involves the fewest stopovers. Accordingly, for a specific starting node s, define

$best[u] = minimum\ number of edges in a shortest path from s to u$.

In the example, the best values for nodes S, A, B, C, D, E, F are 0, 1, 1, 2, 2, 3, respectively.

![](img/3dd1f1364df8f87b80683fc32a15b999_134_0.png)

Give an efficient algorithm for the following problem.

Input: Graph $G = (V, E)$; positive edge lengths $l_e; s \in V$.
Output: The values of $best[u]$ should be for all nodes $u \in V$.

4.19. Generalized shortest-paths problem. In Internet routing, there are delays on lines but also more, delays at routers. This motivates a generalized shortest-paths problem.

Suppose that in adding edge lengths $[l_e : e \in E]$, a graph also has vertex costs $[c_v : v \in V]$. Now define the cost of a path to be the sum of its edge lengths, plus the costs of all vertices on the path (including the endpoints). Give an efficient algorithm for the following problem.

Input: A directed graph $G = (V, E)$; positive edge lengths $l_e$ and positive vertex costs $c_v$; a starting vertex $s \in V$.
Output: An array $cost[]$ that for every vertex $u$, $cost[u]$ is the least cost of any path from $s$ to $u$ (i.e., the cost of the cheapest path). Notice that $cost[s] = c_s$.

4.20. There is a network of roads $G = (V, E)$ connecting a set of cities $V$. Each road has an associated length $l_e$. There is a proposal to add one new road from a list $E'$ of pairs which can be built. As a designer for the public works, you are asked to determine road $e' \in E'$ whose addition to the existing network would result in the maximum decrease in the distance between two cities $s$ and $t$. Give an efficient algorithm for solving this.

4.21. Shortest path algorithms can be applied in currency trading. Let $c_1, \dots, c_n$ be various currencies; for instance $c_1$ might be dollars. For any two currencies $c_i$ and $c_j$, there is an exchange rate $r_{ij}$, which that you can purchase $r_{ij}$ units of $c_j$ for one unit of $c_i$. The exchange rates satisfy the condition $r_{ij}r_{ji} < 1$, so if you start with a unit of $c_i$, change it into $c_j$ and then convert back to $c_i$, you end up with less than one unit of $c_i$. Such anomalies last only a fraction of a minute, but they provide an opportunity for risk-free profits.

- (A) Give an algorithm for the following problem: Given a set of exchange rates $r_{ij}$ and two currencies $s$ and $t$, find the most advantageous sequence of currency exchanges for converting currency $s$ into currency $t$.
- (B) Give an algorithm for detecting the presence of such an anomaly. Use the graph representation found above.

4.22. The tramp problem. Suppose you are the owner of a ship that can travel between a group of port cities $V$. You make money at each port: a visit to city $i$ earns you a profit of $p_i$ dollars. Meanwhile, the transportation cost from port $i$ to port $j$ is $c_{ij} > 0$. You want to find a cyclic route in which the ratio of profit is maximized. To this end, consider a directed graph $G = (V, E)$ whose nodes are ports, and has edges between each pair of ports. For any cycle $C$ in this graph, the profit-to-cost ratio is

$r(C) = \frac{\sum_{(i,j) \in C} p_i}{\sum_{(i,j) \in C} c_{ij}}$

Let $r^*$ be the maximum ratio achievable by a simple cycle. One way to determine $r^*$ is by binary search: by first guessing some ratio $r$, and then testing whether it is too large or small.

Consider any positive $r > 0$. Give each edge $(i, j)$ a weight of $w_{ij} = r^{c_{ij}} - p_j$.

- (a) Show that if there is a cycle of negative weight, $r < r^*$.
- (b) Show that if all cycles in the graph have strictly positive weight, then $r > r^*$.
- (c) Give an efficient algorithm that takes as input a desired accuracy $\epsilon > 0$ and returns a simple cycle $C$ for which $r(C) \geq r^* - \epsilon$. Justify the correctness of your algorithm and analyze its running time in terms of $|V|, \epsilon$, and $R = \max_{(i,j) \in E}(p_j/c_{ij})$.

# Chapter 5
Greedy algorithms

A game like chess can be won only by thinking ahead: a player who is focused entirely on immediate advantage is easy to defeat. But in many other games, as Scrabble, it is possible to do quite well by simply making whichever seems best at the moment and not worrying too much about future consequences.

This sort of behavior is easy and convenient, making it an attractive algorithmic strategy. Greedy algorithms build up a solution by piece, always choosing the next piece that offers the most obvious and immediate benefit. Although such an approach can be disastrous for some computational tasks, there are many for which it is optimal. Our first example is that of minimum spanning trees.

# 5.1 Minimum spanning trees

Suppose we are asked to network a collection of computers by linking pairs of them. This translates into a graph problem in which nodes are computers, undirected edges are potential links, and the goal is to pick each of these edges that the nodes are connected. This is not at all; each link also has a maintenance cost, reflected in that edge's weight. What is the cheapest possible network?

![](img/3dd1f1364df8f87b80683fc32a15b999_137_0.png)

**Property 1** Removing a cycle edge cannot disconnect a graph.

So the solution must be connected and acyclic: undirected graphs of this kind are called trees. The particular tree we want is the one with minimum total weight, known as the minimum spanning tree. Here is its formal definition.
