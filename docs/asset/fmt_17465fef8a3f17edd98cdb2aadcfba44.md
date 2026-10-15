
- 变换单个常数项向量 `b`（`m = 1`）：
  - 求和与减法（方程 7.21 和 7.22）：
    $$S_b(n) = \sum_{k=1}^{n} \sum_{i=k+1}^{n} 1 + \sum_{k=1}^{n-1} \left(1 + \sum_{i=k+1}^{n-1} 1\right) = n^2 - n,$$
  - 乘法与除法（方程 7.20 至 7.22）：
    $$M_b(n) = \sum_{k=1}^{n} 1 + \sum_{k=1}^{n} \sum_{i=k+1}^{n} 1 + \sum_{k=1}^{n-1} \sum_{i=k+1}^{n} 1 = n^2.$$

- 求解单个线性方程组：
  $$S_A(n) + M_A(n) + S_b(n) + M_b(n) = \frac{2}{3} n^3 + \frac{3}{2} n^2 - \frac{7}{6} n \sim \frac{2}{3} n^3. \tag{7.23}$$

- 求逆系数矩阵 `A` 或求解 `n × n` 矩阵方程：
  $$S_A(n) + M_A(n) + n\left[S_b(n) + M_b(n)\right] = \frac{8}{3} n^3 - \frac{3}{2} n^2 - \frac{1}{6} n \sim \frac{8}{3} n^3. \tag{7.24}$$

尽管在数学上完全一致，但在某些情况下基于方程 7.20 至 7.22 的算法仍会失败。具体而言，高斯消元的实现在每一步 `$k$` 都涉及将枢轴行 `$k$` 除以对角枢轴元素 `$a_{kk}^{(k-1)}$`。除法众所周知具有放大舍入误差的潜力，并且可能遇到实际上等于零的枢轴，在这种情况下，若无额外措施算法无法继续。此外，即使值非零，也可证明较大的枢轴会使变换后的矩阵 `$A^{(k)}$` 以及隐含的最终上三角矩阵 `$A^{(n)}$` 中的舍入误差更小。

为了抵消除以枢轴元素带来的不利副作用，一个选择是执行所谓的局部主元法。特别是在消元步骤 `$k$` 中，主元法意味着在列 `$k$` 上且在枢轴行及以下（`$l \ge k$`）定位最大元素 `$a_{lk}^{(k-1)}$`，并通过交换行 `$k$` 和 `$l$` 将该元素置于主对角线上（成为实际枢轴 `$a_{kk}^{(k-1)}$`）。然而，在计算行列式作为连续枢轴的乘积时，必须对行交换进行符号变化进行考虑。总的来说，主元法增加了高斯消元的计算成本，但确保了算法的稳定性和解的准确性。

在使用中更有效的主元算法有完全主元法，其中枢轴从尚未进行主元处理的矩阵 `$A^{(k-1)}$` 的所有列和行中选取。因此舍入误差进一步减小，但代价是更复杂的编码和额外的存储。完全主元法与 Gauss–Jordan 方法结合在下一节中进行了说明。

来自列表 7.1 的函数 `Gauss` 密切实现了上述描述的高斯消元算法，并且通过使用列上的局部主元法使例程操作稳定。数组 `a` 在输入时包含系数矩阵 `A` 的元素，并在消元过程中被破坏。为了在例程操作后仍可使用，矩阵 `A` 还应保存在备份数组中。数组 `b` 在输入时包含常数项 `B` 的元素，并在退出时返回解矩阵 `X` 的相应分量。系数矩阵的行列式由

## Listing 7.1 用高斯消去法带部分主元求解矩阵方程（Python 编码）

```
# =================================================================================

def Gauss(a, b, n, m):

# --------------------------------------------------------------------------------

# Solves matrix equation a x = b by Gaussian elimination with partial

# pivoting on columns.

# a  - coefficient matrix (n x n); destroyed on exit

# b  - matrix of constant terms (n x m); solution x on exit

# det - determinant of coefficient matrix (output).

# --------------------------------------------------------------------------------

det = 1e0

for k in range(1,n+1):                     # FORWARD ELIMINATION

    amax = 0e0                             # determine pivot row with

    for i in range(k,n+1):                 # max. element on column k

        if (amax < fabs(a[i][k])): amax = fabs(a[i][k]); imax = i

    if (amax == 0e0):

        print("Gauss: singular matrix !"); return 0e0

    if (imax != k):                        # interchange rows imax and k

        det = -det                         # to put pivot on diagonal

        for j in range(k,n+1): (a[imax][j],a[k][j]) = (a[k][j],a[imax][j])

        for j in range(1,m+1): (b[imax][j],b[k][j]) = (b[k][j],b[imax][j])

    det *= a[k][k]                         # multiply determinant with pivot

    t = 1e0/a[k][k]                        # divide pivot row by pivot

    for j in range(k+1,n+1): a[k][j] *= t

    for j in range(1,m+1): b[k][j] *= t

    for i in range(k+1,n+1):               # reduce non-pivot rows

        t = a[i][k]

        for j in range(k+1,n+1): a[i][j] -= a[k][j]*t

        for j in range(1,m+1): b[i][j] -= b[k][j]*t

for k in range(n-1,0,-1):                  # BACKWARD SUBSTITUTION

    for j in range(1,m+1):

        sum = b[k][j]

        for i in range(k+1,n+1): sum -= a[k][i]*b[i][j]

        b[k][j] = sum

return det
```

参数 `det`。 在消去过程中的某个阶段，如果无法识别出非零主元，则表明系数矩阵 `A` 是奇异的，例程会发出错误消息后退出。

一个简单的测试程序在 Listing 7.2 中说明了例程 `Gauss` 的用法。 按照第 2.5 节讨论的基本编程技术，在 Python 中我们将 2D 数组定义为行向量的集合。具体而言，Listing 7.2 中使用的特定语法允许数组 `a` 和 `b` 的最后一个可用元素分别为 `a[n][n]` 和 `b[n][m]`。 该程序的 C/C++ 对应版本作为补充材料提供（文件 `P07-Gauss.cpp`），借助 `memalloc.h` 包含文件中的函数 `Matrix` 来动态分配数组 `a` 和 `b`（见第 2 章）。 对于格式化的输出，程序调用 `matutil.py` 模块中定义的函数 `MatPrint`。

## Listing 7.2 用高斯消去法求解线性系统（Python 编码）

```
# Solves linear system by Gauss elimination
from linsys import *

from matutil import *

n = 4                                          # order of system
m = 1                                          # number of constant vectors
a = [[0]*(n+1) for i in range(n+1)]            # system matrix
b = [[0]*(m+1) for i in range(n+1)]            # constant terms
a[1][1] = 1; a[1][2] = 2; a[1][3] = 3; a[1][4] = 4; b[1][1] = 30
a[2][1] = 2; a[2][2] = 1; a[2][3] = 2; a[2][4] = 3; b[2][1] = 22
a[3][1] = 3; a[3][2] = 2; a[3][3] = 1; a[3][4] = 2; b[3][1] = 18
a[4][1] = 4; a[4][2] = 3; a[4][3] = 2; a[4][4] = 1; b[4][1] = 20

                                          # Solution: 1.0, 2.0, 3.0, 4.0; det = -20.0

print("A:")
MatPrint(a,n,n)

print("B:")
MatPrint(b,n,m)

det = Gauss(a,b,n,m)                          # solve system
print("det A =",det)
print("Solution:")
MatPrint(b,n,m)
```

## 7.3 高斯-约当消去法

高斯-约当方法可以被视为高斯消去法的变体，其中，不是通过初等行变换将系数矩阵 `A` 转化为上三角形式，而是在每一步中在整个矩阵内进行消去过程，最终将其转化为单位矩阵。因此，尽管前向消去阶段更为复杂，但向后回代被完全消除。此外，通过高效的编码和内存使用，高斯-约当消去法允许在求解矩阵方程的同时就地计算系数矩阵 `A⁻¹` 的逆。

让我们再次考虑在上一节中使用标准高斯消去法带回代求解的简单数值例子：

[ 3  4  5 ] [ x₁ ]   [ 10 ]
[ 4  2  3 ] [ x₂ ] = [  9 ]
[ -2 -3  1 ] [ x₃ ]   [  7 ]

在消去的第一步，未知数 `x₁` 要从除第一个方程之外的所有方程（第二和第三）中消去。为此，我们首先将第一个方程除以首项系数 3：

[ 1  4/3  5/3 ] [ x₁ ]   [ 10/3 ]
[ 4   2    3  ] [ x₂ ] = [   9  ]
[ -2 -3    1  ] [ x₃ ]   [   7  ]

然后我们用变换后的第一个方程乘以首项系数 4 从第二个方程中减去，并分别用首项系数 −2 乘以从第三个方程中减去：

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_200_0.png)

在第二步消去中，我们从除第二个方程之外的所有方程（第一个和第三个）中消去 `$x_2$`。因此，我们首先将第二个方程除以 `$x_2$` 的系数 `$-10/3$`，

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_200_1.png)

然后我们用变换后的第二个方程乘以 `$x_2$` 的系数 `$4/3$` 从第一个方程中减去，并分别用 `$−1/3$` 乘以从第三个方程中减去：

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_200_2.png)

在最后一步消去中，我们从除第二个方程之外的所有方程（第一个和第二个）中消去 `$x_3$`。为此，我们用 `$x_3$` 的系数分别乘以第三个方程，从第一个和第二个方程中减去：

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_200_3.png)

显然，没有必要进行向后回代，如标准高斯消去法那样，因为解的分量已经显式地出现在系数矩阵为单位矩阵的变换系统之中。

为了制定一般算法，我们注意到，在 *前向消去* 的第 `$k$` 步，未知数 `$x_k$` 从系统除第 `$k$` 个主元方程外的所有方程中消去，并且变换后的系统因此采取以下形式：

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_200_4.png)

主元行的元素根据以下公式更新

```
\begin{cases} a_{kk}^{(k)} = 1, \\ a_{kj}^{(k)} = a_{kj}^{(k-1)} / a_{kk}^{(k-1)}, \quad j = k+1,\dots,n, \\ b_{k}^{(k)} = b_{k}^{(k-1)} / a_{kk}^{(k-1)}, \end{cases} \tag{7.26}
```

非主元行的新元素由下式给出

```
\begin{cases} a_{ik}^{(k)} = 0, \\ a_{ij}^{(k)} = a_{ij}^{(k-1)} - a_{ik}^{(k-1)} a_{kj}^{(k)}, \quad j = k+1,\dots,n,\ i = 1,\dots,n,\ i \neq k \\ b_{i}^{(k)} = b_{i}^{(k-1)} - a_{ik}^{(k-1)} b_{k}^{(k)}. \end{cases} \tag{7.27}
```

可以看出，在消去步骤 k 时，只有主元列 k 右侧的列被修改，主元列本身变得与单位矩阵的相应列相同。对于常数项，它们在所有消去步骤中都会被改变。

在消去阶段结束时，矩阵方程获得了期望的结构，

```
\mathbf{E}_n \mathbf{x} = \mathbf{b}^{(n)}
```

其中 `E_n` 是阶数为 `n` 的单位矩阵。显然，不再需要向后回代阶段（类似于高斯消去法所具有的），因为上述形式允许直接识别解分量：

```
x_k = b_k^{(n)}, \quad k = 1,\dots,n. \tag{7.28}
```

系数矩阵行列式的即时计算与高斯消去法完全相同，并且基于事实 `det A^{(n)} = det E_n = 1`。 由于矩阵 `A^{(n)}` 是通过连续将主元行除以主元元素得到的，因此可得

```
\det \mathbf{A}^{(n)} = \frac{\det \mathbf{A}}{a_{11}^{(1)} a_{22}^{(1)} \cdots a_{nn}^{(n-1)}} = 1
```

由此得出：

```
\det \mathbf{A} = a_{11} a_{22}^{(1)} \cdots a_{nn}^{(n-1)}. \tag{7.29}
```

高斯-约当方法的递推关系可以直接推广到通过仅为常数项 `b_{kj}` 和解分量 `x_{kj}` 增加一个补充列索引来求解矩阵方程。在步骤 `k = 1, ..., n` 时，主元行 `k` 的关系为

```
\begin{cases} a_{kj}^{(k)} = a_{kj}^{(k-1)} / a_{kk}^{(k-1)}, \quad j = k+1,\dots,n, \\ b_{kj}^{(k)} = b_{kj}^{(k-1)} / a_{kk}^{(k-1)}, \quad j = 1,\dots,m, \end{cases} \tag{7.30}
```

而对于非主元行，它们为：

```
\begin{cases} a_{ij}^{(k)} = a_{ij}^{(k-1)} - a_{ik}^{(k-1)} a_{kj}^{(k)}, \quad i = 1,\dots,n, \ i \neq k, \ j = k+1,\dots,n, \\ b_{ij}^{(k)} = b_{ij}^{(k-1)} - a_{ik}^{(k-1)} b_{kj}^{(k)}, \quad i = 1,\dots,n, \ i \neq k, \ j = 1,\dots,m. \end{cases} \tag{7.31}
```
