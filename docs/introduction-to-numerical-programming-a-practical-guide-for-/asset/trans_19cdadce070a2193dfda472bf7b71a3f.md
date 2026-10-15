

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_280_0.png)

图 8.3 初始构型中的飞机（左上），绕 x 轴旋转至主轴系，主对称轴沿 x（右上），绕垂直 z 轴旋转（偏航）（左下），以及绕 x 轴旋转（滚转）（右下）。

## 问题 8.5

在 Hückel 理论框架下，通过求解标准特征值问题求出环状苯分子 C₆H₆ 的本征能量和本征向量：

H · C = C · E.

哈密顿矩阵可以用库仑积分 α = −6.9 eV 和共振能 β = −3.1 eV 表示（Broglia and Heilbronner 1972）：

```
H = [ [α, β, 0, 0, 0, β], [β, α, β, 0, 0, 0], [0, β, α, β, 0, 0], [0, 0, β, α, β, 0], [0, 0, 0, β, α, β], [β, 0, 0, 0, β, α] ]
```

精确的本征值（E 的对角元素）和本征向量为

E₁ = α + 2β,    E₂ = E₃ = α + β,    E₄ = E₅ = α − β,    E₆ = α − 2β,

C₁ = 1/√6 [1 1 1 1 1 1]ᵀ , C₂ = 1/2 [1 1 0 -1 -1 0]ᵀ , C₃ = 1/2 [1 0 -1 -1 0 1]ᵀ ,

C₄ = 1/2 [1 -1 0 1 -1 0]ᵀ , C₅ = 1/2 [1 0 -1 1 0 -1]ᵀ , C₆ = 1/√6 [1 -1 1 -1 1 -1]ᵀ .

利用例程 EigSym，证明非简并态 E₁ 和 E₆ 的精确本征值和本征向量被正确再现，并解释为什么简并态的本征向量与精确值不同，但仍是正确的。通过最大范数估计解的精度：

‖H · C − C · E‖ = maxᵢⱼ |(H · C − C · E)ᵢⱼ| ,

其预期为零。

## 解

应注意，作为一般性质，对应于简并本征值的本征向量的任意线性组合仍是对应于相同本征值的本征向量。相应地，能级 E₂ = E₃ 和 E₄ = E₅ 为二重简并，可以通过任意线性组合 γ₂C₂ + γ₃C₃ 以及分别 γ₄C₄ + γ₅C₅ 正确描述。

Python 实现如清单 8.13 所示，C/C++ 版本作为补充材料提供（P08-Hueckel.cpp）。

### 清单 8.13 苯的 Hückel 方法（Python 编码）

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

## 问题 8.6

在 H₂O 分子电子结构的密度泛函理论（DFT）计算中，Fock 矩阵 F 和重叠矩阵 S 的元素如下所列，并构成数据文件 H2O.dat。Fock 矩阵以常用原子单位，即哈特里单位指定（1 Hartree = 27.21 eV）。

读入文件 H2O.dat（清单 8.14）并通过使用例程 EigSym 求解矩阵 F 和 S 的广义特征值问题，

FC = SCε,

称为 Roothaan 方程（Szabo and Ostlund 1996）。

### 清单 8.14 文件 H2O.dat：H₂O 分子的 Fock 和重叠矩阵

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

考虑到 H₂O 分子有 10 个电子，在基态下以自旋上-自旋下配对占据最低的 5 个能级 εᵢ，最高占据分子轨道（HOMO）为 ε₅，最低未占据分子轨道（LUMO）为 ε₆。确定 HOMO-LUMO 间隙，ε₆−ε₅，并通过估计最大范数 ‖FC−SCε‖ = maxᵢⱼ |(FC−SCε)ᵢⱼ| 检查计算的精度。

## 解

Python 实现如清单 8.15 所示，C/C++ 版本作为补充材料提供（P08-Roothaan.cpp）。

### 清单 8.15 H₂O 分子 Roothaan 方程的求解（Python 编码）

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

## 参考文献和建议进一步阅读

- Beu, T. A. 2004. *Numerical Calculus in C*（第 3 版，罗马尼亚文）。Cluj-Napoca: MicroInformatica.
- Bondi, A. 1964. van der Waals Volumes and Radii. *Journal of Physical Chemistry* 68(3), 441–451.
- Brogli, F. and E. Heilbronner. 1972. Correlation of Hückel molecular orbital energies with π-ionization potentials. *Theoretica Chimica Acta (Berlin)* 26, 289–299.
- Burden, R. and J. Faires. 2010. *Numerical Analysis*（第 9 版）。Boston: Brooks/Cole, Cengage Learning.
- Demidovich, B. and I. Maron. 1987. *Computational Mathematics*（第 4 版）。Moscow: MIR Publishers.
- Maor, E. 1975. A discrete model for the vibrating string. *International Journal of Mathematical Education in Science and Technology* 6(3), 345–352.
- Szabo, A. and N. S. Ostlund. 1996. *Modern Quantum Chemistry: Introduction to Advanced Electronic Structure Theory*. Mineola, NY: Dover Publications.

