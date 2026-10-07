# LEAST SQUARES

$x_1, \dots, x_p$ are linearly independent, $n$-vector columns of $X$. The Gram-Schmidt algorithm creates an orthonormal basis $q_1, \dots, q_p$ for the linear manifold spanned by $x_1, \dots, x_p$.

```
Algorithm 7.5 Gram-Schmidt algorithm
$q_1 = x_1/|x_1|$
for $i = 2, \dots, p$
  $q_i = x_i - \sum_{j=1}^{i-1} (q_j^T x_i) q_j$
  $q_i := q_i/|q_i|$
end
```

A proof that $q_1, \dots, q_p$ are orthonormal and provide a basis for the linear span of $x_1, \dots, x_p$ can be obtained by induction (Exercise 7.31). This algorithm can exhibit numerical instability, but it is easily modified to resolve such problems (Exercise 7.32).
Since the vectors $q_1, \dots, q_p$ returned from the Gram-Schmidt algorithm an orthonormal basis for the columns of $X$ it must be that $X = QR$ with $R$ $p \times p$ matrix with elements $r_{ij} = q_i^T x_j$ the coefficients of $x_j$ in its representation over the $q_1, \dots, q_p$. The order in which the $q_i$ have been constructed guarantees that $R$ is upper-triangular. As a result, the existence has been established of a factorization of the form (7.39). In addition,

> $X^T X = R^T Q^T Q R = R^T R$.

But $R$ is upper-triangular and the Cholesky factorization is unique. Therefore it must be that $R^T$ is the lower-triangular Cholesky factor for the matrix $X^T X$.
Using our $Q$ decomposition the least-squares normal equations $X^T X b = X^T y$.

> $R^T Rb = R^T Q^T y$.

The fact that $R$ is nonsingular has the consequence that this identity is the same as

> $Rb = Q^T y$ (7.40)

which can be solved directly using back substitution.
The modified Gram-Schmidt method from Exercise 7.32 was implemented in C++ (see Appendix D) and then used to solve the least-squares problems in the previous section with the right-hand side vector that was used for our Gaussian elimination in Section 7.2.2. This produced

| The Q matrix | | | |
|---|---|---|--|
| -0.3338547 | 0.7874465 | 0.2822091 | 0.4340472 |
| -0.1371083 | 0.1474621 | 0.2109068 | -0.4703518 |
| 0.9284652 | 0.3428817 | 0.1241733 | 0.0146689 |
| 0.04199925 | -0.4395243 | 0.8533937 | 0.2759971 |
| 0.0707115 | -0.2178078 | -0.363561 | 0.7169494 |
| The R matrix | | | |
| 1.678801 | -1.8735212 | -0.1204544 | -2.4977218 |
| 0 | 1.3883693 | 1.226791 | 0.6009228 |
| 0 | 0 | 0.7663734 | 1.135503 |
| 0 | 0 | 0 | 0.367215 |

| The product QR | | | |
| -0.5604756 | 1.7715065 | 1.2220482 | 1.7869113 |
| -0.2301775 | 0.4860162 | 0.3598138 | 0.4978505 |
| 1.558708 | -1.265061 | 0.4007715 | -1.966617 |
| 0.07050839 | -0.6868529 | 0.1106827 | 0.7013559 |
| 0.1292873 | -0.4456621 | -0.5558411 | -0.4727914 |

![](bbox=[0.104, 0.956, 0.895, 0.973])