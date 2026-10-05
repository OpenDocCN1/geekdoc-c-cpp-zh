# Chapter 2. C/C++: Libraries and Makefiles

2 \times 2 example:

$$\begin{pmatrix} 0 & 1 \ 1 & 0 \end{pmatrix} egin{pmatrix} 5 & -3 \ 10 & 1 \end{pmatrix} = \begin{pmatrix} 10 & 1 \ 0 & -3 \end{pmatrix}$

The left-most matrix flips the rows to ensure that the subdiagonal entries of the lower triangular factor are at most 1 in magnitude. Each row pivoting promotes numerical stability.

DGETRF carries out triangular factorization in place, and when the function returns, the lower and upper triangular factors will be stored using the same array. The unit diagonal of the lower triangular matrix is not stored. The row that ends as the ith row after pivoting is *ipiv[i] (ipiv must be allocated as an integer array of length m before the function is called). The last parameter *info returns information about possible errors: if *info=0, the execution was successful; if *info=-i, the argument had an invalid value; if *info=i with $i=1, \dots, m$, the input matrix is singular and the $(i-1, i)$ entry of the upper triangular factor is zero.

After triangular factorization, matrix systems are solved using DGETRES. Here is the code for triangular solve. In MKL, there are four possible names for the same function as declarations in mkl_lapack.h. One of these is dgetrs():

```
void dgetrs_( char *trans, MKL_INT *n,
MKL_INT *nrhs, double *a,
MKL_INT *lda, MKL_INT *ipiv,
double *b, MKL_INT *ldb,
MKL_INT *info );
```
```

Before this function is called, the matrix stored in the array must have undergone triangular factorization. The first argument to this function is a character string named trans. This string allows us to ask for the solution of the transposed system. The system is not transposed if trans='N' but is transposed if trans='T'. When the Fortran function is called from C, we must ordinarily pass the length of the string explicitly as the last argument. However, MKL takes advantage of the way strings are handled by LAPACK's Fortran routines and do not require us to pass that last argument.

Once A has been factored $PA=LU$, where $P$ is the pivoting matrix and $L$ and $U$ are lower and upper triangular factors, respectively, the solution of $Ax=b$ is