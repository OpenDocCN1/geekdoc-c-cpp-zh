# 9.5.2 Dijkstra's Algorithm

Dijkstra's algorithm solves the single source shortest path problem when all edges have non -ve weights. It is a greedy algorithm and similar to prim's algorithm. Algorithm starts at the source vertex S it grows a tree T that ultimately spans all vertices recehable from S. Vertices are added to T in order of distance i.e/ first S, then the vertex closest to S, then the next closest and so on.

# ALGORITHM DIJKSTRA(G,W,S)

+   1. INITIALIZE-SINGLE-SOURCE(G,S)
+   2. S <- {}
+   3. Initialize Priority Queue i.e/ Q <- V[G]
+   4. While Q != phi
+   5. do u <- Extract_min(Q)
+   6. S <- S U {u}
+   7. for each vertex v E Adj[u]
+   8. do RELAX(u,v,w)

# Example:

![](bbox=[0.23, 0.5, 0.75, 0.7])

# Distance

| Steps | S | U | V | Y | X |
|---|---|---|---|---|---|
| | ∞ | ∞ | ∞ | ∞ | ∞ |
| | 0 | | | | |
| 1 | | 10 | | | 5 |
| 2 | | 8 | 14 | 7 | |
| 3 | | | 13 | | |
| 4 | | | 9 | | |