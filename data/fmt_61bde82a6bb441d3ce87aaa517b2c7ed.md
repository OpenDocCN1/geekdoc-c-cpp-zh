
# Hueckel method for benzene

```
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

在 `H₂O` 分子电子结构的密度泛函理论（DFT）计算中，Fock 矩阵 `F` 和重叠矩阵 `S` 的元素如下所列，并构成数据文件 `H2O.dat`。Fock 矩阵以常用原子单位，即哈特里单位指定（1 Hartree = 27.21 eV）。

读入文件 `H2O.dat`（清单 8.14）并通过使用例程 `EigSym` 求解矩阵 `F` 和 `S` 的广义特征值问题，

`FC = SCε`,

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

考虑到 `H₂O` 分子有 10 个电子，在基态下以自旋上-自旋下配对占据最低的 5 个能级 `εᵢ`，最高占据分子轨道（HOMO）为 `ε₅`，最低未占据分子轨道（LUMO）为 `ε₆`。确定 HOMO-LUMO 间隙，`ε₆−ε₅`，并通过估计最大范数 `‖FC−SCε‖ = maxᵢⱼ |(FC−SCε)ᵢⱼ|` 检查计算的精度。

## 解

Python 实现如清单 8.15 所示，C/C++ 版本作为补充材料提供（`P08-Roothaan.cpp`）。

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

## 表格函数的建模

### 9.1 插值与回归

对不完全已知或存在偏差的函数依赖进行建模的必要性出现在相当多样化的数值背景中，所发展的公式和方法的多样性正是其直接反映。

在数值应用中，经常需要使用仅知道其在离散网格点上取值的函数。这种不连续的依赖关系可以表示，例如，数学函数的表格或测量的物理量。为简单起见，我们将讨论限制在单个实变量的实值依赖关系。在这种情况下，定义在某个实区间上的函数

`f : [α, β] → ℝ, [α, β] ⊂ ℝ,`

由其在若干网格点 `x_i ∈ [α, β]` 上的取值 `y_i` 指定：

`f(x_i) = y_i, i = 1, 2, …, n.`

对这种依赖关系的数值处理经常需要使用对应于与表格化参数不同的参数的补充值。可惜的是，在许多情况下，获得对依赖关系的额外信息是困难的，如果不是不可能的话。特别是，即使算法是已知的，其复杂性也可能使在大规模计算中直接计算某些函数变得过于昂贵。另一方面，如果表格值来自观测，它们通常受到测量（观测）误差的影响。

为了综合表格依赖关系 `f` 的信息并在进一步计算中有效地使用它，常见的做法是用一个连续函数来近似它，称为模型函数，`F = F(x; a_1, …, a_m)`，它通常依赖于一定数量的可调模型参数 `a_j`。模型 `F` 的函数形式和参数 `a_j` 的取值有一定的自由度，但无论如何必须确定，以便以预定义的方式最优地近似离散函数 `f`。

模型函数 `F` 的具体选择确实是一个非平凡的任务，并且应尽可能基于严格的推理。总体而言，可用的选项如下：

- 模型函数从一个方便的类中选取（如多项式、高斯函数等），这确保了后处理的简单性和效率。
- 模型函数源自理论框架，其中参数具有明确的意义。
- 模型函数是前两种选项的约束和优势之间的折中。

为了确定最优模型参数，首先必须定义一个反映模型函数 `F` 近似表格依赖关系 `f` 的程度的泛函。承认通常遇到的情况，`f` 和 `F` 都是 `[α, β]` 上的平方可积函数（它们的平方的积分是有限的），

模型函数与被建模函数偏差的有用综合度量由距离提供

```
$$d(f,F)=\left\{\int_{\alpha}^{\beta}[f(x)-F(x;\mathbf{a})]^2dx\right\}^{1/2},$$
```

其中 `a` ≡ (`a₁, a₂,…`) 表示模型参数的集合。从建模问题的一般表述来看，很明显这个定义实际上不可操作，因为它意味着知道 `f` 的解析表达式。然而，一个不太严格但仅适用于离散函数的距离定义是

```
$$d(f,F)=\left\{\sum_{i=1}^{n}[f(x_i)-F(x_i;\mathbf{a})]^2\right\}^{1/2}.\tag{9.3}$$
```

基于距离 (9.3) 调整模型参数或将模型函数拟合到观测数据集的方法称为 *最小二乘逼近*，是两种基本方法，即 *插值* 和 *回归* 的核心。

**插值。** 如果表格值 `yᵢ = f(xᵢ)` 被认为是 *无误差* 或数值上 *精确* 的，那么自然要求函数 `f` 和 `F` 之间具有 *零距离*：

```
$$d(f,F)=0.\tag{9.4}$$
```

这相当于构造一个具有一定连续性类的模型函数，该函数在数据节点 `xᵢ` 处取与被建模函数 `f(x)` *相同的值*：

```
$$F(x_i;\mathbf{a})=y_i,\quad i=1,2,\dots,n.\tag{9.5}$$
```

满足这些条件的模型函数通常用于近似区间 `[x₁,xₙ]` 内点的函数 `f(x)`，该过程称为 *插值*。`F(x; a)` 称为 *插值函数* 或 *插值多项式*，而离散参数 `xᵢ` 也称为 *插值节点*。如果用于评估插值多项式的参数位于表格区间 `[x₁,xₙ]` 之外，则该方法称为 *外推*。

从几何角度看，插值意味着找到曲线 `y = F(x; a)` 经过 *所有* 数据点 `Mᵢ(xᵢ,yᵢ)`（见图 9.1a）。尽管有这样的一般表述，但建模问题可能有无限多个解或无解，这取决于模型函数所属的连续性类。相比之下，如果例如模型函数被

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_286_0.png)
