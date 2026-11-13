From the above examples, we can draw the following conclusions:

+   - For a simple graph (that has no loops), the adjacency matrix has 0s on the diagonal.
+   - The adjacency matrix of an undirected graph is symmetric.
+   - The memory use of an adjacency matrix is $O(n^2)$, where n is the number of nodes in the graph.
+   - Number of 1s (or non-zero entries) in an adjacency matrix is equal to the number of edges in the graph.
+   - The adjacency matrix for a weighted graph contains the weights of the edges connecting the nodes.

Now let us discuss the powers of an adjacency matrix. From adjacency matrix $A^1$, we can conclude that an entry 1 in the $i$th row and $j$th column means that there exists a path of length 1 from $v_i$ to $v_j$. Now, consider, $A^2, A^3,$ and $A^4$.

```
$(a_{ij})^r = \Sigma_{ik} a_{ik}$
```

Any entry $a_{ij} = 1$ if $a_{ij} = a_{1j} = 1$. That is, if there is an edge $(v_i, v_j)$ and $(v_j, v_k)$, then there is a path from $v_i$ to $v_k$ of length 2.

![](bbox=[0.1, 0.38, 0.35, 0.47])

Similarly, every entry in the $i$th row and $j$th column of $A^3$ gives the number of paths of length 3 from node $v_i$ to $v_j$.

In general terms, we can conclude that every entry in the $i$th row and $j$th column of $A^r$ (where n is the number of nodes in the graph) gives the number of paths of length n from node $v_i$ to $v_j$. Consider a directed graph given in Fig. 13.15. Given its adjacency matrix A, let us calculate $A^2, A^3,$ and $A^4$.

```
$A^2 = A^1 \times A^1$$
$$
\begin{bmatrix}
0 & 1 & 1 & 0 \\
0 & 0 & 1 & 1 \\
0 & 0 & 0 & 1 \\
1 & 1 & 0 & 0
\end{bmatrix}
\times
\begin{bmatrix}
0 & 1 & 1 & 0 \\
0 & 0 & 1 & 1 \\
0 & 0 & 0 & 1 \\
1 & 1 & 0 & 0
\end{bmatrix}
=
\begin{bmatrix}
0 & 0 & 1 & 2 \\
1 & 1 & 0 & 1 \\
1 & 1 & 0 & 0 \\
1 & 1 & 2 & 1
\end{bmatrix}$$
```

```
$A^3 = $$
$$
\begin{bmatrix}
0 & 1 & 1 & 2 \\
1 & 1 & 0 & 1 \\
1 & 1 & 0 & 0 \\
1 & 1 & 2 & 1
\end{bmatrix}
\times
\begin{bmatrix}
0 & 1 & 1 & 0 \\
0 & 0 & 1 & 1 \\
0 & 0 & 0 & 1 \\
1 & 1 & 0 & 0
\end{bmatrix}
=
\begin{bmatrix}
2 & 2 & 0 & 1 \\
1 & 2 & 2 & 1 \\
0 & 1 & 1 & 1 \\
1 & 2 & 2 & 3
\end{bmatrix}$$
```

```
$A^4 = $$
$$
\begin{bmatrix}
2 & 2 & 0 & 1 \\
1 & 2 & 2 & 1 \\
0 & 1 & 1 & 1 \\
1 & 2 & 2 & 3
\end{bmatrix}
\times
\begin{bmatrix}
0 & 1 & 1 & 0 \\
0 & 0 & 1 & 1 \\
0 & 0 & 0 & 1 \\
1 & 1 & 0 & 0
\end{bmatrix}
=
\begin{bmatrix}
1 & 3 & 4 & 2 \\
1 & 2 & 3 & 4 \\
1 & 1 & 1 & 3 \\
3 & 4 & 3 & 4
\end{bmatrix}$$
```

Now, based on the above calculations, we define matrix B as:

```
$B^r = A^1 + A^2 + ... + A^r$
```

An entry in the $i$th row and $j$th column of matrix B gives the number of paths of length r or less than r from vertex $v_i$ to $v_j$. The main goal to define matrix B is to obtain the path matrix P. The path matrix P can be calculated from B by setting an entry $p_{ij} = 1$, if $b_{ij}$ is non-zero and $p_{ij} = 0$,