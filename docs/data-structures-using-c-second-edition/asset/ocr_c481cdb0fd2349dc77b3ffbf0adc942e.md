| when k = 0 | t*ij = { 0 if (i, j) is not in E ... } |
|---|---|
| when k >= 1 | t*ij = t^(k-1)ij V (t^(k-1)ik ^ t^(k-1)kj) |

The algorithm to find the transitive closure of a graph G is given in Fig. 13.8. In order to determine the transitive closure of a graph, we define a matrix t where t*ij = 1, for i, j, k = 1, 2, 3, ... n if there exists a path in G from the vertex 1 to vertex j with intermediate vertices in the set (1, 2, 3, ..., k) and 0 otherwise. That is, G* is constructed by adding an edge (i, j) into E* if and only if t*ij = 1. Look at Fig. 13.7 which shows the relation between k and t*ij.

Figure 13.7 Relation between k and T*ij

```
Transitive_Closure(A, t, n)
Step 1: SET i=1, j=1, k=1
Step 2: Repeat Steps 3 to 4 while i<=n
Step 3: Repeat Step 4 while j<=n
Step 4: IF (A[i][j]) = 1
        THEN t[i][j] = 1
        ELSE
        SET t[i][j] = 0
        INCREMENT j
        [END OF LOOP]
        INCREMENT i
        [END OF LOOP]
Step 5: Repeat Steps 6 to 11 while k<=n
Step 6: Repeat Steps 7 to 10 while i<=n
Step 7: Repeat Steps 8 to 9 while j<=n
Step 8: SET t[i][j] = t[i][j] V ( t[i][k] ^ t[k][j] )
Step 9: INCREMENT j
        [END OF LOOP]
Step 10: INCREMENT i
         [END OF LOOP]
Step 11: INCREMENT k
         [END OF LOOP]
Step 12: END
```

Figure 13.8 Algorithm to find the transitive enclosure of a graph G

# 13.4 BI-CONNECTED COMPONENTS

A vertex v of G is called an articulation point, if removing v along with the edges incident on v, results in a graph that has at least two connected components.

A bi-connected graph (shown in Fig. 13.10) is defined as a connected graph that has no articulation vertices. That is, a bi-connected graph is connected and non-separable in the sense that even if we remove any vertex from the graph, the resultant graph is still connected. By definition,

+   - A bi-connected undirected graph is a connected graph that cannot be broken into disconnected pieces by deleting any single vertex.
+   - In a bi-connected directed graph, for any two vertices v and w, there are two directed paths from v to w which have no vertices in common other than v and w.

![](bbox=[0.1, 0.76, 0.4, 0.9])

Figure 13.9 Non bi-connected graph

Note that the graph shown in Fig. 13.9(a) is not a bi-connected graph, as deleting vertex x from the graph results in two disconnected components of the original graph (Fig. 13.9(b)).