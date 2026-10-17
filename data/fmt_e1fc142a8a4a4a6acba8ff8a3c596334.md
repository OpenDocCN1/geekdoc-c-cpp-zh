
最后，解的分量可以用变换后常数项的最后一个值简单地标识：

$$
x_{kj}=b_{kj}^{(n)},\quad j=1,\dots,m,\ k=1,\dots,n.\tag{7.32}
$$

从这些关系可以看出，高斯法与高斯-约当法之间有两个显著差异。首先，在高斯法的第 $k$ 步（公式 7.20 至 7.22）中，只有位于主元行 $k$ 下方的非主元行被约化（$i=k+1,\dots,n$），未知数 $x_k$ 仅从这些行中被消去，而在高斯-约当法中，所有非主元行都被处理（$i=1,\dots,k-1,k+1,\dots,n$），未知数 $x_k$ 从所有这些行中被消去。第二大主要区别在于高斯-约当法中完全不存在回代。作为技术细节，如果使用同一个数组同时存放常数项 $\mathbf{B}=[b_{kj}]$ 和解分量 $\mathbf{X}=[x_{kj}]$，则赋值（7.32）实际上无需编码。

与其它方法相比，高斯-约当消去最有益的特性之一是其能够原地求逆系数矩阵 $\mathbf{A}$。该特性依赖于这样一个事实：由于变换后的系数矩阵 $\mathbf{A}^{(k)}$ 仅在列 $j=k+1,\dots,n$ 中包含相关信息，因此原则上只需有效地更新这些列。事实上，在消去过程中从左到右“扫描”数组时，主元列 $k$ 隐式地在其后留下单位矩阵的列，这些列无需实际存储。另一方面，求逆矩阵 $\mathbf{A}$ 本质上等价于求解矩阵方程 $\mathbf{A}\cdot\mathbf{X}=\mathbf{E}$，其中单位矩阵 $\mathbf{E}$ 形式上充当常数项矩阵。通过对矩阵 $\mathbf{A}$ 和 $\mathbf{E}$ 同时进行高斯-约当消去的初等变换，连续矩阵 $\mathbf{A}^{(k)}$ 的相关列数减少 1，而变换后单位矩阵 $\mathbf{E}^{(k)}$ 的相关列数增加 1。由于矩阵 $\mathbf{A}^{(k)}$ 和 $\mathbf{E}^{(k)}$ 的相关列总数保持不变，因此算法的实现原则上可以用单个数组同时存放两个矩阵。随着 $\mathbf{A}^{(k)}$ 相关列的约化，数组的列从左到右逐渐被 $\mathbf{E}^{(k)}$ 的新相关列所取代。技巧之一是初始单位矩阵的列可以在其变换前逐一在同一列中生成。最后，最初包含系数矩阵 $\mathbf{A}$ 的数组将包含其逆 $\mathbf{E}^{(n)}\equiv\mathbf{A}^{-1}$。因此，高斯-约当法可同时求解矩阵方程并求逆其系数矩阵。

高斯-约当消去伴随原地矩阵求逆的浮点运算次数可与标准高斯消去类似地确定：

- 将系数矩阵 $\mathbf{A}$ 变换为单位矩阵：
  - 求和与减法（公式 7.31）：

    $$
    S_A(n)=\sum_{k=1}^{n}\sum_{j=1}^{n}\left(\sum_{i=1}^{k-1}1+\sum_{i=k+1}^{n}1\right)=n^3-n^2,
    $$

  - 乘法与除法（公式 7.30 和 7.31）：

    $$
    M_A(n)=\sum_{k=1}^{n}\sum_{j=1}^{n}1+\sum_{k=1}^{n}\sum_{j=1}^{n}\left(\sum_{i=1}^{k-1}1+\sum_{i=k+1}^{n}1\right)=n^3.
    $$

- 变换单个常数项向量 $\mathbf{b}$（`m` = 1）：
  - 求和与减法（公式 7.31）：

    $$
    S_b(n)=\sum_{k=1}^{n}\left(\sum_{i=1}^{k-1}1+\sum_{i=k+1}^{n}1\right)=n^2-n,
    $$

  - 乘法与除法（公式 7.30 和 7.31）：

    $$
    M_b(n)=\sum_{k=1}^{n}1+\sum_{k=1}^{n}\left(\sum_{i=1}^{k-1}1+\sum_{i=k+1}^{n}1\right)=n^2.
    $$

- 求解单个线性方程组：

  $$
  S_A(n)+M_A(n)+S_b(n)+M_b(n)=2n^3+n^2-n \sim 2n^3. \tag{7.33}
  $$

- 求逆系数矩阵 $\mathbf{A}$：

  $$
  S_A(n)+M_A(n)=2n^3-n^2 \sim 2n^3. \tag{7.34}
  $$

通过比较伴随回代的高斯消去（公式 7.23 和 7.24）所需浮点运算次数与高斯-约当消去（公式 7.33 和 7.34）所需浮点运算次数可知，在求解线性方程组时，高斯消去更优，无论系统规模 $n$ 如何，其速度约为 3 倍（$N_{\mathrm{Gauss}} \sim \frac{2}{3}n^3$，$N_{\mathrm{Gauss\text{–}Jordan}} \sim 2n^3$），而在求逆矩阵时，高斯-约当法速度大约快 4/3 倍（$N_{\mathrm{Gauss}} \sim \frac{8}{3}n^3$，$N_{\mathrm{Gauss\text{–}Jordan}} \sim 2n^3$），并且只需一个数组（而非两个）即可存储系数矩阵及其逆。

第 7.3 节清单中的 `GaussJordan0` 例程突出了高斯法与高斯-约当法之间的技术差异，并在不求逆系数矩阵的情况下尽可能遵循函数 `Gauss` 的结构。为减少舍入误差并稳定算法，采用了相同的列部分主元技术。尽管由于没有回代，高斯-约当算法看起来更紧凑，但由于消去阶段更为复杂，其隐含的初等运算次数超过了高斯消去。

第 7.4 节清单中给出的函数 `GaussJordan1` 在例程 `GaussJordan0` 的基础上实现了上述原地求逆。它在退出时用其逆替换系数 `a` 的数组，并用矩阵方程的解替换常数项 `b` 的数组。

与高斯消去不同，高斯-约当算法在每一步消去中对所有列进行操作（$j=1,\dots,n$），因为系数矩阵和单位矩阵都必须经历初等变换序列。单位矩阵列的初始化（`a[k][k] = 1e0` 和 `a[i][k] = 0e0`）逐渐覆盖已变得冗余的变换后系数矩阵的列。

补充数组 `ipivot` 存储连续主元行的索引。事实上，考虑到主元意味着对初始单位矩阵的行进行重排，为获得系统矩阵的正确逆，需要按 `ipivot` 中存储的索引的逆序对数组 `a` 的列进行最后一次重排。

### 清单 7.3 带部分主元的高斯-约当消去（Python 编码）

```python
# =================================================================================

def GaussJordan0(a, b, n, m):

    # --------------------------------------------------------------------------------
    # Solves matrix equation a x = b by Gauss–Jordan elimination with partial
    # pivoting on columns.
    # a   - coefficient matrix (n x n); destroyed on exit
    # b   - matrix of constant terms (n x m); solution x on exit
    # det - determinant of coefficient matrix (output).
    # --------------------------------------------------------------------------------

    det = 1e0

    for k in range(1,n+1):                                 # FORWARD ELIMINATION
        amax = 0e0                                         # determine pivot row with
        for i in range(k,n+1):                             # max. element on column k
            if (amax < fabs(a[i][k])): amax = fabs(a[i][k]); imax = i

        if (amax == 0e0):
            print("GaussJordan0: singular matrix !"); return 0e0

        if (imax != k):                                    # interchange rows imax and k
            det = -det                                     # to put pivot on diagonal
            for j in range(k,n+1): (a[imax][j],a[k][j]) = (a[k][j],a[imax][j])
            for j in range(1,m+1): (b[imax][j],b[k][j]) = (b[k][j],b[imax][j])

        det *= a[k][k]                                     # multiply determinant with pivot

        t = 1e0/a[k][k]                                    # divide pivot row by pivot

        for j in range(k+1,n+1): a[k][j] *= t

        for j in range(1,m+1): b[k][j] *= t

        for i in range(1,n+1):                             # reduce non-pivot rows
            if (i != k):
                t = a[i][k]
                for j in range(1,n+1): a[i][j] -= a[k][j]*t
                for j in range(1,m+1): b[i][j] -= b[k][j]*t

    return det
```

实现舍入误差最大程度降低的主元方法是完全主元法，与迄今使用的部分主元法不同，它在尚未进行主元的全部行和列中搜索主元元素。清单 7.5 举例说明了带完全主元的高斯-约当消去的编码。

为获得正确的逆，程序结束时必须按它们在主元过程中被互换的逆序重新排列数组 `a` 的行和列。数组 `ipivot` 和 `jpivot` 分别存储主元元素的行和列索引的使用序列，数组 `npivot` 标记已用于主元的行，防止其被重复使用。由于其稳定性、准确性和通用性，在基于消去的矩阵方程求解器中，`GaussJordan` 是在需要同时求解系统和矩阵求逆的应用中首选的例程。

说明高斯-约当消去的应用，清单 7.6 在本质上与使用标准高斯消去的清单 7.2 类似。高斯-约当算法补充的能力——产生系数矩阵的逆——通过评估初始系数矩阵与函数返回的逆的乘积来检验，该初始系数矩阵存储在备份数组 `c` 中。

### Listing 7.4 Gauss–Jordan Elimination with Partial Pivoting and Matrix Inversion (Python Coding)

```python
#===============================================================================

def GaussJordan1(a, b, n, m):

    #-------------------------------------------------------------------------------
    # Solves matrix equation a x = b by Gauss-Jordan elimination with partial
    # pivoting on columns.
    # a  - coefficient matrix (n x n); a^(-1) on exit
    # b  - matrix of constant terms (n x m); solution x on exit
    # det - determinant of coefficient matrix (output).
    #-------------------------------------------------------------------------------
    ipivot = [0]*(n+1)                                            # stores pivot rows

    det = 1e0

    for k in range(1,n+1):                                        # FORWARD ELIMINATION
        amax = 0e0                                                # determine pivot row with
        for i in range(k,n+1):                                    # max. element on column k
            if (amax < fabs(a[i][k])): amax = fabs(a[i][k]); imax = i

        if (amax == 0e0):
            print("GaussJordan1: singular matrix !"); return 0e0

        ipivot[k] = imax                                          # store pivot row index

        if (imax != k):                                           # interchange rows imax and k
            det = -det                                            # to put pivot on diagonal
            for j in range(1,n+1): (a[imax][j],a[k][j]) = (a[k][j],a[imax][j])
            for j in range(1,m+1): (b[imax][j],b[k][j]) = (b[k][j],b[imax][j])

        det *= a[k][k]                                            # multiply determinant with pivot

        t = 1e0/a[k][k]                                           # divide pivot row by pivot

        a[k][k] = 1e0                                             # diagonal element of unit matrix

        for j in range(1,n+1): a[k][j] *= t

        for j in range(1,m+1): b[k][j] *= t

        for i in range(1,n+1):                                    # reduce non-pivot rows
            if (i != k):
                t = a[i][k]
                a[i][k] = 0e0                                     # non-diagonal element of unit matrix
                for j in range(1,n+1): a[i][j] -= a[k][j]*t
                for j in range(1,m+1): b[i][j] -= b[k][j]*t

    for k in range(n,0,-1):                                       # rearrange columns of inverse
        imax = ipivot[k]
        if (imax != k):
            for i in range(1,n+1): (a[i][imax],a[i][k]) = (a[i][k],a[i][imax])

    return det
```
