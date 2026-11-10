
因此，当 $d=n$ 时，矩阵 $K_u$ 是方阵且可逆。因此，它定义了相似变换 $K_u^{-1}AK_u=C_{\varphi_\Delta}$，将 $A$ 化为一个友矩阵。现在，该变换保持行列式，因而也保持特征多项式。因此，特征多项式和最小多项式（在此情形下二者相同）的系数可以直接从友矩阵的最后一列读出。

```sage
A = matrix(GF(97), 4, 4,\
    [86,1,6,68,34,24,8,35,15,36,68,42,27,1,78,26])
e1 = identity_matrix(GF(97),4)[0]
U = matrix(A.transpose().maxspin(e1)).transpose()
F = U^-1*A*U
[0 0 0 83]
[1 0 0 77]
[0 1 0 20]
[0 0 1 10]
```

```sage
K.<x> = GF(97)[]
P = x^4 - sum([F[i,3]*x^i for i in range(4)]); P
x^4 + 87x^3 + 77x^2 + 20x + 14
```

```sage
P == A.charpoly()
True
```

在一般情形（$d\le n$）下，迭代向量 $u,\ldots,A^{d-1}u$ 构成线性子空间 $I$ 的一组基，该子空间在矩阵 $A$ 的作用下不变（即满足 $AI\subseteq I$）。该子空间也称为循环不变子空间，因为这些向量是通过将矩阵 $A$ 反复作用于前一个向量而循环得到的。该子空间的维数是 $u$ 的最小多项式的次数，因而以矩阵 $A$ 的最小多项式的次数为界。当维数达到最大时，该空间由习题 31 中构造的向量的 Krylov 迭代生成，我们将其记为 $u_1^*$。它称为第一不变子空间。令 $V$ 为该第一不变子空间的补子空间。模第一不变子空间进行计算，即只要两个向量之差属于第一不变子空间就认为它们相等，可以为该补子空间中的向量定义第二不变子空间，以及一个称为第二相似不变量的最小多项式。在这种情况下，我们有以下形式的关系：

$$A\begin{bmatrix}K_{u_1^*}&K_{u_2^*}\end{bmatrix}=\begin{bmatrix}K_{u_1^*}&K_{u_2^*}\end{bmatrix}\begin{bmatrix}C_{\varphi_1}&0\\0&C_{\varphi_2}\end{bmatrix},$$

其中 $\varphi_1,\varphi_2$ 是前两个相似不变量，$K_{u_1^*},K_{u_2^*}$ 是对应于由向量 $u_1^*$ 和 $u_2^*$ 生成的两个循环子空间的 Krylov 矩阵。

迭代地，可以构造矩阵 $K=[K_{u_1^*}\;\cdots\;K_{u_k^*}]$，它是方阵且可逆，并满足

$$K^{-1}AK=\begin{bmatrix}C_{\varphi_1}&&\\&\ddots&\\&&C_{\varphi_k}\end{bmatrix}.\tag{8.2}$$

由于每个 $u_i^*$ 都被 $\varphi_j$（$j \le i$）零化，因此对任意 $2 \le i \le k$，有 $\varphi_i \mid \varphi_{i-1}$。等价地，序列 $\varphi_i$ 按整除关系构成全序。可以证明，每个矩阵都存在唯一的相似不变量序列 $\varphi_1,\ldots,\varphi_k$。因此，与矩阵 $A$ 相似且揭示这些多项式的分块对角矩阵 $\mathrm{Diag}(C_{\varphi_1},\ldots,C_{\varphi_k})$ 是一种标准形，称为有理标准形或弗罗贝尼乌斯标准形。

**定理（弗罗贝尼乌斯标准形）。** 对域上的每个矩阵 $A$，存在唯一的矩阵 $F = \begin{bmatrix} C_{\varphi_1} & & \\ & \ddots & \\ & & C_{\varphi_k} \end{bmatrix}$，其中对所有 $i < k$ 有 $\varphi_{i+1} \mid \varphi_i$，且与 $A$ 相似。

式 (8.2) 表明，可以从变换矩阵 $K$ 读出各不变子空间的基。

**注记。**

$$\chi_A(x) = \det(x\mathrm{Id}-A) = \det(K)\det(x\mathrm{Id}-F)\det(K^{-1})$$
$$= \prod_{i=1}^k \det(x\mathrm{Id}-C_{\varphi_i}) = \prod_{i=1}^k \varphi_i(x).$$

因此，最小多项式 $\varphi_1$ 是特征多项式的因子，而特征多项式因此零化矩阵 $A$。

在 Sage 中，可以使用 `frobenius`$^1$ 方法计算系数在 $\mathbb{Z}$ 上的矩阵在 $\mathbb{Q}$ 上的弗罗贝尼乌斯标准形：

```sage
sage: A = matrix(ZZ,8,[[6,0,-2,4,0,0,0,-2],[14,-1,0,6,0,-1,-1,1],\
....: [2,2,0,1,0,0,1,0],[-12,0,5,-8,0,0,0,4],\
....: [0,4,0,0,0,0,4,0],[0,0,0,1,0,0,0,0],\
....: [-14,2,0,-6,0,2,2,-1],[-4,0,2,-4,0,0,4,0]])
sage: A.frobenius()
(
[0 0 0 4 0 0 0 0]
[1 0 0 4 0 0 0 0]
[0 1 0 1 0 0 0 0]
[0 0 1 0 0 0 0 0]
[0 0 0 0 0 0 0 4]
[0 0 0 0 1 0 0 0]
[0 0 0 0 0 1 1 0]
[0 0 0 0 0 0 0 2]
)
```

也可以通过传入 1 作为参数来获得相似不变量列表。为了获得相关不变子空间的信息，传入 2 作为参数，这将产生变换矩阵 $K$。它是整个空间的一组基，分解为不变子空间的直和。

```sage
sage: A.frobenius(1)
[x^4 - x^2 - 4x - 4, x^3 - x^2 - 4, x - 2]
```

```sage
sage: F, K = A.frobenius(2)
sage: K
[ 1 -15/56 17/224 15/56 -17/896 0 -15/112 17/64 ]
[ 0 229/224 -223/896 -23/224 -17/896 -17/896 29/448 13/128 ]
[ 0 -75/896 75/896 -75/896 -47/896 0 -17/896 23/128 ]
[ 0 17/896 29/896 15/896 0 -896/448 0 0 ]
[ 0 0 0 0 0 1 0 0 ]
[ 0 0 0 0 0 0 1 0 ]
[ 0 1 0 0 0 0 1 0 ]
[ 0 -4/21 -4/21 -10/21 0 0 -2/21 1 ]
```

```sage
sage: K^-1*F*K == A
True
```

这些结果隐含地假设矩阵 A 嵌入在分式域 ℚ 中。为了研究矩阵 A 在自由模 ℤ^n 上的作用，并明确该模相应的分解，可以使用 decomposition 方法。然而，对该方法的进一步解释将超出本书范围。

### 不变因子与相似不变量

有一个基本性质将相似不变量与不变因子联系起来，这在 8.2.1 节中已提及。

**定理。** 域 F 上矩阵 A 的相似不变量对应于其特征矩阵 xId - A 在环 F[x] 上的不变因子。

该定理的证明远远超出本书范围，我们仅在前面的例子中说明。

```sage
sage: S.<x> = QQ[]
sage: B = x*identity_matrix(8) - A
sage: B.elementary_divisors()
[1, 1, 1, 1, 1, x - 2, x^3 - x^2 - 4, x^4 - x^2 - 4*x - 4]
```

```sage
sage: A.frobenius(1)
[x^4 - x^2 - 4*x - 4, x^3 - x^2 - 4, x - 2]
```

### 特征值与特征向量

考虑将最小多项式分解为不可约因子，$\varphi_1 = \psi_1^{m_1}\cdots\psi_s^{m_s}$，则每个不变因子可以写成 $\varphi_i = \psi_1^{m_{i1}}\cdots\psi_s^{m_{is}}$，其中重数 $m_{i,j} \le m_j$。可以证明存在相似变换，将弗罗贝尼乌斯标准形中的每个友矩阵块 $C_{\varphi_i}$ 替换为对角块 $\mathrm{Diag}(C_{\psi_1^{m_{i1}}},\ldots,C_{\psi_s^{m_{is}}})$。这种弗罗贝尼乌斯标准形的变体称为中间形式，它仍由友矩阵块组成，但每个友矩阵块现在对应于某个不可约多项式的某次幂。

![](img/99840d73c45ee58b635c4eedc727fd9a_188_0.png)

当一个不可约因子 $\psi_i$ 的次数为 1 且重数为 1 时，其友矩阵块是主对角线上的 1×1 矩阵，因此对应于一个特征值。当最小多项式分裂且无平方因子时，矩阵可对角化。

特征值通过 `eigenvalues` 方法获得。`eigenvectors_right` 和 `eigenvectors_left` 方法分别列出每个特征值关联的右（分别左）特征向量以及该特征值的重数。最后，`eigenspaces_right` 和 `eigenspaces_left` 方法返回特征空间以及特征向量的一组基。

```sage
sage: A = matrix(GF(7),4,[5,5,4,3,0,3,3,4,0,1,5,4,6,0,6,3])
sage: A.eigenvalues()
[4, 1, 2, 2]
sage: A.eigenvectors_right()
[(4, [
(1, 5, 5, 1)
], 1), (1, [
(0, 1, 1, 4)
], 1), (2, [
(1, 3, 0, 1),
(0, 0, 1, 1)
], 2)]
sage: A.eigenspaces_right()
[
(4, Vector space of degree 4 and dimension 1 over Finite Field
of size 7
User basis matrix:
[1 5 5 1]),
(1, Vector space of degree 4 and dimension 1 over Finite Field
of size 7
User basis matrix:
[0 1 1 4]),
(2, Vector space of degree 4 and dimension 2 over Finite Field
of size 7
User basis matrix:
[1 3 0 1]
[0 0 1 1])
]
```

