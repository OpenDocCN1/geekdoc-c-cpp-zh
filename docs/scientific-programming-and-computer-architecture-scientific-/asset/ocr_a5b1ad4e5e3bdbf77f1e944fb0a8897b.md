# 2.2. Using BLAS and LAPACK libraries

| S | single precision | GE | general | TRF | triangular factorization |
|---|---|---|---|---|---|
| D | double precision | GT | general triangular | TRS | triangular solve |
| C | complex single precision | PB | positive banded | LSS | least squares solver |
| Z | complex double precision | SP | symmetric packed storage | SVD | singular values |
| | | TB | triangular banded | EV | eigenvalues |

Table 2.1: Convention for naming functions in BLAS and LAPACK. Function names are formed by adjoining codes in columns 1, 3, and 5. For instance, DGETRF() implements triangular factorization of general matrices with double-precision entries. Columns 3 and 5 list only a small subset of the possible codes.

```
void DGETRF ( MKL_INT *m, MKL_INT *n, double *a, MKL_INT \
*lda, MKL_INT *ipiv, MKL_INT *info );
void DGETRF_( MKL_INT *m, MKL_INT *n, double *a, \
MKL_INT *lda, MKL_INT *ipiv, MKL_INT *info );
void dgetrf ( MKL_INT *m, MKL_INT *n, double *a, \
MKL_INT *lda, MKL_INT *ipiv, MKL_INT *info );
dgetrf_ ( MKL_INT *m, MKL_INT *n, double *a, \
MKL_INT *lda, MKL_INT *ipiv, MKL_INT *info );
```

These names are all bound to the same function in the object code of the library. So we may call the function by any of the four names. MKL_INT is used as a synonym for int to facilitate porting the library to systems with different conventions for int and long int. The parameters m and n of dgetrf_ are the number of rows and columns of the matrix whose (i,j) entry is a[i+j*lda].

Triangular factorizations are useful for solving matrix systems. The following is a