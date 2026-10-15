Identifying the corresponding entries from Equation 7.84, one can express the components of the intermediate solution y in ascending order of the indexes:

y1 = d1,
 y_i = d_i − α_i y_{i−1},   i = 2,3,…,n.   (7.86)

To improve the efficiency of the calculations, we group the above relations with Equations 7.82, for which the index equally runs in ascending order, to define the factorization phase of the algorithm:

α_i = a_i/β_{i−1},   β_1 = b_1,   y_1 = d_1,
 β_i = b_i − α_i c_{i−1},   y_i = d_i − α_i y_{i−1},   i = 2,3,…,n.   (7.87)

Through the same technique of identifying the corresponding elements from both sides of Equation 7.85, we express the final solution x by backward substitution:

x_n = y_n/β_n,
 x_i = (y_i − c_i x_{i+1})/β_i,   i = n−1,…,1.   (7.88)

The analysis of the data flow involved in Equations 7.87 and 7.88 reveals that, for the concrete implementation of the algorithm, four arrays, a, b, c, and d, associated, respectively, with the quantities a_i, b_i, c_i, and d_i, are sufficient. The coefficients α_i can be stored in array a, overwriting the values a_i that have been used to calculate them. Similarly, coefficients β_i replace the values b_i in array b. The entries of array c remain unchanged, since each element γ_i coincides with the corresponding c_i. Having in view their logical overlap, the quantities d_i, y_i, and x_i can be successively stored in the same array d, which finally contains the solution of the system.

Algorithm 7.87–7.88 and the above considerations on the optimal storage usage are coded within the function TriDiagSys shown in Listing 7.17. Since no pivoting is carried out, TriDiagSys can fail, in principle, even if the coefficient matrix is nonsingular, but one of the coefficients β_i vanishes. Typically, however, the practical problems leading to tridiagonal systems are by nature well behaved and

# Listing 7.17 Solver for Linear Systems with Tridiagonal Matrix (Python Coding)

```
# ===========================================================
def TriDiagSys(a, b, c, d, n):
# -----------------------------------------------------------
# Solves a system with tridiagonal matrix by LU factorization (diag(L) = 1).
# a - lower codiagonal (i=2,n)
# b - main diagonal (i=1,n)
# c - upper codiagonal (i=1,n-1)
# d - constant terms (i=1,n); solution on exit
# n - order of system.
# -----------------------------------------------------------
if (b[1] == 0e0): print("TriDiagSys: singular matrix!"); return
for i in range(2,n+1):                # factorization
a[i] /= b[i-1]
b[i] -= a[i]*c[i-1]
if (b[i] == 0e0): print("TriDiagSys: singular matrix!"); return
d[i] -= a[i]*d[i-1]

d[n] /= b[n]                          # backward substitution
for i in range(n-1,0,-1): d[i] = (d[i] - c[i]*d[i+1])/b[i]
```