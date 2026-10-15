The routine’s input consists of the coefficient matrix a, the vector of constant terms b, the vector x holding the initial approximation of the solution, the order n of the system, and the initialization option init. If init is set to 0, the routine refines the initial approximation received via x, or else, the solution is initialized with the constant terms of the reduced system. On exit from the routine, x returns the refined solution, while err represents the maximum relative error of its components.

The convergence of the algorithm is ensured, as explained above, by multiplying both sides of the original system with the transpose of the coefficient matrix. Array s is thus used at first to store the matrix Aᵀ·A of the normal system and, then, the matrix S of the reduced system. Analogously, array t contains at first the vector of constant terms Aᵀ·b of the normal system and, then, the vector t of the reduced system.

Except for the additional requirement of specifying an initial approximation for the solution, the usage of the routine GaussSeidel is similar to the one of direct methods.

# 7.11 Implementations in C/C++

Listing 7.20 shows the content of the file linsys.h, which contains equivalent C/C++ implementations of the Python functions developed in the main text and included in the module linsys.py. The corresponding routines have identical names and functionalities.

Listing 7.20 Solvers for Systems of Linear Equations (linsys.h)

```
//------------------------------------------- linsys.h -------------------------------------------
// Contains routines for solving systems of linear equations.
// Part of the numxlib numerics library. Author: Titus Beu, 2013
//-----------------------------------------------------------------------------------------------
#ifndef _LINSYS_
#define _LINSYS_

#include <stdio.h>
#include <math.h>
#include "memalloc.h"

//================================================================================================
void Gauss(double **a, double **b, int n, int m, double &det)
//-----------------------------------------------------------------------------------------------
// Solves matrix equation a x = b by Gaussian elimination with partial
// pivoting on columns.
// a   - coefficient matrix (n x n); destroyed on exit
// b   - matrix of constant terms (n x m); solution x on exit
// det - determinant of coefficient matrix (output).
//-----------------------------------------------------------------------------------------------
{
#define Swap(a,b) { t = a; a = b; b = t; }
    double amax, sum, t;
    int i, imax, j, k;

    det = 1e0;
    for (k=1; k<=n; k++) {                      // FORWARD ELIMINATION
        amax = 0e0;                             // determine pivot row with
        for (i=k; i<=n; i++)                    // max. element on column k
            if (amax < fabs(a[i][k])) { amax = fabs(a[i][k]); imax = i; }
        if (amax == 0e0)
            { printf("Gauss: singular matrix !\n"); det = 0e0; return; }

        if (imax != k) {                        // interchange rows imax and k
```