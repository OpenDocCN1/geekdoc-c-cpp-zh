The Path Matrix is

| 1 | 1 | 1 | 1 |
|---|---|---|---|
| 1 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 |

# 13.8.6 Modified Warshall's Algorithm

Warshall's algorithm can be modified to obtain a matrix that gives the shortest paths between the nodes in a graph G. As an input to the algorithm, we take the adjacency matrix A of G and replace all the values of A which are zero by infinity (∞). Infinity (∞) denotes a very large number and indicates that there is no path between the vertices. In Warshall's modified algorithm, we obtain a set of matrices Q0, Q1, Q2, ..., Qn using the formula given below.

Q_k[i][j] = Minimum { Q_{k-1}[i][j], Q_{k-1}[i][k] + Q_{k-1}[k][j] }

Qn is exactly the same as A with a little difference that every element having a zero value in A is replaced by (∞) in Qn. Using the given formula, the matrix Q will give the path matrix that has the shortest path between the vertices of the graph. Warshall's modified algorithm is shown in Fig. 13.40.

```
Step 1: [Initialize the Shortest Path Matrix, Q] Repeat Step 2 for I = 0 to n-1, where n is the number of nodes in the graph
Step 2: Repeat Step 3 for J = 0 to n-1
Step 3: IF A[I][J] = 0, then SET Q[I][J] = Infinity (or 9999) ELSE Q[I][J] = A[I][J] [END OF LOOP]
Step 4: [CALCULATE] Repeat Step 5 for K = 0 to n-1
Step 5: Repeat Step 6 for I = 0 to n-1
Step 6: Repeat Step 7 for J to n-1
Step 7: IF Q[I][J] <= Q[I][K] + Q[K][J] SET Q[I][J] = Q[I][J] ELSE SET Q[I][J] = Q[I][K] + Q[K][J] [END OF IF] [END OF LOOP] [END OF LOOP] [END OF LOOP]
Step 8: EXIT
```

Figure 13.40 Modified Warshall's algorithm

Example 13.12 Consider the unweighted graph G given in Fig. 13.41 and apply Warshall's algorithm to it.

![](bbox=[0.1, 0.75, 0.2, 0.81])

Q0 =
| 9999 | 1 | 1 | 9999 |
|---|---|---|---|
| 9999 | 9999 | 9999 | 1 |
| 9999 | 1 | 9999 | 9999 |
| 1 | 9999 | 1 | 9999 |

Q1 =
| 9999 | 1 | 1 | 9999 |
|---|---|---|---|
| 9999 | 9999 | 9999 | 1 |
| 9999 | 1 | 9999 | 9999 |
| 1 | 9999 | 1 | 9999 |

Q1 =
| 9999 | 1 | 1 | 9999 |
|---|---|---|---|
| 9999 | 9999 | 9999 | 1 |
| 9999 | 1 | 9999 | 9999 |
| 1 | 2 | 1 | 9999 |

Q2 =
| 9999 | 1 | 1 | 2 |
|---|---|---|---|
| 9999 | 9999 | 9999 | 1 |
| 9999 | 1 | 9999 | 2 |
| 1 | 2 | 9999 | 3 |

Q3 =
| 9999 | 1 | 1 | 2 |
|---|---|---|---|
| 9999 | 9999 | 9999 | 1 |
| 9999 | 1 | 9999 | 2 |
| 1 | 2 | 9999 | 3 |

Q4 = Q
| 3 | 1 | 1 | 2 |
|---|---|---|---|
| 2 | 3 | 2 | 1 |
| 3 | 1 | 3 | 2 |
| 1 | 2 | 1 | 3 |

Figure 13.41 Graph G