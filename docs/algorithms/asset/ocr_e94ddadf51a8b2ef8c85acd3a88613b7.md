# 124

4.17. Suppose we to run Dijkstra's algorithm on a graph whose edge weights are integers in the range 0, 1, ..., W, where W is a relatively small number.

+   (a) Show Dijkstra's algorithm can be made to run in time
$O(|V| + |E|).

+   (b) Show an alternative implementation that takes just
$O(|V| + |E| \log W$.

4.18. In cases where are several shortest paths between two nodes (and edges having lengths), the most convenient of these paths is *the one* with fewest edges. For instance, if nodes represents cities edge lengths represents of flying between cities, there might be many ways to get city s to city t which all have the same cost. The most convenient of these alternatives is the one which involves the fewest stopovers. Accordingly, for a specific starting node s, define

$best[u] = minimum number of edges in a shortest path from s to u$.

In the example, the best values for nodes S, A, B, C, D, E, F are
0, 1, 1, 2, 2, 3, respectively.

![](bbox=[0.2, 0.4, 0.6, 0.54])

Give an efficient algorithm for the following problem.

Input: Graph $G = (V, E)$; positive edge lengths $l_e; s \in V$.
Output: The values of $best[u]$ should be for all nodes $u \in V$.

4.19. Generalized shortest-paths problem. In Internet routing, there are delays on lines but also more, delays at routers. This motivates a generalized shortest-paths problem.

Suppose that in adding edge lengths $[l_e : e \in E]$, a graph also has vertex costs $[c_v : v \in V]$. Now define the cost of a path to be the sum of its edge lengths, plus the costs of all vertices on the path (including the endpoints). Give an efficient algorithm for the following problem.

Input: A directed graph $G = (V, E)$; positive edge lengths $l_e$ and positive
vertex costs $c_v$; a starting vertex $s \in V$.
Output: An array $cost[]$ that for every vertex $u$, $cost[u]$ is the least
cost of any path from $s$ to $u$ (i.e., the cost of the cheapest path), under the
def above.

Notice that $cost[s] = c_s$.

4.20. There is a network of roads $G = (V, E)$ connecting a set of cities $V$. Each road in
 has an associated length $l_e$. There is a proposal to add one new road to this

Exercises