
5. Recompose the eigenvectors x = (L⁻¹)ᵀ · x̃ of the initial eigenvalue problem (8.30) based on

x_ij = Σ_{k=i}^n l'_ki x̃_kj.    (8.37)

In the implementation of the above algorithm given in Listing 8.4, the Cholesky factorization of matrix B is carried out by calling the function Cholesky, while the inversion of the yielded lower triangular matrix L is performed by the routine MatTriInv (both routines are developed in Chapter 7 and included in the module linsys.py). The actual solution of the resulting standard eigenvalue problem (8.34) is performed by calling the function Jacobi, described in Section 8.3.

## Listing 8.4 Solver for Generalized Eigenvalue Problems for Symmetric Matrices (Python Coding)

```
#===============================================================================
def EigSym(a, b, x, d, n):
#-------------------------------------------------------------------------------
# Solves the generalized eigenvalue problem a x = lambda b x for the real
# symmetric matrix a and the real positive-definite symmetric matrix b,
# reducing it to standard form at xt = lambda xt by Cholesky factorization
# of matrix b = L * LT.
# a - real symmetric matrix
# b - real positive-definite symmetric matrix (L replaces lower triangle)
# x - modal matrix: eigenvectors on columns (output)
# d - vector of eigenvalues
# n - order of matrix a
# Error flag: 0 - normal execution
#             1 - matrix b not positive-definite
# Calls: Cholesky, MatTriInv, Jacobi.
#-------------------------------------------------------------------------------
    (det,i err) = Cholesky(b,n)                 # Cholesky factorization b = L * LT
    if (i err):
        print("EigSym: matrix b is not positive-definite!"); return 1

    MatTriInv(b,n)                              # b = L^(-1)

    for i in range(1,n):
        for j in range(i+1,n+1): a[i][j] = a[j][i]      # fill upper triangle of a

    at = [[0]*(n+1) for i in range(n+1)]
    xt = [[0]*(n+1) for i in range(n+1)]

    for i in range(1,n+1):      # transformed matrix at = L^(-1) * a * LT^(-1)
        for j in range(1,i+1):
            sum = 0e0
            for k in range(1,i+1):
                for m in range(1,j+1): sum += b[i][k] * a[k][m] * b[j][m]
            at[i][j] = sum

    Jacobi(at,xt,d,n)           # solve transformed problem at xt = lambda xt

    for j in range(1,n+1):                      # recompose eigenvectors of
        for i in range(1,n+1):                  # initial eigenvalue problem
            sum = 0e0
            for k in range(i,n+1): sum += b[k][i] * xt[k][j]
            x[i][j] = sum

    return 0
```

The elements of matrices A and B are passed to the routine EigSym by the lower triangles of the arrays a and b. The lower triangle of b is then used to store successively the elements of the factorization matrix L and those of the inverse L⁻¹. The allocated arrays at and xt correspond, respectively, to the matrices Ã and x̃. On exit from the routine, the array d contains the calculated eigenvalues, while the array x returns on its columns the corresponding eigenvectors.

## 8.5 Implementations in C/C++

Listing 8.5 shows the content of the file eigsys.h, which contains equivalent C/C++ implementations of the Python functions developed in the main text and included in the module eigsys.py. The corresponding routines have identical names, parameters, and functionalities.

## Listing 8.5 Solvers for Eigenvalue Problems (eigsys.h)

```
//------------------------------------------------------------- eigsys.h -------------------------------------------------------------
// Contains routines for solving eigenvalue problems.
// Part of the numxlib numerics library. Author: Titus Beu, 2013
//-------------------------------------------------------------
#ifndef _EIGSYS_
#define _EIGSYS_

#include <stdio.h>
#include <math.h>
#include "memalloc.h"
#include "linsys.h"

//==================================================================================================================================
int Jacobi(double **a, double **x, double d[], int n)
//-------------------------------------------------------------
// Solves the eigenvalue problem of a real symmetric matrix using the
// Jacobi method
// a  - real symmetric matrix (lower triangle is destroyed)
// x  - modal matrix: eigenvectors on columns (output)
// d  - vector of eigenvalues
// n  - order of matrix a
// Error flag: 0 - normal execution, 1 - exceeded max. no. of iterations
//-------------------------------------------------------------
{
    const double eps = 1e-30;                     // precision criterion
    const int itmax = 50;                         // max no. of iterations
    double aii, aij, ajj, amax, c, s, t;
    int i, it, j, k;

    for (i=1; i<=n; i++) {                         // initialization
        for (j=1; j<=n; j++) x[i][j] = 0e0;        // modal matrix = unit matrix
        x[i][i] = 1e0;
        d[i] = a[i][i];                           // eigenvalues = diagonal elements
    }

    for (it=1; it<=itmax; it++) {                  // loop of iterations
        amax = 0e0;
        for (i=2; i<=n; i++)                       // lower triangle: i > j
            for (j=1; j<=(i-1); j++) {
                aii = d[i]; ajj = d[j];            // diagonal elements
                aij = fabs(a[i][j]);
                if (aij > amax) amax = aij;                     // max. non-diagonal element
                if (aij > eps) {                                 // perform rotation
                    c = 0.5e0*(aii-ajj)/a[i][j];
                    t = 1e0/(fabs(c) + sqrt(1e0+c*c));            // tangent
                    if (c < 0e0) t = -t;                          // sign
                    c = 1e0/sqrt(1e0+t*t); s = c*t;               // cos, sin
                    for (k=1; k<=(j-1); k++) {                    // columns k < j
                        t       = a[j][k]*c - a[i][k]*s;
                        a[i][k] = a[i][k]*c + a[j][k]*s;
                        a[j][k] = t;
                    }
                    for (k=(j+1); k<=(i-1); k++) {                // columns k > j
                        t       = a[k][j]*c - a[i][k]*s;          // interchange j <> k
                        a[i][k] = a[i][k]*c + a[k][j]*s;
                        a[k][j] = t;
                    }
                    for (k=(i+1); k<=n; k++) {                    // columns k > i
                        t       = a[k][j]*c - a[k][i]*s;          // interchange i <> k
                        a[k][i] = a[k][i]*c + a[k][j]*s;          // interchange j <> k
                        a[k][j] = t;
                    }
                    for (k=1; k<=n; k++) {                        // transform modal matrix
                        t       = x[k][j]*c - x[k][i]*s;
                        x[k][i] = x[k][i]*c + x[k][j]*s;
                        x[k][j] = t;
                    }
                    t = 2e0 * s * c * a[i][j];
                    d[i] = aii*c*c + ajj*s*s + t;                 // update eigenvalues
                    d[j] = ajj*c*c + aii*s*s - t;
                    a[i][j] = 0e0;
                }
            }
        if (amax<=eps) break;                             // check convergence
    }

    if (it > itmax) {
        printf("Jacobi: max. no. of iterations exceeded !\n"); return 1;
    }
    return 0;
}

//==============================================================================
int EigSym(double **a, double **b, double **x, double d[], int n)
//------------------------------------------------------------------------------
// Solves the generalized eigenvalue problem a x = lambda b x for the real
// symmetric matrix a and the real positive-definite symmetric matrix b,
// reducing it to standard form at xt = lambda xt by Cholesky factorization
// of matrix b = L * LT.
// a  - real symmetric matrix
// b  - real positive-definite symmetric matrix (L replaces lower triangle)
// x  - modal matrix: eigenvectors on columns (output)
// d  - vector of eigenvalues
// n  - order of matrix a
// Error flag: 0 - normal execution
//             1 - matrix b not positive-definite
// Calls: Cholesky, MatTriInv, Jacobi.
//------------------------------------------------------------------------------
{
    double **at, **xt, det, sum;
    int i, j, k, m;

    if (Cholesky(b,n,det))                      // Cholesky factorization b = L * LT
      { printf("EigSym: matrix b is not positive-definite !\n"); return 1; }

    MatTriInv(b,n);                             // b = L^(-1)

    for (i=1; i<=(n-1); i++)                    // fill upper triangle of a
      for (j=i+1; j<=n; j++) a[i][j] = a[j][i];

    at = Matrix(1,n,1,n);
    xt = Matrix(1,n,1,n);

    for (i=1; i<=n; i++)        // transformed matrix at = L^(-1) * a * LT^(-1)
      for (j=1; j<=i; j++) {
        sum = 0e0;
        for (k=1; k<=i; k++)
          for (m=1; m<=j; m++) sum += b[i][k] * a[k][m] * b[j][m];
        at[i][j] = sum;
      }

    Jacobi(at,xt,d,n);          // solve transformed problem at xt = lambda xt

    for (j=1; j<=n; j++)                        // recompose eigenvectors of
      for (i=1; i<=n; i++) {                    // initial eigenvalue problem
        sum = 0e0;
        for (k=i; k<=n; k++) sum += b[k][i] * xt[k][j];
        x[i][j] = sum;
      }

    FreeMatrix(at,1,1);
    FreeMatrix(xt,1,1);
    return 0;
}
//==============================================================================
void EigSort(double **x, double d[], int n, int isort)
//------------------------------------------------------------------------------
// Sorts the eigenvalues d and eigenvectors x according to the eigenvalues
// x  - eigenvectors on columns
// d  - vector of eigenvalues
// n  - dimension of eigenvalue problem
// isort = 0: no sorting; > 0: ascending sorting; < 0: descending sorting
//------------------------------------------------------------------------------
{
  double dmax, t;
  int i, j, jmax;

  if (isort == 0) return;

  for (j=1; j<=n-1; j++) {
    jmax = j; dmax = d[j];                  // find column of maximum eigenvalue
    for (i=j+1; i<=n; i++) {
      if (isort * (dmax - d[i]) > 0e0) {
        jmax = i; dmax = d[i];
      }
    }
    if (jmax != j) {
      d[jmax] = d[j]; d[j] = dmax;  // swap current component with maximum
