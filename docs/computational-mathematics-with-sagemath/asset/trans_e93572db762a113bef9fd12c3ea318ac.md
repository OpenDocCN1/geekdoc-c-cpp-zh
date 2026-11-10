
通常的 Python 约定。行索引和列索引 $i$ 和 $j$ 可以是整数（用于访问某个系数），也可以是形如 \(1:3\) 的区间（回忆：Python 中的索引从 0 开始，区间总是下界包含、上界不包含）。不带边界的区间“:”对应于所考虑维度中所有可能的索引。记号 `a:b:k` 按步长 $k$ 枚举 $a$ 到 $b-1$ 之间的所有索引。最后，负索引同样有效，允许从索引空间的末尾开始迭代。因此，`A[-2,:]` 指的是矩阵 `A` 的倒数第二行。这些访问子矩阵的模式既可用于读取操作，也可用于写入操作。例如，可以如下修改某一列：

```python
sage: A = matrix(3,3,range(9))
sage: A[:,1] = vector([1,1,1]); A
( 0  1  2 )
( 3  1  5 )
( 6  1  8 )
```

步长 $k$ 也可以为负，以便按递减顺序迭代。

```python
sage: A[::-1], A[:,::-1], A[:,2:-1]
( ( 6  1  8 )   ( 2  1  0 )   ( 2 ) )
( ( 3  1  5 ) , ( 5  1  3 ) , ( 8 ) )
( ( 0  1  2 )   ( 8  1  6 )       )
```

**提取子矩阵。** 为了从一组行或列索引中提取子矩阵（这些索引不一定连续），可以使用方法 `A.matrix_from_rows`、`A.matrix_from_columns`，或者在更一般的场景中使用方法 `A.matrix_from_rows_and_columns`。

```python
sage: A = matrix(ZZ,4,4,range(16)); A
(  0   1   2   3 )
(  4   5   6   7 )
(  8   9  10  11 )
( 12  13  14  15 )
```

```python
sage: A.matrix_from_rows_and_columns([0,2,3], [1,2])
(  1   2 )
(  9  10 )
( 13  14 )
```

另外，当行和列索引连续时，也可以使用方法 `A.submatrix(i,j,m,n)`，它形成维度为 $m \times n$ 的子矩阵，其左上角系数位于 `A` 中的位置 \((i,j)\)。

| 基本操作 | |
| --- | --- |
| 转置、共轭 | `A.transpose(), A.conjugate()` |
| 标量乘法 | `a*A` |
| 和、积、k 次幂、逆 | `A + B, A * B, A^k, A^-1 or ~A` |

*表 8.2——基本操作与矩阵运算*

**嵌入与扩张。** 矩阵空间的 `base_extend` 方法可以将一个矩阵空间嵌入到另一个维度相同、但基环为原基环的扩张的矩阵空间。然而，此操作仅对域扩张或环扩张有效。若要在环态射（如果存在）下改变矩阵空间的环，则应改用 `change_ring` 方法。

```text
sage: MS = MatrixSpace(GF(3),2,3)
sage: MS.base_extend(GF(9,'x'))
Full MatrixSpace of 2 by 3 dense matrices over Finite Field
in x of size 3^2
sage: MS = MatrixSpace(ZZ,2,3)
sage: MS.change_ring(GF(3))
Full MatrixSpace of 2 by 3 dense matrices over Finite Field of size 3
```

**可变性与缓存。** 默认情况下，矩阵对象是可变的，这意味着在构造之后可以修改其成员（即系数）。为了保护矩阵不被修改，可以使用函数 `A.set_immutable()` 使其不可变。之后仍然可以使用函数 `copy(A)` 创建此矩阵的可变副本。注意，对计算结果（如秩、行列式等）的缓存机制始终处于激活状态，与可变性状态无关。

### 8.1.4 矩阵的基本运算

矩阵的算术运算使用通常的运算符 `+,-,*,^`。矩阵 `A` 的逆可以通过 `A^-1` 或 `~A` 等价地得到。对于标量 `a` 和矩阵 `A`，运算 `a*A` 对应矩阵空间中的标量乘法。对于任何其他以标量 `a` 代替矩阵的运算（例如 `a+A`），如果维度允许且 `a != 0`，则该标量会被解释为相应的标量矩阵 `aI_n`。两个矩阵的逐元素乘积通过 `elementwise_product` 方法实现。

## 8.2 矩阵计算

在线性代数中，矩阵通常用于表示向量族、线性方程组、线性变换或向量子空间。因此，计算诸如向量族的秩、线性方程组的解、线性变换的特征空间或子空间的维数等性质，最终都归结为对相应矩阵的运算，这些运算将揭示相应的性质。

这些变换通常对应于基变换，从矩阵的角度来看，它们转化为等价变换：$B = PAQ^{-1}$，其中 $P$ 和 $Q$ 是可逆矩阵。如果两个矩阵之间存在这样的变换，则称它们是等价的。然后可以针对这一关系形成等价类，并定义以唯一方式刻画每个等价类的标准形。下面，我们将从这类变换的两种实例出发，介绍 Sage 中的大部分矩阵计算：

-   左等价变换，形式为 $B = UA$，揭示向量族的特征性质，例如它们的秩（线性无关向量的个数）、行列式（由向量族构成的平行六面体的体积）、秩轮廓（构成该向量族张成空间的一组基的最初一组向量）……高斯消元是这些变换的关键工具，而简化阶梯形是相应的标准形（在 Z 上则为 Hermite 标准形）。

-   相似变换，形式为 $B = UAU^{-1}$，揭示表示自同态的矩阵的特征性质，如特征值、特征空间、最小多项式与特征多项式……根据底层域的不同，Jordan 标准形或 Frobenius 标准形将是这些变换的标准形。

Gram-Schmidt 正交化过程则产生了另一种基于左等价变换的分解，它将一个矩阵变为一组正交向量。

### 8.2.1 高斯消元与阶梯形

**高斯消元与左等价。** 高斯消元是计算线性代数中的基础运算，因为它提供了一种矩阵表示，即三角因子的乘积，它既更适合计算（例如求解线性方程组），又能揭示诸如秩、秩轮廓、行列式等基本性质。用于定义高斯消元的基本运算是初等行运算：

-   交换两行：$L_i \leftrightarrow L_j$，
-   将一行的倍数加到另一行：$L_i \leftarrow L_i + sL_j$。

从矩阵的角度来看，这些变换分别对应左乘一个置换矩阵 $T_{i,j}$ 和一个切变矩阵 $C_{i,j,s}$，它们的定义如下：

$$
T_{i,j} =
\begin{bmatrix}
1 & & & & & \\
& \ddots & & & & \\
& & 0 & 1 & & \\
& & 1 & 0 & & \\
& & & & \ddots & \\
& & & & & 1
\end{bmatrix},
\qquad
C_{i,j,s} =
\begin{bmatrix}
1 & & & & & \\
& \ddots & & & & \\
& & 1 & & s & \\
& & & \ddots & & \\
& & & & 1 & \\
& & & & & \ddots
\end{bmatrix}
$$

这些矩阵的行列式均为 $1$ 或 $-1$。因此，左乘这些矩阵的任意乘积是一种保持体积的基变换，即保持行列式（至多相差一个符号）。在 Sage 中，切变通过 `add_multiple_of_row(i,j,s)` 方法实现，换位通过 `swap_rows(i,j)` 方法实现。

| 操作 | Sage 命令 |
|---|---|
| **高斯消元及其应用** | |
| 行切变 | `add_multiple_of_row(i,j,s)` |
| 列切变 | `add_multiple_of_column(i,j,s)` |
| 行、列换位 | `swap_rows(i,j), swap_columns(j,i)` |
| 简化行阶梯形，不可变 | `echelon_form` |
| 简化行阶梯形，就地 | `echelonize` |
| 史密斯标准形 | `elementary_divisors` |
| 不变因子 | `smith_form` |
| 行列式、秩 | `det, rank` |
| k 阶子式 | `minors(k)` |
| 列、行秩轮廓 | `pivot, pivot_rows` |
| 左侧系统求解 (Ax = b) | `b/A or A.solve_left(b)` |
| 右侧系统求解 (Ax = b) | `A\b or A.solve_right(b)` |
| 像空间 | `image` |
| 左核 | `kernel or left_kernel` |
| 右核 | `right_kernel` |
| 基环中的核 | `integer_kernel` |
| **谱分解** | |
| 最小多项式 | `minimal_polynomial or minpoly` |
| 特征多项式 | `characteristic_polynomial or charpoly` |
| 左端 Krylov 迭代 | `maxspin(v)` |
| 特征值 | `eigenvalues` |
| 左、右特征向量 | `eigenvectors_left, eigenvectors_right` |
| 左、右特征空间 | `eigenspaces_left, eigenspaces_right` |
| 对角化 | `eigenmatrix_left, eigenmatrix_right` |
| Jordan 块 $J_{n,k}$ | `jordan_block(n,k)` |

*表 8.3——矩阵计算*
