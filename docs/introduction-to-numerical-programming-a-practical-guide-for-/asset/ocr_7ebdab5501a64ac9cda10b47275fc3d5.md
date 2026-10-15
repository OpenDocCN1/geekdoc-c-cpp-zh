# Listing 7.2 Solution of a Linear System by Gaussian Elimination (Python Coding)

```
# Solves linear system by Gauss elimination
from linsys import *
from matutil import *

n = 4                                          # order of system
m = 1                                          # number of constant vectors
a = [[0]*(n+1) for i in range(n+1)]            # system matrix
b = [[0]*(m+1) for i in range(n+1)]            # constant terms

a[1][1] = 1; a[1][2] = 2; a[1][3] = 3; a[1][4] = 4; b[1][1] = 30
a[2][1] = 2; a[2][2] = 1; a[2][3] = 2; a[2][4] = 3; b[2][1] = 22
a[3][1] = 3; a[3][2] = 2; a[3][3] = 1; a[3][4] = 2; b[3][1] = 18
a[4][1] = 4; a[4][2] = 3; a[4][3] = 2; a[4][4] = 1; b[4][1] = 20
                                          # Solution: 1.0, 2.0, 3.0, 4.0; det = -20.0
print("A:")
MatPrint(a,n,n)
print("B:")
MatPrint(b,n,m)

det = Gauss(a,b,n,m)                          # solve system

print("det A =",det)
print("Solution:")
MatPrint(b,n,m)
```

# 7.3 Gauss–Jordan Elimination

The Gauss–Jordan method can be regarded as a variant of the Gaussian elimination, in which, instead of transforming the coefficient matrix A by elementary row operations into upper triangular form, the elimination process is carried out at each step within the entire matrix, which is finally transformed into the unit matrix. As such, even though the forward elimination phase is more elaborate, the backward substitution is eliminated altogether. In addition, by efficient coding and memory usage, the Gauss–Jordan elimination allows for the inverse of the coefficient matrix A⁻¹ to be calculated in place, simultaneously with the solution of a matrix equation.

Let us consider again the simple numerical example that was solved in the previous section using the standard Gaussian elimination with backward substitution:

[ 3  4  5 ] [ x₁ ]   [ 10 ]
[ 4  2  3 ] [ x₂ ] = [  9 ]
[ -2 -3  1 ] [ x₃ ]   [  7 ]

At the first step of the elimination, the unknown x₁ is to be eliminated from all equations (second and third), except for the first one. To this end, we first divide the first equation by the leading coefficient 3:

[ 1  4/3  5/3 ] [ x₁ ]   [ 10/3 ]
[ 4   2    3  ] [ x₂ ] = [   9  ]
[ -2 -3    1  ] [ x₃ ]   [   7  ]