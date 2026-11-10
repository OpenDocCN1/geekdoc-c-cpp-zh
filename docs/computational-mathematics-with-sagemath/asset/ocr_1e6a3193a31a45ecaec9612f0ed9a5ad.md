```
```sage
sage: A = matrix(RDF, [[1,3,2],[1,4,2],[0,5,2],[1,3,2]])
sage: b = vector(RDF, [1,2,3,4])
sage: Z = transpose(A)*A
sage: C = Z.cholesky()
sage: R = transpose(A)*b
sage: Z.solve_right(R)
(-1.5000000000000135, -0.5000000000000085, 2.7500000000000213)
```
```

We should note that Cholesky's decomposition is cached, and is used by `Z.solve_right(R)`, without being recomputed.

**With the QR decomposition.** Assume $A$ of full rank$^7$; we consider the $QR$ decomposition of $A$. Then

$$\|Ax-b\|_2^2 = \|QRx-b\|_2^2 = \|Rx-Q^T b\|_2^2.$$

We have: $R = \begin{bmatrix} R_1 \\ 0 \end{bmatrix}$ where $R_1$ is $m \times m$ upper triangular and $Q^T b = \begin{bmatrix} c \\ d \end{bmatrix}$ with $c$ of size $m$. Thus $\|Ax-b\|_2^2 = \|R_1 x - c\|_2^2 + \|d\|_2^2$, and the minimum is obtained by solving the triangular system $R_1 x = c$:

```
```sage
sage: A = matrix(RDF, [[1,3,2],[1,4,2],[0,5,2],[1,3,2]])
sage: b = vector(RDF, [1,2,3,4])
sage: Q, R = A.QR()
sage: R1 = R[0:3,0:3]
sage: b1 = transpose(Q)*b
sage: c = b1[0:3]
sage: R1.solve_right(c)
(-1.499999999999999, -0.4999999999999867, 2.749999999999997)
```
```

Let us compute the condition number of $A^T A$ in infinite norm:

```
```sage
sage: Z = A.transpose()*A
sage: Z.norm(Infinity)*Z^(-1).norm(Infinity)
1992.375000000168
```
```

The $QR$ method and the method of normal equations give results that agree to within the roundoff level times $\kappa(A^T A)$.

**With the Singular Value Decomposition.** The singular value decomposition $A = U\Sigma V^T$ also allows us to compute the solution; moreover, we can use it when $A$ is not of full rank. If $A$ is not the zero matrix, $\Sigma$ has $0 < r \le m$ positive coefficients $\sigma_i$ (assumed in decreasing order). We then have:

$$\|Ax-b\|_2^2 = \|U^T A V V^T x - U^T b\|_2^2.$$

Writing $\lambda = V^T x$, and $u_i$ for the columns of $U$, we have:

$$\|Ax-b\|_2^2 = \sum_{i=1}^{r} (\sigma_i \lambda_i - u_i^T b)^2 + \sum_{i=r+1}^{m} (u_i^T b)^2.$$