# Listing 7.18 Solution of Linear System with Tridiagonal Matrix (Python Coding)

```
# Solves system with tridiagonal matrix by LU factorization
from linsys import *

n = 4                                         # order of system
a = [0]*(n+1)                                # lower diagonal
b = [0]*(n+1)                                # main diagonal
c = [0]*(n+1)                                # upper diagonal
d = [0]*(n+1)                                # constant terms and solution

a[1] = 0; b[1] = 1; c[1] = 2; d[1] = 1
a[2] = 2; b[2] = 1; c[2] = 2; d[2] = 2
a[3] = 2; b[3] = 1; c[3] = 2; d[3] = 3
a[4] = 2; b[4] = 1; c[4] = 0; d[4] = 4          # Solution: -3.0, 2.0, 3.0, -2.0

TriDiagSys(a,b,c,d,n)                        # solve tridiagonal system

print("Solution:")
for i in range(1,n+1): print('{0:10.3f}'.format(d[i]),end="")
print()
```

this is reflected from a mathematical perspective by diagonally dominant coefficient matrices and from a numerical perspective, by the stability of the presented factorization method.

The typical usage of function TriDiagSys, assumed to be included in module linsys.py, is indicated in Listing 7.18. The system is specified just by its three nonzero diagonals, a, b, and c, while the vector d is used both to convey the constant terms to the routine and to return the calculated solution.

# 7.8 Block Tridiagonal Systems of Linear Equations

By applying discretization methods for solving systems of ordinary differential equations or differential equations with partial derivatives, sometimes, systems of linear equations with block tridiagonal matrix can result. Essentially, such matrix equations reflect some sort of intrinsic 2D coupling within the modeled system and their structure is

```
[ B₁  C₁          0 ] [ x₁ ]   [ d₁ ]
[ A₂  B₂  C₂       ] [ x₂ ]   [ d₂ ]
[   ⋱  ⋱  ⋱       ] [ ⋮  ] = [ ⋮  ]
[      Aᵢ  Bᵢ  Cᵢ  ] [ xᵢ ]   [ dᵢ ]
[          ⋱  ⋱  ⋱ ] [ ⋮  ]   [ ⋮  ]
[ 0        Aₙ₋₁ Bₙ₋₁ Cₙ₋₁ ] [ xₙ₋₁ ] [ dₙ₋₁ ]
[              Aₙ  Bₙ ] [ xₙ ]   [ dₙ ]   (7.89)
```

where Aᵢ, Bᵢ, and Cᵢ are (m × m) square matrices, while xᵢ and dᵢ are column vectors with m components. Obviously, the order of the coefficient matrix is (m × n).

In many problems of practical interest, due to the excessive size of the coefficient matrix, the solution of blocked systems by general methods, such as Gaussian elimination or LU factorization, is intractable and, therefore, out of question. Instead, a block tridiagonal matrix equation such as Equation 7.89 can