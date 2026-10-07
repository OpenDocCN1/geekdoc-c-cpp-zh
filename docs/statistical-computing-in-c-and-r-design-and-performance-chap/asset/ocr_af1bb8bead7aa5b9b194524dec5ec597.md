# NUMERICAL LINEAR ALGEBRA

270

for

```
$D^T = \begin{bmatrix} \text{diag}(1/\lambda_1, \dots, 1/\lambda_r) & O_r \times (n-r) \ 0_{(p-r) \times r} & 0_{(p-r) \times (n-r)} \end{bmatrix} \quad (7.38)$
```

The proof (Exercise 7.23) consists of showing that the Penrose equations are satisfied with this choice for $X^T$. The implication of $(7.37)-(7.38)$ is that $b$ in $(7.35)$ has the form

```
$b = VD^T U^T y = \sum_{j=1}^r \lambda_j^{-1} a_j v_j$
```

with $a_j = u_j^T y, j=1, \dots, r$. As result, $b$ can be evaluated using the SVD for $X$ is available. To give an example of how the SVD is used in a least-squares method, consider finding the least-squares solution $Xb=y$ with $X$ given by

| | [1] | [2] | [3] |
|---|---|---||
| [1] | 1 | 1 | 0 |
| [2] | 1 | 1 | 0 |
| [3] | 1 | 1 | 0 |
| [4] | 0 | 1 | 1 |
| [5] | 0 | 0 | 1 |
| [6] | 1 | 0 | 1 |

and the response $y$ created in R

+   - set.seed(123)
- y <- rnorm(6)

This choice for the $X$ matrix corresponds to a two-sample mean comparison problem over the model for treatment effects $	au_i$ and random errors the formulation $X$ has rank two with which $X^TX$ is singular. An application of (7.35) and (7.24) in conjunction with the SVD method for class Matrix (with parameters itMax and delta at 35 and $10^{-8}$, respectively) produces

| 0.11111 | 0.11111 | 0.11111 | 0.111112 | 0.111112 | 0.111112 |
| 0.22222 | 0.22222 | 0.22222 | -0.111112 | -0.111112 | -0.111112 |
| -0.11111 | -0.11111 | -0.11111 | 0.222224 | 0.222224 | 0.222224 |

Moore-Penrose inverse of A
Least square solution
0.298133
0.0420867
0.34019

One may check these calculations with R using the ginv function from the MASS package that computes the Moore-Penrose inverse of a matrix as its argument (Example 7.26). Assume that $X$ has rank $p$. In this instance another of computing a leastsquares solution of $Xb=c$ through a QR decomposition of $X$ obtained via Gram-Schmidt orthogonalization. The first idea is to factorize $X$ as

```
$X = QR \quad (7.39)$
```

with $Q = [q_1, \dots, q_p]$ an $n \times p$ orthogonal matrix and $R$ a $p \times p$ nonsingular, upper-triangular matrix. To create the $Q$ columns of $X$ can be orthonormalized using the procedure now