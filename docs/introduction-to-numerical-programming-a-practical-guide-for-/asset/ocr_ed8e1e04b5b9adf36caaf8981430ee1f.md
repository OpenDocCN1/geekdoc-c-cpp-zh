| 0.00 0.00 0.00 0.00 0.00 0.50 0.00 0.00 1.00 |
| 0.03 0.23 0.41 0.27 0.01 0.00 0.58 0.01 0.00 1.00 |
| 0.07 0.37 0.67 0.15 0.00 0.00 0.49 0.01 0.00 0.66 1.00 |
| 0.03 0.23 0.41 -0.08 0.26 0.00 -0.18 0.55 0.00 0.04 0.20 1.00 |
| 0.07 0.37 0.67 -0.05 0.14 0.00 -0.15 0.46 0.00 0.20 0.49 0.66 1.00 |

Taking into account that the H₂O molecule has 10 electrons, which, in the ground state, occupy in spin-up–spin-down pairs the lowest 5 energy levels εᵢ, the highest occupied molecular orbital (HOMO) is ε₅ and the lowest unoccupied molecular orbital (LUMO) is ε₆. Determine the HOMO–LUMO gap, ε₆−ε₅, and check the accuracy of the calculation by estimating the max norm ‖FC−SCε‖ = maxᵢⱼ |(FC−SCε)ᵢⱼ|.

# Solution

The Python implementation is shown in Listing 8.15 and the C/C++ version is available as supplementary material (P08-Roothaan.cpp).

# Listing 8.15 Solution of the Roothaan Equation for the H₂O Molecule (Python Coding)

```
# Solves the Roothaan equation F C = S C E for the H2O molecule
from eigsys import *
from matutil import *

n = 13

C = [[0]*(n+1) for i in range(n+1)]                 # molecular coefficients
F = [[0]*(n+1) for i in range(n+1)]                 # Fock matrix
S = [[0]*(n+1) for i in range(n+1)]                 # overlap matrix
S0 = [[0]*(n+1) for i in range(n+1)]                # backup copy of overlap matrix
E = [0]*(n+1)                                       # energy levels

f = open('H2O.dat','r')                             # read in F and S
line = f.readline()                                 # skip header
for i in range(1,n+1):                              # read in lower triangle of F
    line = f.readline()                             # F not altered by EigSym
    for j in range(1,i+1):
        F[i][j] = float(line.split()[j-1])
        F[j][i] = F[i][j]                           # symmetrize

line = f.readline()                                 # skip header
for i in range(1,n+1):
    line = f.readline()
    for j in range(1,i+1):                          # read in lower triangle of S
        S[i][j] = float(line.split()[j-1])          # S destroyed by EigSym
        S0[i][j] = S0[j][i] = S[i][j]               # backup S
f.close()

print("F: Fock matrix (sample)")
MatPrint(F,5,5)
print("S: overlap matrix (sample)")
MatPrint(S,5,5)

EigSym(F,S,C,E,n)                                   # solve Roothaan equation
EigSort(C,E,n,1)                                    # sort eigenvalues and eigenvectors

print("\nEigenenergies:")
VecPrint(E,n)
```