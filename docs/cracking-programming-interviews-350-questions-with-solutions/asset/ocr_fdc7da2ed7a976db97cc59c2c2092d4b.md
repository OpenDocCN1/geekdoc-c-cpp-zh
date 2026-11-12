connected, the running time is $O(|E|\log |V|)$. If we use a Fibonacci heap, the running time is $O(|V|\log |V|+|E|)$. In addition, we need to compute the minimum cost distribution. Dijkstra’s algorithm computes backpointers $\pi[v]$ to represent the shortest paths. We can use these to represent the distribution; when asked for the shortest path from $s$ to $v$, we trace the backpointers from $v$ to $s$ and return the traversed edges (in reverse).

+   2. If an edge is removed from the graph, it is possible that the cost of the minimum cost distribution on the resulting graph may be more than the cost of our original cheapest distribution. That is, let $D$ be the minimum cost distribution found in the first part, and let $C(D)$ be its cost. If we remove edge $e$ from the graph, let $C(e)$ denote the cost of the minimum cost distribution for the new graph (with edge set $E-\{e\}$). We need to compute
+   
+   $$\max_{e\in E} C(e)-C(D)$$
+   
+   First recall that cost of a distribution is $\sum_{v\in V} d[v]$, where the $d[v]$ are the distance values returned by Dijkstra.
+   
+   The straightforward brute-force approach to solve this problem is compute $C(e)$ by deleting $e$ from the graph and rerunning the algorithm from the first part. However, note that if the deleted edge $e\notin D$ then $C(e)=C(D)$, since the removal of $e$ does not affect the distribution $D$. So we only need to find
+   
+   $$\max_{e\in E} C(e)-C(D)$$
+   
+   Since the edges in $D$ are a set of shortest paths, they form a tree, and it has $|V|-1$ edges. To compute $C(e)$ for an edge $e\in D$, we can delete and then rerun Dijkstra’s algorithm on the resulting graph. It is important to note that removing $e$ may make some vertices unreachable from $s$. To check this, we remove $e$, rerun Dijkstra, and then check if any of the $d$ distances are $\infty$. If so, then $C(e)=\infty$ and we should halt the algorithm and return $\infty$ as the maximum possible increase. If so, then $C(e)=\sum_v d[v]$.
+   
+   The running time of this solution is the cost of $|V|-1$ calls to Dijkstra’s algorithm. Using Fibonacci heaps, this is $O(|V|^2\log |V|+|V||E|)$.

# 5.2 Independent Set

# Problem

Given a graph $G$, we have to compute the size of a maximum independent set of $G$.