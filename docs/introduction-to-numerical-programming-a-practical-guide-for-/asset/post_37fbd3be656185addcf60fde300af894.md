
# Listing 7.9 Typical Sequence for Solving a Linear System by LU Factorization (Python Coding)

```
a = [[0]*(n+1) for i in range(n+1)]                # coefficient matrix
b = [0]*(n+1)                                      # vector of constant terms
ipivot = [0]*(n+1)                                 # vector of pivots
...
det = LUFactor(a,ipivot,n)
LUSystem(a,ipivot,b,n)
```

reflect the row permutations performed by the pivoting algorithm during the factorization. Specifically, the components of ipivot are just the indexes of the successive pivot rows and, accordingly, before being used, the constant terms b[i] and b[ipivot[i]] are interchanged. In solving the second system, U·x = y, the array b plays at first the role of the vector of constant terms y and, thereafter, on exit, it represents the final solution x.

A typical code sequence for solving a system of linear equations by LU decomposition is provided by Listing 7.9. It is assumed that arrays a, b, and ipivot are allocated with offset 1 and n components. The call to routine LUFactor replaces the coefficient matrix stored in a by its LU decomposition, returning at the same time the list of pivot rows in ipivot. Using the LU decomposition stored in a and the constant terms stored in b, the call to routine LUSystem returns in b the solution of the system.

The pair of routines LUFactor and LUSystem is particularly useful for calculating the inverse of a matrix and this is implemented in the routine MatInv included in Listing 7.10. Essentially, inverting a matrix implies first performing its LU factorization with the help of LUFactor and then the solution

# Listing 7.10 Matrix Inversion Using LU Factorization (Python Coding)

```
================================================================================
def MatInv(a, n):
#--------------------------------------------------------------------------------
# Calculates inverse of (n x n) matrix a by LU factorization.
# a - (n x n) matrix (input); a^(-1) (output)
# det - determinant of coefficient matrix (output).
# Calls: LUFactor, LUSystem.
#--------------------------------------------------------------------------------
aInv = [[0]*(n+1) for i in range(n+1)]      # temporary storage for inverse
b = [0]*(n+1)
ipivot = [0]*(n+1)                          # stores pivot rows

det = LUFactor(a,ipivot,n)                  # LU factorization of a
if (det == 0e0):                            # singular matrix
    print("MatInv: singular matrix!"); return 0e0

for j in range(1,n+1):                      # loop over columns of unit matrix
    for i in range(1,n+1): b[i] = 0e0       # column j
    b[j] = 1e0
    LUSystem(a,ipivot,b,n)                  # solve system
    for i in range(1,n+1): aInv[i][j] = b[i] # column j of inverse

for j in range(1,n+1):                      # copy inverse in a
    for i in range(1,n+1): a[i][j] = aInv[i][j]

return det
```

of a sequence of linear systems having as constant vectors the columns of the unit matrix by means of LUSystem. The successive solutions precisely represent the columns of the inverse matrix and, for their temporary storage, the routine allocates a supplementary array, ainv, which is finally copied in array a. In this way, the routine returns the inverse by the same array by which the original matrix is initially conveyed.

An example program designed for testing the matrix inversion performed by the routine MatInv is presented in Listing 7.11. The program generates a random matrix, creates a copy, inverts the copy, and multiplies the original array with its inverse. Owing to the roundoff errors, the result of the check is a numerical approximation of the unit matrix, having nondiagonal elements of the order 10^-15 – 10^-17. The invoked auxiliary functions for operations with 2D arrays are defined in the files matutil.py and matutil.h, respectively.

# Listing 7.11 Application of Matrix Inversion Based on LU Factorization (Python Coding)

```
# Check of matrix inversion using LU decomposition
from random import *
from linsys import *
from matutil import *

n = 5                                         # order of matrix
a = [[0]*(n+1) for i in range(n+1)]           # original matrix and inverse
b = [[0]*(n+1) for i in range(n+1)]           # backup of original
c = [[0]*(n+1) for i in range(n+1)]           # check matrix

for i in range(1,n+1):                        # generate random matrix
    for j in range(1,n+1): a[i][j] = random()

print("Original matrix:")
MatPrint(a,n,n)

MatCopy(a,b,n,n)                              # backup original matrix

det = MatInv(a,n)                             # invert original
if (det == 0e0): print("Singular matrix"); exit(1)

print("Inverse matrix:")
MatPrint(a,n,n)

print("Check A^(-1)A = I:")
MatProd(a,b,c,n,n,n)                          # multiply inverse with original
MatPrint(c,n,n)                               # print check matrix
```

The flops count involved by applying the LU factorization can be established similarly to the Gaussian elimination:

- LU factorization of the coefficient matrix A (Equations 7.42 and 7.43):
  - Summations and subtractions:

```
S_A(n) = sum_{j=1}^{n} sum_{i=1}^{j} (1 + sum_{k=1}^{i-2} 1) + sum_{j=1}^{n} sum_{i=j+1}^{n} (1 + sum_{k=1}^{j-2} 1) = 1/3 n^3 - 1/2 n^2 + 1/6 n,
```

- Multiplications and divisions:

$$M_A(n) = \sum_{j=1}^{n} \sum_{i=1}^{j} \sum_{k=1}^{i-1} 1 + \sum_{j=1}^{n} \sum_{i=j+1}^{n} \left(1 + \sum_{k=1}^{j-1} 1\right) = \frac{1}{3} n^3 - \frac{1}{3} n.$$

- Transformation of the vector of constant terms **b** (Equations 7.51 and 7.53):
  - Summations and subtractions:

$$S_b(n) = \sum_{i=2}^{n} \left(1 + \sum_{j=1}^{i-2} 1\right) + \sum_{i=1}^{n-1} \left(1 + \sum_{j=i+1}^{n-1} 1\right) = n^2 - n,$$

  - Multiplications and divisions:

$$M_b(n) = \sum_{i=2}^{n} \sum_{j=1}^{i-1} 1 + 1 + \sum_{i=1}^{n-1} \left(1 + \sum_{j=i+1}^{n} 1\right) = n^2.$$

- Solution of a single system of linear equations:

$$S_A(n) + M_A(n) + S_b(n) + M_b(n) = \frac{2}{3} n^3 + \frac{3}{2} n^2 - \frac{7}{6} n \sim \frac{2}{3} n^3. \qquad (7.54)$$

- Inversion of the coefficient matrix **A**:

$$S_A(n) + M_A(n) + n\left(S_b(n) + M_b(n)\right) = \frac{8}{3} n^3 - \frac{3}{2} n^2 - \frac{1}{6} n \sim \frac{8}{3} n^3. \qquad (7.55)$$

It can be noticed right away that the costs for all operations based on the LU decomposition perfectly coincide with the ones for the standard Gaussian elimination, proving that the two methods are *perfectly equivalent*. However, due to the possibility to store the details of the forward elimination, as contained in the matrices **L** and **U**, the LU factorization may be preferable in situations in which repeated solutions of a system are required for several vectors of constant terms that are not available at the same time.

## 7.5 Inversion of Triangular Matrices

Sometimes, even though rarely directly from the primary formulation of practical problems, the necessity arises for inverting *triangular* matrices. Two such examples are the solution of generalized eigenvalue problems for symmetric positive-definite matrices and the inversion thereof. In both cases, the standard procedure implies the Cholesky factorization of the matrix (see Section 7.6), followed by the inversion of the resulting lower triangular matrix.

It is easily provable that the inverse of a nonsingular (invertible) triangular matrix is equally a triangular matrix. From the detailed equality of the product of the lower triangular matrices **A** = $[a_{ij}]_{nn}$ and

A⁻¹ = [a′ᵢⱼ]ₙₙ with the unit matrix,

```
[ a₁₁ ⋱ 0 ; … aᵢⱼ … aᵢᵢ ; aₙ₁ … aₙₙ ] · [ a′₁₁ ⋱ 0 ; … a′ⱼⱼ ; … a′ⱼⱼ ; a′ₙ₁ … a′ₙₙ ] = Eₙ, (7.56)
```

the following relations can be established by identifying the corresponding elements:

```
∑ₖ₌ⱼⁱ aᵢₖ a′ₖⱼ = δᵢⱼ,  i = j,…,n,  j = 1,2,…,n. (7.57)
```

The diagonal equation (for i = j) has the simplest form, since the sum reduces to a single term, aⱼⱼ a′ⱼⱼ = 1, and it allows for the diagonal element of the inverse to be expressed:

```
a′ⱼⱼ = 1 / aⱼⱼ.
```

Descending on the same column j, the equation corresponding to i = j+1 reads aⱼ₊₁,ⱼ a′ⱼⱼ + aⱼ₊₁,ⱼ₊₁ a′ⱼ₊₁,ⱼ = 0, and enables a new element of the inverse situated on the same column to be expressed in terms of the already-calculated a′ⱼⱼ:

```
a′ⱼ₊₁,ⱼ = − 1 / aⱼ₊₁,ⱼ₊₁ aⱼ₊₁,ⱼ a′ⱼⱼ.
```

Generalizing the procedure and expressing from the last terms of the sums in Equation 7.57 the elements a′ᵢⱼ, we obtain the recurrence relations:

```
{ a′ⱼⱼ = 1 / aⱼⱼ,  j = 1,2,…,n,  a′ᵢⱼ = − 1 / aᵢᵢ ∑ₖ₌ⱼⁱ⁻¹ aᵢₖ a′ₖⱼ,  i = j+1,…,n. } (7.58)
```

Scanning these relations column wise and evaluating on each column j first the diagonal element a′ⱼⱼ and then the elements a′ᵢⱼ located on the rows i = j+1,…,n underneath, as indicated by Equations 7.58, the entries a′ₖⱼ on the right-hand sides are already calculated as they become necessary and Equations 7.58 prove to be algorithmically self-consistent.

The function MatTriInv from Listing 7.12 exactly translates Relations 7.58 and it is conceived so as to return the inverse through the same lower triangle of array a by which the initial matrix is introduced. The algorithm does not require pivoting, being perfectly stable for any invertible lower triangular matrix.
