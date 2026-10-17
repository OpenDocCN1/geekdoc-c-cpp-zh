
```
x[k][j] = t

t = 2e0 * s * c * a[i][j]

d[i] = aii*c*c + ajj*s*s + t    # update eigenvalues

d[j] = ajj*c*c + aii*s*s - t

a[i][j] = 0e0

if (amax<=eps): break           # check convergence

if (it > itmax):

print("Jacobi: max. no. of iterations exceeded !"); return 1

return 0
```

存储在数组 `a` 的下三角中，而它们的对角元素被放置在向量 `d` 中。由于矩阵 `A_l` 的极限近似于对角矩阵 `Λ`，向量 `d` 在退出时包含矩阵 `A` 的计算特征值。

数组 `x` 在其列中返回 `A` 的特征向量。在例程运行期间，数组 `x` 用于存储连续旋转矩阵的元素，并在进入例程后立即通过单位矩阵进行初始化（`X0 = E`）。这种方法的理由是模态矩阵 `X` 被获得为变换矩阵序列 `X_l` 的极限。

局部变量 `t`、`c` 和 `s` 分别存储表征变换的旋转角 `φ` 的正切、余弦和正弦。`eps` 表示预定义的容差，与之比较产生的非对角数值“零”，而 `amax` 在每次正交变换后包含其绝对值的最大值。

由于在采用的经济存储使用策略中，数组 `a` 的上三角不参与基于公式 `8.20` 更新 `A_l` 的元素，因此对于 `k > j` 的 `a[j][k]`（来自上三角），必须使用对称元素 `a[k][j]`，而对于 `k > i` 的 `a[i][k]`，则需要考虑同样来自下三角的对称元素 `a[k][i]`。然而，这种方法要求将 `i > j` 的双重循环，其中评估元素 `a'_ik` 和 `a'_jk`，分解为三个循环，对应于索引 `k` 与 `i` 和 `j` 的三种可能顺序关系。

列表 8.2 展示了一个有用的辅助例程 `EigSort`，它通过选择排序方法（类似于插入排序；参见第 4 章）对存储在 `d` 中的特征值和存储在 `x` 中的相应特征向量进行重新排序，按特征值排序——如果 `isort>0` 则按升序，分别如果 `isort<0` 则按降序。

列表 8.3 说明了函数 `Jacobi` 和 `EigSort` 的典型用法，假设它们包含在模块 `eigsys.py` 中。为了例程 `Jacobi` 的正确操作，仅指定矩阵 `A` 的下三角就足够了。尽管如此，为了随后检查计算解的精度，主程序将数组 `a` 对称化，使用上三角作为备份副本。作为误差指示，使用特征值方程的最大范数，

## 列表 8.2 特征值和特征向量的排序（Python 编码）

```
# =================================================================================

def EigSort(x, d, n, isort):

# ---------------------------------------------------------------------------------

# Sorts the eigenvalues d and eigenvectors x according to the eigenvalues

# x - eigenvectors on columns

# d - vector of eigenvalues

# n - dimension of eigenvalue problem

# isort = 0: no sorting; > 0: ascending sorting; < 0: descending sorting

# ---------------------------------------------------------------------------------

    if (isort == 0): return

    for j in range(1,n):

        jmax = j; dmax = d[j]                 # find column of maximum eigenvalue

        for i in range(j+1,n+1):

            if (isort * (dmax - d[i]) > 0e0):

                jmax = i; dmax = d[i]

        if (jmax != j):

            d[jmax] = d[j]; d[j] = dmax       # swap current component with maximum

            for i in range(1,n+1):

                t = x[i][j]; x[i][j] = x[i][jmax]; x[i][jmax] = t
```

## 列表 8.3 对称矩阵的特征值和特征向量（Python 编码）

```
# Eigenvalues and eigenvectors of symmetric matrices by the Jacobi method

from eigsys import *

n = 4

a = [[0]*(n+1) for i in range(n+1)]

x = [[0]*(n+1) for i in range(n+1)]

d = [0]*(n+1)

a[1][1] = 1                                    # lower triangle

a[2][1] = 2; a[2][2] = 1

a[3][1] = 3; a[3][2] = 2; a[3][3] = 1

a[4][1] = 4; a[4][2] = 3; a[4][3] = 2; a[4][4] = 1

# Eigenvalues: -3.414214, -1.099019, -0.585786, 9.099020

for i in range(2,n+1):                        # complete upper triangle

    for j in range(1,i): a[j][i] = a[i][j]     # - not altered by Jacobi

Jacobi(a,x,d,n)

EigSort(x,d,n,1)                              # sort eigenvalues and eigenvectors

print("Eigenvalues:")

for i in range(1,n+1): print("{0:10.5f}".format(d[i]),end="")

print()

for i in range(2,n+1):                        # restore original matrix

    for j in range(1,i): a[i][j] = a[j][i]     # from upper triangle

err = 0e0

for i in range(1,n+1):                        # accuracy check

    for j in range(1,n+1):

        t = -x[i][j] * d[j]

        for k in range(1,n+1): t += a[i][k] * x[k][j]

        if (err < fabs(t)): err = fabs(t)      # err = max|A x - lambda x|

print("\nMaximum error = ","{0:8.2e}".format(err))
```

即 `‖A · x − λx‖ = max |(A · x − λx)ij|`，原则上预计与内部双精度浮点表示的精度相匹配。

## 8.4 对称矩阵的广义特征值问题

在某些应用数学问题中，例如源自量子力学形式体系的问题，可以出现所谓的广义特征值问题，它不是由单个矩阵，而是由两个方阵 `A` 和 `B` 定义：

`A · x = λ B · x.` `(8.30)`

在大多数情况下，这类问题是相对于有限维空间中非正交基，例如 `ℝⁿ` 的算子方程的矩阵表示。

假设矩阵 `B` 可逆，将广义方程 `(8.30)` 转换为标准方程 `(A · x = λx)` 的直接方法之一是对方程进行左乘 `B⁻¹`：

`(B⁻¹ · A) · x = λx.`

5. 基于

`x_ij = Σ_{k=i}^n l'_ki x̃_kj.` `(8.37)`

重组初始特征值问题 `(8.30)` 的特征向量 `x = (L⁻¹)ᵀ · x̃`。

在《第 8.4 节 代码清单》中给出的上述算法实现中，矩阵 `B` 的 Cholesky 分解通过调用函数 `Cholesky` 来执行，而所得下三角矩阵 `L` 的求逆则由例程 `MatTriInv` 执行（这两个例程均在第 7 章中开发并包含在模块 `linsys.py` 中）。所得标准特征值问题 `(8.34)` 的实际求解通过调用第 8.3 节中描述的函数 `Jacobi` 来执行。

## 代码清单 8.4 对称矩阵广义特征值问题的求解器（Python 代码）

```
#===============================================================================

def EigSym(a, b, x, d, n):

#-------------------------------------------------------------------------------

# Solves the generalized eigenvalue problem a x = lambda b x for the real

# symmetric matrix a and the real positive-definite symmetric matrix b,

# reducing it to standard form at xt = lambda xt by Cholesky factorization

# of matrix b = L * LT.

# a - real symmetric matrix

# b - real positive-definite symmetric matrix (L replaces lower triangle)

# x - modal matrix: eigenvectors on columns (output)

# d - vector of eigenvalues

# n - order of matrix a

# Error flag: 0 - normal execution

#             1 - matrix b not positive-definite

# Calls: Cholesky, MatTriInv, Jacobi.

#-------------------------------------------------------------------------------

    (det,i err) = Cholesky(b,n)                 # Cholesky factorization b = L * LT

    if (i err):

        print("EigSym: matrix b is not positive-definite!"); return 1

    MatTriInv(b,n)                              # b = L^(-1)

    for i in range(1,n):

        for j in range(i+1,n+1): a[i][j] = a[j][i]      # fill upper triangle of a

    at = [[0]*(n+1) for i in range(n+1)]

    xt = [[0]*(n+1) for i in range(n+1)]

    for i in range(1,n+1):      # transformed matrix at = L^(-1) * a * LT^(-1)

        for j in range(1,i+1):

            sum = 0e0

            for k in range(1,i+1):

                for m in range(1,j+1): sum += b[i][k] * a[k][m] * b[j][m]

            at[i][j] = sum

    Jacobi(at,xt,d,n)           # solve transformed problem at xt = lambda xt

    for j in range(1,n+1):                      # recompose eigenvectors of

        for i in range(1,n+1):                  # initial eigenvalue problem

            sum = 0e0

            for k in range(i,n+1): sum += b[k][i] * xt[k][j]

            x[i][j] = sum

    return 0
```

矩阵 `A` 和 `B` 的元素通过数组 `a` 和 `b` 的下三角部分传递给例程 `EigSym`。`b` 的下三角部分随后被用来依次存储分解矩阵 `L` 的元素和逆矩阵 `L⁻¹` 的元素。分配的数组 `at` 和 `xt` 分别对应于矩阵 `Ã` 和 `x̃`。例程退出时，数组 `d` 包含计算得到的特征值，而数组 `x` 在其列中返回相应的特征向量。

## 8.5 C/C++ 实现

代码清单 8.5 显示了文件 `eigsys.h` 的内容，其中包含与正文中开发并包含在模块 `eigsys.py` 中的 Python 函数等价的 C/C++ 实现。相应的例程具有相同的名称、参数和功能。

## 代码清单 8.5 特征值问题求解器（eigsys.h）

```
//------------------------------------------------------------- eigsys.h -------------------------------------------------------------

// Contains routines for solving eigenvalue problems.

// Part of the numxlib numerics library. Author: Titus Beu, 2013

//-------------------------------------------------------------

#ifndef _EIGSYS_

#define _EIGSYS_

#include <stdio.h>

#include <math.h>

#include "memalloc.h"

#include "linsys.h"

//==================================================================================================================================

int Jacobi(double **a, double **x, double d[], int n)

//-------------------------------------------------------------

// Solves the eigenvalue problem of a real symmetric matrix using the

// Jacobi method

// a  - real symmetric matrix (lower triangle is destroyed)

// x  - modal matrix: eigenvectors on columns (output)

// d  - vector of eigenvalues

// n  - order of matrix a

// Error flag: 0 - normal execution, 1 - exceeded max. no. of iterations

//-------------------------------------------------------------

{

    const double eps = 1e-30;                     // precision criterion

    const int itmax = 50;                         // max no. of iterations

    double aii, aij, ajj, amax, c, s, t;

    int i, it, j, k;

    for (i=1; i<=n; i++) {                         // initialization

        for (j=1; j<=n; j++) x[i][j] = 0e0;        // modal matrix = unit matrix

        x[i][i] = 1e0;

        d[i] = a[i][i];                           // eigenvalues = diagonal elements
```
