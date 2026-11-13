+   3. a(f - h)
+   4. d(g - e)
+   5. (a + b)h
+   6. (c - a)(e + f)
+   7. (b - d)(g + h)

Certain versions of the programming language BASIC have matrix operations built into the language. Specifically, the following are valid BASIC statements where A and B are two-dimensional arrays that have appropriate dimensions and K is a scalar:

```
MAT C = A + B
MAT D = (K)*A
MAT E = A*B
```

Each statement begins with the keyword MAT, which indicates that matrix operations will be performed. Thus C will be the matrix sum of A and B, D will be the scalar product of the matrix A by the scalar K, and E will be the matrix product of A and B.

# 4.17 SPARSE MATRICES

Matrices with a relatively high proportion of zero entries are called sparse matrices. Two general types of n-square sparse matrices, which occur in various applications, are pictured in Fig. 4.26. (It is sometimes customary to omit blocks of zeros in a matrix as in Fig. 4.26.) The first matrix, where all entries above the main diagonal are zero or, equivalently, where nonzero entries can only occur on or below the main diagonal, is called a (lower) triangular matrix. The second matrix, where nonzero entries can only occur on the diagonal or on elements immediately above or below the diagonal, is called a tridiagonal matrix.

![](bbox=[0.15, 0.61, 0.88, 0.79])

The natural method of representing matrices in memory as two-dimensional arrays may not be suitable for sparse matrices. That is, one may save space by storing only those entries which may be nonzero. This is illustrated for triangular matrices in the following example. Other cases will be discussed in the solved problems.