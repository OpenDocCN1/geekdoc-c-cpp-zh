
# Solves multiple linear systems by LU factorization

```python
from random import *
from linsys import *
from matutil import *

n = 5                                         # order of system
a  = [[0]*(n+1) for i in range(n+1)]          # system matrix
a0 = [[0]*(n+1) for i in range(n+1)]          # backup matrix
b = [0]*(n+1)                                 # constant terms
x = [0]*(n+1)                                 # solution
ipivot = [0]*(n+1)                            # pivots

for i in range(1,n+1):                        # random matrix
    for j in range(1,n+1): a[i][j] = a0[i][j] = random()
print("A:")
MatPrint(a,n,n)

det = LUFactor(a,ipivot,n)                    # LU decomposition of a
print("LU decomposition:")
MatPrint(a,n,n)

for k in range(1,n+1):                        # loop over constant vectors
    for i in range(1,n+1): b[i] = x[i] = random()   # random constant terms
    print("b:")
    VecPrint(b,n)

    LUSystem(a,ipivot,x,n)                    # solve linear system

    err = 0e0                                 # check max(Ax-b) = 0
    for i in range(1,n+1):
        erri = -b[i]
        for j in range(1,n+1): erri += a0[i][j] * x[j]   # element i of (Ax-b)
        err = max(err,fabs(erri))
    print("   max(Ax-b) = {0:.1e}".format(err))
```

## 代码清单 7.24 用 LU 分解求解多个线性系统（C/C++ 编程）

```c
// Solves multiple linear systems by LU factorization
#include <stdio.h>
#include "memalloc.h"
#include "linsys.h"
#include "matutil.h"

int main()
{
    double **a, **a0, *b, *x, det, err, erri;
    int *ipivot, i, j, k, n;

    n = 5;                                    // order of system
    a  = Matrix(1,n,1,n);                     // system matrix
    a0 = Matrix(1,n,1,n);                     // backup matrix
    b = Vector(1,n);                          // constant terms
    x = Vector(1,n);                          // solution
    ipivot = IVector(1,n);                    // pivots

for (i=1; i<=n; i++)                         // random matrix
    for (j=1; j<=n; j++) a[i][j] = a0[i][j] = rand();
printf("A:\n");
MatPrint(a,n,n);

LUFactor(a,ipivot,n,det);                     // LU decomposition of a
printf("LU decomposition:\n");
MatPrint(a,n,n);

for (k=1; k<=n; k++) {                         // loop over constant vectors
    for (i=1; i<=n; i++) b[i] = x[i] = rand();       // random constant terms
    printf("b:\n");
    VecPrint(b,n);

    LUSystem(a,ipivot,x,n);                    // solve linear system

    err = 0e0;                                 // check max (Ax-b) = 0
    for (i=1; i<=n; i++) {
        erri = -b[i];
        for (j=1; j<=n; j++) erri += a0[i][j] * x[j]; // element i of (Ax-b)
        err = max(err,fabs(erri));
    }
    printf("   max (Ax-b) = % .1e\n",err);
}
}
```

## 问题 7.3

编写采用例程 `TriDiagSys` 的 Python 和 C/C++ 程序，用于求解阶数 `$n = 100$` 的三对角线性系统（见公式 7.78），矩阵元素随机生成。通过验证最大残差误差 `$\Delta = \max_i |a_i x_{i-1} + b_i x_i + c_i x_{i+1} - d_i|$` 的消失来综合检查解。

### 解答

Python 实现给出在代码清单 7.25 中，C/C++ 版本作为补充材料提供（`P07-TriDiagSys1.cpp`）。

### Listing 7.25 Solution of System with Tridiagonal Matrix by LU Factorization (Python Coding)

```python
# Solves system with tridiagonal matrix by LU factorization
from random import *
from linsys import *

n = 100                                      # order of system
a = [0]*(n+1); a0 = [0]*(n+1)               # lower diagonal
b = [0]*(n+1); b0 = [0]*(n+1)               # main diagonal
c = [0]*(n+1); c0 = [0]*(n+1)               # upper diagonal
d = [0]*(n+1); x = [0]*(n+1)               # constant terms and solution

for i in range(1,n+1):                       # generate system
    if (i > 1): a[i] = a0[i] = random()          # a[i], i=2,n
    if (i < n): c[i] = c0[i] = random()          # c[i], i=1,n-1
    b[i] = b0[i] = random()
    d[i] = x[i]  = random()

TriDiagSys(a,b,c,x,n)                        # solve tridiagonal system
```

```python
err = 0e0
for i in range(1,n+1):
    err -= b0[i]*x[i] - d[i]
    if (i > 1): err += a0[i]*x[i-1]
    if (i < n): err += c0[i]*x[i+1]
    err = max(err,fabs(err))
print("max(Ax-d) = {0:.1e}".format(err))
```

## 问题 7.4

对于两个非奇异矩阵 **A** 和 **B**，数值检验恒等式：

$$\det(A\cdot B)=\det(A)\det(B).$$

为此，(a) 生成两个 *随机* 2D 矩阵 **A** 和 **B**，阶数 `n=100`；(b) 使用例程 `Gauss` 计算 `$\det(A\cdot B)$` 和 `$\det(A)\det(B)$`；以及 (c) 检查两者表达式之间相对差的消失。

### 解答

由于其简单的消去阶段，例程 `Gauss` 特别高效地用于计算行列式。通过考虑 `m=0` 个常数项列来抑制回代。Python 实现给出在代码清单 7.26 中，C/C++ 版本作为补充材料提供（`P07-MatDetIdent.cpp`）。

**代码清单 7.26** 矩阵乘积行列式恒等式检验（Python 编程）

```python
# Check matrix identity det(A*B) == det(A)*det(B)
from random import *
from linsys import *
from matutil import *

n = 100
a = [[0]*(n+1) for i in range(n+1)]
b = [[0]*(n+1) for i in range(n+1)]
c = [[0]*(n+1) for i in range(n+1)]

for i in range(1,n+1):
    for j in range(1,n+1):
        a[i][j] = random()
        b[i][j] = random()

MatProd(a,b,c,n,n,n)                         # C = A * B
detA  = Gauss(a,b,n,0)                       # m=0: performs only elimination
detB  = Gauss(b,b,n,0)                       # and calculates the determinant
detAB = Gauss(c,b,n,0)

print("det(A)  = {0:9.2e}".format(detA))
print("det(B)  = {0:9.2e}".format(detB))
print("det(AB) = {0:9.2e}".format(detAB))
print("Error   = {0:9.2e}".format(1e0 - detA*detB/detAB))
```

## 问题 7.5

数值验证矩阵恒等式

$$(A \cdot B)^{-1} = B^{-1} \cdot A^{-1}.$$

为此，（a）生成两个 `n = 100` 阶的随机二维矩阵 `A` 和 `B`；（b）使用例程 `GaussJordan` 或 `MatInv` 计算 `A` 和 `B` 的逆矩阵，并计算差值矩阵

`D = (A · B)^{-1} − B^{-1} · A^{-1}`，

作为零矩阵的数值近似；（c）确定 `D` 的最大绝对值元素，作为最大误差的估计。

### 解答

Python 实现见代码清单 7.27，C/C++ 版本见补充材料（`P07-MatInvIdent.cpp`）。

### 代码清单 7.27 矩阵乘积逆的恒等式验证（Python 代码）

```python
# Check matrix identity: (A*B)^(-1) = B^(-1)*A^(-1)

from random import *

from linsys import *

from matutil import *

n = 100

a = [[0]*(n+1) for i in range(n+1)]

b = [[0]*(n+1) for i in range(n+1)]

c = [[0]*(n+1) for i in range(n+1)]

d = [[0]*(n+1) for i in range(n+1)]

for i in range(1,n+1):                # generate matrices a and b randomly

    for j in range(1,n+1):

        a[i][j] = random()

        b[i][j] = random()

MatProd(a,b,c,n,n,n)                          # c = a * b

det = GaussJordan(c,d,n,0)  # det = MatInv(c,n)      # c = (a b)^(-1)

det = GaussJordan(a,d,n,0)  # det = MatInv(a,n)      # a -> a^(-1)

det = GaussJordan(b,d,n,0)  # det = MatInv(b,n)      # b -> b^(-1)

MatProd(b,a,d,n,n,n)                          # d = b^(-1) a^(-1)

MatDiff(c,d,d,n,n)                            # d = (a b)^(-1) - b^(-1)a^(-1)

print("(A B)^(-1) - B^(-1)A^(-1)  (sample):\n")

MatPrint(d,5,5)                               # print sample of "zero" matrix

err = MatNorm(d,n,n)                          # max(abs(d[i][j]))

print("\nMaximum error = ","{0:8.2e}".format(err))
```

### 代码清单 7.28 通过 Cholesky 分解进行矩阵求逆（Python 代码）

```python
# Inversion of symmetric positive-definite matrix by Cholesky factorization

from random import *

from linsys import *

from matutil import *

n = 100                                          # order of matrices

a = [[0]* (n+1) for i in range(n+1)]

b = [[0]* (n+1) for i in range(n+1)]

c = [[0]* (n+1) for i in range(n+1)]

for i in range(1,n+1):                           # generate random lower triangular matrix

    for j in range(1 ,i+1): a[i][j] = random()    # lower triangle

    for j in range(i+1,n+1): a[i][j] = 0e0        # upper triangle

    a[i][i] += 1e0                               # increase diagonal

MatCopy(a,b,n,n)

MatTrans(b,n)                                    # create upper triangular matrix b = a^T

MatProd(a,b,c,n,n,n)                             # c = a a^T symmetric positive-definite

MatCopy(c,a,n,n)

MatCopy(c,b,n,n)

det = MatSymInv(a,n)                             # inverse by Cholesky factorization

MatProd(a,b,c,n,n,n)                             # c = a^(-1)a "unit" matrix

print("A^(-1)A (sample):\n")

MatPrint(c,5,5)                                  # print sample of "unit" matrix

for i in range(1,n+1): c[i][i] -= 1e0             # transform to "zero" matrix

err = MatNorm(c,n,n)                             # max(abs(c[i][j]))
```
