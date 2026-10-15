
```python
for k in range(i,n+1): sum += a[k][i] * a[k][j]

a[j][i] = sum                          # store in upper triangle

for i in range(1,n+1):                         # complete lower triangle

    for j in range(1,i+1): a[i][j] = a[j][i]

return det
```

需要初始化。下三角部分在调用 `Cholesky` 函数后依次容纳矩阵 `L`，并在调用 `MatTriInv` 函数后容纳矩阵 `L⁻¹`，该函数专门设计用于求逆三角矩阵，如第 7.5 节所述。最终的乘法 `(L⁻¹)ᵀ · L⁻¹` 在 `a` 的上三角部分产生 `A⁻¹` 的相关元素，然后将其复制到下三角部分，然后例程终止执行。

Cholesky 分解涉及的浮点运算计数如下：

- 系数矩阵 `A` 的 `L · Lᵀ` 分解（公式 7.63）：
  - 求和与减法：
  - 乘法与除法：
  - 平方根运算：`n`。

`S_A(n) = Σ_{j=1}^n (1 + Σ_{k=1}^{j-2} 1) + Σ_{j=1}^n Σ_{i=j+1}^n (1 + Σ_{k=1}^{j-2} 1) = 1/6 n³ - 1/6 n,`

`M_A(n) = Σ_{j=1}^n Σ_{k=1}^{j-1} 1 + Σ_{j=1}^n Σ_{i=j+1}^n (1 + Σ_{k=1}^{j-1} 1) = 1/6 n³ + 1/2 n² - 2/3 n,`

- 乘法 `A⁻¹ = (L⁻¹)ᵀ · L⁻¹`（公式 7.74）：
  - 求和与减法：
  
    \[S_I(n)=\sum_{j=1}^{n}\sum_{i=j+1}^{n}\sum_{k=i}^{n-1}1=\frac{1}{6}n^3-\frac{1}{2}n^2+\frac{1}{3}n\]
  
  - 乘法与除法：
  
    \[M_I(n)=\sum_{j=1}^{n}\sum_{i=j+1}^{n}\sum_{k=i}^{n}1=\frac{1}{6}n^3-\frac{1}{6}n\]

- 常数项向量 `b` 的变换（公式 7.69 和 7.71）：
  - 求和与减法：
  
    \[S_b(n)=\sum_{i=2}^{n}\left(1+\sum_{j=1}^{i-2}1\right)+\sum_{i=1}^{n-1}\left(1+\sum_{j=i+1}^{n-1}1\right)=n^2-n\]
  
  - 乘法与除法：
  
    \[M_b(n)=1+\sum_{i=2}^{n}\left(1+\sum_{j=1}^{i-1}1\right)+1+\sum_{i=1}^{n-1}\left(1+\sum_{j=i+1}^{n}1\right)=n^2+n\]

- 求解单个线性方程组（另加 *n* 次平方根运算）：
  
  \[S_A(n)+M_A(n)+S_b(n)+M_b(n)=\frac{1}{3}n^3+\frac{5}{2}n^2-\frac{5}{6}n-\frac{1}{3}n^3,\tag{7.75}\]

- 正定矩阵 `A` 的求逆（另加 *n* 次平方根运算）：
  
  \[S_A(n)+M_A(n)+\frac{1}{3}n^3+\frac{2}{3}n+S_I(n)+M_I(n)=n^3.\tag{7.76}\]

除 *n* 次额外的平方根运算外，Cholesky 分解在求逆正定矩阵（~*n*³）方面大约比 Gauss–Jordan 消去（~2*n*³）快 2 倍。

## 7.7 三对角线性方程组

在科学和工程的许多数值应用中，需要求解具有特殊结构的线性方程组。相当频繁地，这些是 *稀疏矩阵*，其元素主要等于零。有时，非零元素又结构化为包含主对角线以及可能两侧额外对角线的带状结构，这些被称为 *带矩阵*。

存在系数矩阵为 *三对角* 的情况，其相关元素局限于主对角线和两个相邻对角线。当用有限差分格式离散微分方程的边值问题时，或当用分段光滑函数插值数值表时，例如用样条函数（在第 9 章中处理）时，会出现具有三对角矩阵的系统。即使可以对这类系统的求解应用任何通用方法（高斯消去、LU 分解等），考虑到系数矩阵的特殊性会导致在初等运算和存储需求方面不可比较更高效的算法。

让我们考虑三对角线性方程组

`A · x = d`,    (7.77)

可以详细写成

[ [b1 c1      0] [a2 b2 c2] [⋱ ⋱ ⋱] [a_{i-1} b_{i-1} c_{i-1}] [a_i b_i c_i] [⋱ ⋱ ⋱] [0      a_{n-1} b_{n-1} c_{n-1}] [a_n b_n] ] [x1 x2 ⋮ x_{i-1} x_i ⋮ x_{n-1} x_n]^T = [d1 d2 ⋮ d_{i-1} d_i ⋮ d_{n-1} d_n]^T .   (7.78)

依据第 7.4 节所述的 LU 分解的哲学，求解该系统的最有效方法是把矩阵 `A` 分解为下双对角矩阵 `L` 和上双对角矩阵 `U` 的乘积：

`A = L · U`.    (7.79)

矩阵 `L` 和 `U` 可以包含与矩阵 `A` 中一样多的相关（原则上非零）条目，即 `3n − 2`（`A` 的两个副对角线只有 `n − 1` 个条目）。换句话说，从 `L` 和 `U` 的四个对角线中，只有三个可以从 `A` 的元素唯一确定，因此，我们可以任意指定第四个对角线的元素。如在一般 LU 分解的背景下所述，可以对 `L` 或 `U` 施加单位对角线，这两种选择在代数上完全等价。

在下文中，我们选择矩阵 `L` 的对角元素等于 1，使得两个分解矩阵具有结构：

`L = [ [1      0] [α2 1] [⋱ ⋱] [α_{i-1} 1] [α_i 1] [⋱ ⋱] [0      α_{n-1} 1] [α_n 1] ] ,   (7.80)`

`U = [ [β1 γ1      0] [β2 γ2] [⋱ ⋱] [β_{i-1} γ_{i-1}] [β_i γ_i] [⋱ ⋱] [0      β_{n-1} γ_{n-1}] [β_n] ] .   (7.81)`

识别矩阵 `A` 与 `L · U` 的对应元素可得：

\{ \begin{array}{lll} b_1 = \beta_1, & c_1 = \gamma_1, \\ a_i = \alpha_i \beta_{i-1}, & b_i = \alpha_i \gamma_{i-1} + \beta_i, & c_i = \gamma_i, \quad i = 2,3,\dots,n-1, \\ a_n = \alpha_n \beta_{n-1}, & b_n = \alpha_n \gamma_{n-1} + \beta_n. \end{array} \}

通过求逆这些关系，可表达矩阵 `L` 和 `U` 的元素：

\{ \begin{array}{l} \beta_1 = b_1, \\ \alpha_i = a_i / \beta_{i-1}, \quad \beta_i = b_i - \alpha_i c_{i-1}, \quad i = 2,3,\dots,n, \end{array} \quad (7.82) \\ \gamma_i = c_i, \quad i = 1,2,\dots,n-1.

正如人们可能注意到的那样，`U` 的元素 `γ_i` 与 `A` 的元素 `c_i` 完全一致，且根本不需要任何计算。只要 `β_i ≠ 0` 对 `i = 1,2,…,n` 成立，矩阵 `A` 就是非奇异的，且根据公式 7.82 的分解总是可能的。

有了 LU 分解，原系统 (7.78) 变为

`L · (U · x) = d`,

求解它相当于求解两个三对角系统：

\{ \begin{array}{l} L · y = d, \\ U · x = y. \end{array} \quad (7.83)

这些矩阵方程可详细写为

\begin{bmatrix} 1 & & & & & 0 \\ \alpha_2 & 1 & & & & \\ & \ddots & \ddots & & & \\ & & \alpha_{i-1} & 1 & & \\ & & & \alpha_i & 1 & \\ & & & & \ddots & \ddots \\ 0 & & & & \alpha_{n-1} & 1 \\ & & & & & \alpha_n & 1 \end{bmatrix} \begin{bmatrix} y_1 \\ y_2 \\ \vdots \\ y_{i-1} \\ y_i \\ \vdots \\ y_{n-1} \\ y_n \end{bmatrix} = \begin{bmatrix} d_1 \\ d_2 \\ \vdots \\ d_{i-1} \\ d_i \\ \vdots \\ d_{n-1} \\ d_n \end{bmatrix}, \quad (7.84)

\begin{bmatrix} \beta_1 & c_1 & & & & 0 \\ & \beta_2 & c_2 & & & \\ & & \ddots & \ddots & & \\ & & & \beta_{i-1} & c_{i-1} & \\ & & & & \beta_i & c_i \\ & & & & & \ddots & \ddots \\ 0 & & & & & \beta_{n-1} & c_{n-1} \\ & & & & & & \beta_n \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_{i-1} \\ x_i \\ \vdots \\ x_{n-1} \\ x_n \end{bmatrix} = \begin{bmatrix} y_1 \\ y_2 \\ \vdots \\ y_{i-1} \\ y_i \\ \vdots \\ y_{n-1} \\ y_n \end{bmatrix}. \quad (7.85)

从方程 7.84 中识别对应的项，可按指标升序表达中间解 `y` 的分量：

`y1 = d1,`
 `y_i = d_i − α_i y_{i−1},   i = 2,3,…,n.   (7.86)`

为了提高计算效率，我们将上述关系与方程 7.82 结合起来，其中指标同样按升序运行，以定义算法的分解阶段：

`α_i = a_i/β_{i−1},   β_1 = b_1,   y_1 = d_1,`
 `β_i = b_i − α_i c_{i−1},   y_i = d_i − α_i y_{i−1},   i = 2,3,…,n.   (7.87)`

通过同样从方程 7.85 两侧识别对应元素的技术，我们通过回表表达最终解 `x`：

`x_n = y_n/β_n,`
 `x_i = (y_i − c_i x_{i+1})/β_i,   i = n−1,…,1.   (7.88)`

对方程 7.87 和 7.88 所涉及的数据流的分析表明，对于算法的具体实现，四个数组 `a`、`b`、`c` 和 `d` 分别与量 `a_i`、`b_i`、`c_i` 和 `d_i` 相关联就足够了。系数 `α_i` 可存储在数组 `a` 中，覆盖用于计算它们的 `a_i` 值。类似地，系数 `β_i` 用数组 `b` 中的 `b_i` 值替换。数组 `c` 的条目保持不变，因为每个元素 `γ_i` 与对应的 `c_i` 完全一致。考虑到它们的逻辑重叠，量 `d_i`、`y_i` 和 `x_i` 可以依次存储在同一个数组 `d` 中，最终包含系统的解。

算法 7.87–7.88 以及关于最优存储使用的上述考虑已编码在第 7.17 节列表中所示的函数 `TriDiagSys` 内。由于没有进行主元选择，`TriDiagSys` 在原则上即使系数矩阵是非奇异的，只要某个系数 `β_i` 为零就可能失败。然而，通常导致三对角系统的实际问题本质上是良态的，

## Listing 7.17 Solver for Linear Systems with Tridiagonal Matrix (Python Coding)

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

这从数学角度由对角占优系数矩阵反映出来，从数值角度由所提出分解方法的稳定性反映出来。

函数 `TriDiagSys` 的典型用法，假定包含在模块 `linsys.py` 中，在第 7.18 节列表中给出。系统仅由其三个非零对角线 `a`、`b` 和 `c` 指定，而向量 `d` 用于将常数项传给例程并返回计算出的解。

## Listing 7.18 Solution of Linear System with Tridiagonal Matrix (Python Coding)

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

## 7.8 Block Tridiagonal Systems of Linear Equations

通过求解常微分方程系统或偏微分方程的离散化方法，有时可得到具有块三对角矩阵的线性方程组。本质上，这类矩阵方程反映了所建模系统中的某种内在二维耦合，其结构为

```
[ B₁  C₁          0 ] [ x₁ ]   [ d₁ ]

[ A₂  B₂  C₂       ] [ x₂ ]   [ d₂ ]

[   ⋱  ⋱  ⋱       ] [ ⋮  ] = [ ⋮  ]

[      Aᵢ  Bᵢ  Cᵢ  ] [ xᵢ ]   [ dᵢ ]

[          ⋱  ⋱  ⋱ ] [ ⋮  ]   [ ⋮  ]

[ 0        Aₙ₋₁ Bₙ₋₁ Cₙ₋₁ ] [ xₙ₋₁ ] [ dₙ₋₁ ]

[              Aₙ  Bₙ ] [ xₙ ]   [ dₙ ]   (7.89)
```
