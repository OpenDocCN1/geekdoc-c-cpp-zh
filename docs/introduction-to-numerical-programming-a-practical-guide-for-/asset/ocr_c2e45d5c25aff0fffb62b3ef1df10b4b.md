```
```c
for (i=1; i<=n; i++)                         // random matrix
    for (j=1; j<=n; j++) a[i][j] = a0[i][j] = rand();
printf("A:\n");
MatPrint(a,n,n);

LUFactor(a,ipivot,n,det);                     // LU decomposition of a
printf("LU decomposition:\n");
MatPrint(a,n,n);

for (k=1; k<=n; k++) {                         // loop over constant vectors
    for (i=1; i<=n; i++) b[i] = x[i] = rand();       // random constant terms
    printf("b:\n");
    VecPrint(b,n);

    LUSystem(a,ipivot,x,n);                    // solve linear system

    err = 0e0;                                 // check max (Ax-b) = 0
    for (i=1; i<=n; i++) {
        erri = -b[i];
        for (j=1; j<=n; j++) erri += a0[i][j] * x[j]; // element i of (Ax-b)
        err = max(err,fabs(erri));
    }
    printf("   max (Ax-b) = % .1e\n",err);
}
```
```

# PROBLEM 7.3

Write Python and C/C++ programs employing routine `TriDiagSys` for solving a tridiagonal linear system (see Equation 7.78) of order $n = 100$ with the matrix elements generated randomly. Check the solution synthetically, by verifying the vanishing of the maximum residual error $\Delta = \max_i |a_i x_{i-1} + b_i x_i + c_i x_{i+1} - d_i|$.

# Solution

The Python implementation is given in Listing 7.25 and the C/C++ version is available as supplementary material (`P07-TriDiagSys1.cpp`).

```
Listing 7.25   Solution of System with Tridiagonal Matrix by LU Factorization (Python Coding)

```python
# Solves system with tridiagonal matrix by LU factorization
from random import *
from linsys import *

n = 100                                      # order of system
a = [0]*(n+1); a0 = [0]*(n+1)               # lower diagonal
b = [0]*(n+1); b0 = [0]*(n+1)               # main diagonal
c = [0]*(n+1); c0 = [0]*(n+1)               # upper diagonal
d = [0]*(n+1); x = [0]*(n+1)               # constant terms and solution

for i in range(1,n+1):                       # generate system
    if (i > 1): a[i] = a0[i] = random()          # a[i], i=2,n
    if (i < n): c[i] = c0[i] = random()          # c[i], i=1,n-1
    b[i] = b0[i] = random()
    d[i] = x[i]  = random()

TriDiagSys(a,b,c,x,n)                        # solve tridiagonal system
```
```