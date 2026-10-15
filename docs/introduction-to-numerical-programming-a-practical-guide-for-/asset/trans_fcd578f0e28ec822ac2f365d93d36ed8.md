

# Listing 7.9 用 LU 分解求解线性系统的典型序列（Python 编码）

```
a = [[0]*(n+1) for i in range(n+1)]                # coefficient matrix
b = [0]*(n+1)                                      # vector of constant terms
ipivot = [0]*(n+1)                                 # vector of pivots
...
det = LUFactor(a,ipivot,n)
LUSystem(a,ipivot,b,n)
```

反映了分解过程中选主元算法所执行的行置换。具体而言，ipivot 的各分量只是连续主元行的索引，因此在使用前，常数项 b[i] 和 b[ipivot[i]] 会被互换。在求解第二个系统 U·x = y 时，数组 b 最初充当常数项向量 y 的角色，而在退出后，它表示最终解 x。

由 Listing 7.9 给出的求解线性方程组的一种典型代码序列采用 LU 分解。假定数组 a、b 和 ipivot 以偏移 1 分配并具有 n 个分量。对例程 LUFactor 的调用用存储在 a 中的系数矩阵替换为其 LU 分解，同时返回 ipivot 中的主元行列表。利用存储在 a 中的 LU 分解和存储在 b 中的常数项，对例程 LUSystem 的调用在 b 中返回系统的解。

例程 LUFactor 和 LUSystem 的配对对于计算矩阵的逆特别有用，这一点在 Listing 7.10 中包含的例程 MatInv 中得以实现。本质上，矩阵求逆首先借助 LUFactor 执行其 LU 分解，然后求解

# Listing 7.10 使用 LU 分解进行矩阵求逆（Python 编码）

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

一系列线性系统的解，其常数向量为单位矩阵的列，由 LUSystem 实现。连续的解恰好表示逆矩阵的列，为其临时存储，例程分配一个补充数组 ainv，最后将其复制到数组 a 中。这样，例程通过与原始矩阵最初传入的同一数组返回逆矩阵。

为测试由例程 MatInv 执行的矩阵求逆而设计的示例程序在 Listing 7.11 中给出。该程序生成一个随机矩阵，创建其副本，对副本进行求逆，并将原始数组与其逆相乘。由于舍入误差，检查的结果是单位矩阵的数值近似，其非对角元素的量级为 10^-15 – 10^-17。用于 2D 数组操作的调用辅助函数分别定义在文件 matutil.py 和 matutil.h 中。

# Listing 7.11 基于 LU 分解的矩阵求逆应用（Python 编码）

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

可以与高斯消去法类似地确定应用 LU 分解所涉及的 flop 计数：

- 系数矩阵 A 的 LU 分解（方程 7.42 和 7.43）：
  - 求和与减法：

```
S_A(n) = sum_{j=1}^{n} sum_{i=1}^{j} (1 + sum_{k=1}^{i-2} 1) + sum_{j=1}^{n} sum_{i=j+1}^{n} (1 + sum_{k=1}^{j-2} 1) = 1/3 n^3 - 1/2 n^2 + 1/6 n,
```

- 乘法与除法：

$$M_A(n) = \sum_{j=1}^{n} \sum_{i=1}^{j} \sum_{k=1}^{i-1} 1 + \sum_{j=1}^{n} \sum_{i=j+1}^{n} \left(1 + \sum_{k=1}^{j-1} 1\right) = \frac{1}{3} n^3 - \frac{1}{3} n.$$

- 常数项向量 **b** 的变换（方程 7.51 和 7.53）：
  - 求和与减法：

$$S_b(n) = \sum_{i=2}^{n} \left(1 + \sum_{j=1}^{i-2} 1\right) + \sum_{i=1}^{n-1} \left(1 + \sum_{j=i+1}^{n-1} 1\right) = n^2 - n,$$

  - 乘法与除法：

$$M_b(n) = \sum_{i=2}^{n} \sum_{j=1}^{i-1} 1 + 1 + \sum_{i=1}^{n-1} \left(1 + \sum_{j=i+1}^{n} 1\right) = n^2.$$

- 求解单个线性方程组：

$$S_A(n) + M_A(n) + S_b(n) + M_b(n) = \frac{2}{3} n^3 + \frac{3}{2} n^2 - \frac{7}{6} n \sim \frac{2}{3} n^3. \qquad (7.54)$$

- 系数矩阵 **A** 的求逆：

$$S_A(n) + M_A(n) + n\left(S_b(n) + M_b(n)\right) = \frac{8}{3} n^3 - \frac{3}{2} n^2 - \frac{1}{6} n \sim \frac{8}{3} n^3. \qquad (7.55)$$

可以立即注意到，基于 LU 分解的所有操作的成本与标准高斯消去法的成本完全一致，证明了两种方法是 *完全等价* 的。然而，由于可以存储前向消去的细节，如矩阵 **L** 和 **U** 所包含的那样，LU 分解在需要对在同一时间不可用的多个常数项向量重复求解系统时可能更可取。

## 7.5 三角矩阵的求逆

有时，即使很少直接来自实际问题的原始表述，也会出现求逆 *三角* 矩阵的必要性。两个这样的例子是对对称正定矩阵的广义特征值问题的求解及其求逆。在这两种情况下，标准过程都意味着矩阵的 Cholesky 分解（参见第 7.6 节），然后是所得下三角矩阵的求逆。

可以很容易证明，非奇异（可逆）三角矩阵的逆同样是三角矩阵。从下三角矩阵 **A** = $[a_{ij}]_{nn}$ 与

A⁻¹ = [a′ᵢⱼ]ₙₙ 的乘积等于单位矩阵的详细等式，

```
[ a₁₁ ⋱ 0 ; … aᵢⱼ … aᵢᵢ ; aₙ₁ … aₙₙ ] · [ a′₁₁ ⋱ 0 ; … a′ⱼⱼ ; … a′ⱼⱼ ; a′ₙ₁ … a′ₙₙ ] = Eₙ, (7.56)
```

通过识别相应的元素可以建立以下关系：

```
∑ₖ₌ⱼⁱ aᵢₖ a′ₖⱼ = δᵢⱼ,  i = j,…,n,  j = 1,2,…,n. (7.57)
```

对角方程（i = j 时）形式最简单，因为和简化为单项 aⱼⱼ a′ⱼⱼ = 1，并且允许对逆的对角元素进行表达：

```
a′ⱼⱼ = 1 / aⱼⱼ.
```

沿同一列 j 下降，对应于 i = j+1 的方程为 aⱼ₊₁,ⱼ a′ⱼⱼ + aⱼ₊₁,ⱼ₊₁ a′ⱼ₊₁,ⱼ = 0，并且能够将逆的同一列上的新元素表示为已计算的 a′ⱼⱼ 的函数：

```
a′ⱼ₊₁,ⱼ = − 1 / aⱼ₊₁,ⱼ₊₁ aⱼ₊₁,ⱼ a′ⱼⱼ.
```

将过程推广并从方程 7.57 的和的最后项中表达元素 a′ᵢⱼ，我们得到递推关系：

```
{ a′ⱼⱼ = 1 / aⱼⱼ,  j = 1,2,…,n,  a′ᵢⱼ = − 1 / aᵢᵢ ∑ₖ₌ⱼⁱ⁻¹ aᵢₖ a′ₖⱼ,  i = j+1,…,n. } (7.58)
```

按列扫描这些关系，并在每列 j 上首先计算对角元素 a′ⱼⱼ，然后计算位于行 i = j+1,…,n 下方的元素 a′ᵢⱼ，如方程 7.58 所示，右手边的条目 a′ₖⱼ 在需要时已计算，方程 7.58 在算法上是自洽的。

Listing 7.12 中的函数 MatTriInv 正好翻译了关系 7.58，并且被设计为通过与初始矩阵引入的同一数组 a 的下三角部分返回逆。该算法不需要选主元，对于任何可逆下三角矩阵都是完全稳定的。

