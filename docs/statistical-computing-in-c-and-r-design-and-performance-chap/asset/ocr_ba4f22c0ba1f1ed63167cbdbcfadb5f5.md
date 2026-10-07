# SOLVING LINEAR EQUATIONS

and then loaded with

+   > library (SparseM)

The slots for objects of class.csr can be determined by the getClass function.
The result is

+   > getClass("matrix.csr")
Class "matrix.csr" [package "SparseM"]

Slots:

Name: ra ja ia dimension
Class: numeric integer integer integer

The ra is a one-dimensional array that has the nonzero elements of the matrix and
dimension is a two-dimensional array that gives the number of rows and columns of the
matrix as its first and second component, respectively. The ja and ia slots specify
the elements of ra are located in matrix. First, ja is the column location of the corresponding entry
same length as ra with entries that give the column location of an array length equal to the number of rows
 1. The nonzero elements of ia are the elements in ra where new rows
should be started. The last entry is a new row if one were to be appended
to the array; i.e. it is the number of nonzero plus 1.

To illustrate the use of the Sparse package we first created a positive-definite two-banded
matrix with

```
> set.seed(123)
> A <- rnorm(36, 0, 6)
> check <- function(i, j) {
  if (abs(i - j) == 0
  else A[i, j] = A[i, j]
}
> v <- Vectorize(check)
> t(A) <- outer(1, 6, v(A))
```

| [1] | [2] | [3] | [4] | [5] | [6] |
| [1] | 0.3671463 | 0.0328561 | -0.0254767 | 0.0000000 | 0.0000000 | 0.0000000 |
| [2] | 0.0328561 | 2.2845952 | 0.2417066 | 0.7334377 | 0.0000000 | 0.0000000 |
| [3] | -0.0254767 | 0.2417066 | 3.5142658 | 0.2040381 | 0.2740644 | 0.0000000 |
| [4] | 0.0000000 | 0.2040381 | 2.2404456 | 1.1340201 | 2.8909306 | -0.8249454 |
| [5] | 0.0000000 | 0.0000000 | 1.1340201 | -0.0161435 | -0.0161435 | 1.4922087 |
| [6] | 0.0000000 | 0.0000000 | 0.0000000 | 0.0000000 | 0.0000000 | |

A 6×6 matrix is first created using random numbers from the standard normal distribution.
To convert it to a banded matrix the Vectorize function from Section 5.5 has been used
to vectorize a function that replaces elements outside a unit band length with 0
ent. This vectorized function is used with outer to carry out the restructuring.
A positive-definite two-banded matrix is then produced from the product of the transpose
of the banded matrix with slots. The as.matrix csr function can now be used to convert
t matrix A that we created into an object of class matrix.csr: i.e.,

+   > as.matrix.csr(A)

The slots of A.csr are

+   > A.csrra

| [1] | 0.3671463 | 0.0328561 | -0.0254767 | 0.0328561 | 2.2845952 | 0.2417066 |
| [7] | 0.7334376 | -0.0254767 | 0.2417066 | 3.5142658 | 0.2040381 | 0.2740644 |
| [13] | 0.7334376 | 0.2040381 | 2.2404456 | 1.1340201 | -0.8249454 | 0.2740644 |
| [19] | 1.1340201 | 2.8909306 | -0.0161435 | -0.8249454 | -0.0161435 | 1.4922087 |