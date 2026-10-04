You can show that matrix multiplication is noncommutative using the same two matrices. Switching the order of multiplication gives you an entirely different result.

```
R> B%%***
[,1] [2] [3]
[1,] -12 12 -6
[2,] 4 -4 2
[3,] 32 10 22
```

# 3.3.6 Matrix Inversion

Some square matrices can be inverted. The inverse of a matrix A is denoted A⁻¹. An invertible matrix satisfies the following equation:

```
AA^{-1} = I_m
```

Here's an example of a matrix and its inverse:

| 3 1 | 1 -0.5 |
| 4 2 | -2 1.5 |

Matrices that are not invertible are referred to as singular. Inverting a matrix is often necessary when solving equations with matrices has important practical ramifications. There are several different approaches to matrix inversion, and these calculations can become extremely expensive as you increase the size of a matrix. We won't go into too much detail here, but if you're interested, see Golub and Van Loan (1989) for formal discussions.

For now, I'll show you the R function solve as one option for inverting a matrix.

```
R> matrix(data=c(3,4,1,2),nrow=2,ncol=2)
R> A
[,1] [,2]
[1,] 3 1
[2,] 4 2
R> solve(A)
[,1] [,2]
[1,] 1 -0.5
[2,] -2 1.5
```

You can also verify that the product of these two matrices (using matrix multiplication rules) results in the 2×2 identity matrix.