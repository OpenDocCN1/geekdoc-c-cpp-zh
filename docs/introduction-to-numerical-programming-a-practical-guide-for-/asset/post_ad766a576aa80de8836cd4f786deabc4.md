
![](img/5c6c126e3d8cf2b3029f4242e9ad2887_280_0.png)

FIGURE 8.3 Airplane in the initial configuration (top left), rotated to the system of principal axes with the main symmetry axis along x (top right), rotated around the vertical z axis (yaw) (bottom left), and rotated about the x-axis (roll) (bottom right).

## PROBLEM 8.5

Find the eigenenergies and eigenvectors for the cyclic benzene molecule C₆H₆ in the framework of the Hückel theory by solving the standard eigenvalue problem:

H · C = C · E.

The Hamiltonian matrix can be expressed in terms of the Coulomb integral, α = −6.9 eV, and the resonance energy, β = −3.1 eV (Broglia and Heilbronner 1972):

```
H = [ [α, β, 0, 0, 0, β], [β, α, β, 0, 0, 0], [0, β, α, β, 0, 0], [0, 0, β, α, β, 0], [0, 0, 0, β, α, β], [β, 0, 0, 0, β, α] ]
```

The exact eigenvalues (diagonal elements of E) and eigenvectors are

E₁ = α + 2β,    E₂ = E₃ = α + β,    E₄ = E₅ = α − β,    E₆ = α − 2β,

C₁ = 1/√6 [1 1 1 1 1 1]ᵀ , C₂ = 1/2 [1 1 0 -1 -1 0]ᵀ , C₃ = 1/2 [1 0 -1 -1 0 1]ᵀ ,

C₄ = 1/2 [1 -1 0 1 -1 0]ᵀ , C₅ = 1/2 [1 0 -1 1 0 -1]ᵀ , C₆ = 1/√6 [1 -1 1 -1 1 -1]ᵀ .

Using the routine EigSym, prove that the exact eigenvalues and eigenvectors for the nondegenerate states E₁ and E₆ are correctly reproduced and explain why the eigenvectors for the degenerate states differ from the exact ones, being yet correct. Estimate the accuracy of the solution by means of the max norm:

‖H · C − C · E‖ = maxᵢⱼ |(H · C − C · E)ᵢⱼ| ,

which is expected to vanish.

## Solution

It should be noted, as a general property, that any linear combination of eigenvectors corresponding to degenerate eigenvalues is still an eigenvector corresponding to the same eigenvalue. Correspondingly, the energy levels E₂ = E₃ and E₄ = E₅ are two-fold degenerate and can be described properly by any linear combination γ₂C₂ + γ₃C₃ and, respectively, γ₄C₄ + γ₅C₅.

The Python implementation is shown in Listing 8.13 and the C/C++ version is available as supplementary material (P08-Hueckel.cpp).

### Listing 8.13 Hueckel Method for Benzene (Python Coding)

```
# Hueckel method for benzene
from eigsys import *
from matutil import *

n = 6

H = [[0]*(n+1) for i in range(n+1)]                 # Hamiltonian matrix
C = [[0]*(n+1) for i in range(n+1)]                 # molecular coefficients
E = [0]*(n+1)                                       # eigenenergies

alpha = -6.9                                        # Coulomb & resonance integrals: F. Brogli &
beta = -3.2                                         # E. Heilbronner, Theoret. Chim. Acta 1972

for i in range(1,n+1): H[i][i] = alpha               # diagonal elements
for i in range(1,n):
    H[i+1][i] = beta; H[i][i+1] = beta               # off-diagonal elements
H[1][6] = beta; H[6][1] = beta                       # cyclic boundary conditions
X = (0, alpha+2*beta, alpha+beta, alpha+beta, \     # exact eigenenergies
     alpha-beta, alpha-beta, alpha-2*beta )
print("Eigenenergies (exact):")
VecPrint(X,n)
```

```
Jacobi(H,C,E,n)
EigSort(C,E,n,1)                      # sort eigenvalues and eigenvectors

print("Eigenenergies (eV):")
VecPrint(E,n)

print("Eigenvectors:")
MatPrint(C,n,n)

for i in range(2,n+1):                # restore Hamiltonian
    for j in range(1,i): H[i][j] = H[j][i]   # from upper triangle

err = 0e0
for i in range(1,n+1):
    for j in range(1,n+1):
        t = - E[j] * C[i][j]
        for k in range(1,n+1): t += H[i][k] * C[k][j]
        if (err < fabs(t)): err = fabs(t)    # err = max|A x - lambda x|

print("\nMaximum error = {0:8.2e}".format(err))
```

## PROBLEM 8.6

In a density functional theory (DFT) calculation of the electronic structure of the H₂O molecule, the Fock matrix F and the overlap matrix S have the elements listed below and compose the data file H2O.dat. The Fock matrix is specified in the commonly used atomic units, the so-called Hartrees (1 Hartree = 27.21 eV).

Read in the file H2O.dat (Listing 8.14) and solve the generalized eigenvalue problem of the matrices F and S,

FC = SCε,

known as the Roothaan equation (Szabo and Ostlund 1996), by using the routine EigSym.

### Listing 8.14 File H2O.dat: Fock and Overlap Matrices for the H₂O Molecule

```
F: Fock matrix
-18.74
-4.74 -1.74
-3.34 -1.65 -1.26
-0.01 -0.07 -0.07 -0.10
-0.02 -0.10 -0.10 0.02 -0.08
0.00 0.00 0.00 0.00 0.00 -0.02
0.00 -0.05 -0.10 -0.44 0.02 0.00 -0.06
0.00 -0.06 -0.14 0.02 -0.43 0.00 0.04 -0.03
0.00 0.00 0.00 0.00 0.00 -0.37 0.00 0.00 0.11
-0.63 -0.56 -0.51 -0.38 -0.02 0.00 -0.29 -0.02 0.00 -0.17
-1.34 -0.84 -0.70 -0.22 -0.05 0.00 -0.16 -0.07 0.00 -0.48 -0.44
-0.63 -0.56 -0.51 0.11 -0.36 0.00 0.08 -0.28 0.00 -0.11 -0.26 -0.17
-1.34 -0.84 -0.70 0.03 -0.22 0.00 -0.02 -0.18 0.00 -0.26 -0.39 -0.48 -0.44
S: overlap matrix
1.00
0.23 1.00
0.17 0.76 1.00
0.00 0.00 0.00 1.00
0.00 0.00 0.00 0.00 1.00
0.00 0.00 0.00 0.00 0.00 1.00
0.00 0.00 0.00 0.50 0.00 0.00 1.00
0.00 0.00 0.00 0.00 0.50 0.00 0.00 1.00
0.00 0.00 0.00 0.00 0.00 0.50 0.00 0.00 1.00
0.03 0.23 0.41 0.27 0.01 0.00 0.58 0.01 0.00 1.00
0.07 0.37 0.67 0.15 0.00 0.00 0.49 0.01 0.00 0.66 1.00
0.03 0.23 0.41 -0.08 0.26 0.00 -0.18 0.55 0.00 0.04 0.20 1.00
0.07 0.37 0.67 -0.05 0.14 0.00 -0.15 0.46 0.00 0.20 0.49 0.66 1.00
```

Taking into account that the H₂O molecule has 10 electrons, which, in the ground state, occupy in spin-up–spin-down pairs the lowest 5 energy levels εᵢ, the highest occupied molecular orbital (HOMO) is ε₅ and the lowest unoccupied molecular orbital (LUMO) is ε₆. Determine the HOMO–LUMO gap, ε₆−ε₅, and check the accuracy of the calculation by estimating the max norm ‖FC−SCε‖ = maxᵢⱼ |(FC−SCε)ᵢⱼ|.

## Solution

The Python implementation is shown in Listing 8.15 and the C/C++ version is available as supplementary material (P08-Roothaan.cpp).

### Listing 8.15 Solution of the Roothaan Equation for the H₂O Molecule (Python Coding)

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

```
print("\nHOMO–LUMO gap E[6]–E[5] = {0:4.3f} Hartrees".format(E[6]-E[5]))

err = 0e0
for i in range(1,n+1):
    for j in range(1,n+1):
        t = 0e0
        for k in range(1,n+1): t += (F[i][k] - E[j]*S0[i][k]) * C[k][j]
        if (err < fabs(t)): err = fabs(t)          # err = max|a x – lambda x|

print("\nMaximum error = {0:8.2e}".format(err))
```

## References and Suggested Further Reading

- Beu, T. A. 2004. *Numerical Calculus in C* (3rd ed., in Romanian). Cluj-Napoca: MicroInformatica.
- Bondi, A. 1964. van der Waals Volumes and Radii. *Journal of Physical Chemistry* 68(3), 441–451.
- Brogli, F. and E. Heilbronner. 1972. Correlation of Hückel molecular orbital energies with π-ionization potentials. *Theoretica Chimica Acta (Berlin)* 26, 289–299.
- Burden, R. and J. Faires. 2010. *Numerical Analysis* (9th ed.). Boston: Brooks/Cole, Cengage Learning.
- Demidovich, B. and I. Maron. 1987. *Computational Mathematics* (4th ed.). Moscow: MIR Publishers.
- Maor, E. 1975. A discrete model for the vibrating string. *International Journal of Mathematical Education in Science and Technology* 6(3), 345–352.
- Szabo, A. and N. S. Ostlund. 1996. *Modern Quantum Chemistry: Introduction to Advanced Electronic Structure Theory*. Mineola, NY: Dover Publications.
