
### 8.2.2 线性方程组求解、像与零空间基

**线性方程组求解。** 线性方程组可以用矩阵 $A$ 以及右端向量或左端向量 $b$ 表示，分别对应形如 $Ax = b$ 或 $x^T A = b^T$ 的方程组。方法 `solve_right` 和 `solve_left` 可求解这些方程组。也可以使用运算符 `A\b` 和 `b/A`。当方程组由环上的矩阵给出时，求解会系统地在环的分式域上进行（例如，对于环 $\mathbb{Z}$ 使用 $\mathbb{Q}$，对于 $K[X]$ 使用 $K(X)$）。稍后我们将看到如何在基环上求解方程组。方程组等式中的右端可以是向量或矩阵（后者对应于用同一矩阵求解多个方程组）。

方程组的矩阵可以是矩形，方程组可能有唯一解、无解或无穷多解。在后一种情况下，求解方法返回其中一个解，并将方程组中线性相关列对应的系数置零。

```sage
sage: R.<x> = PolynomialRing(GF(5),'x')
sage: A = random_matrix(R,2,3); A
[ 3*x^2 + x        x^2 + 2*x         2*x^2 + 2]
[ x^2 + x + 2   2*x^2 + 4*x + 3    x^2 + 4*x + 3]
```

```sage
sage: b = random_matrix(R,2,1); b
[  4*x^2 + 1]
[  3*x^2 + 2*x]
```

```sage
sage: A.solve_right(b)
[ (4*x^4 + 2*x + 4)/(3*x^2 + 2*x + 2)]
[ (3*x^3 + 3*x + 3)/(3*x^2 + 2*x + 2)]
[ (x^3 + 4*x^2 + 4*x)/(3*x^2 + 2*x + 2)]
[                                     0]
```

```sage
sage: A.solve_right(b) == A\b
True
```

**像与核。** 一个 $m \times n$ 矩阵 $A$ 可视为线性变换 $\Phi$，它分别定义了 $K^m$ 和 $K^n$ 的两个子空间，即 $\Phi$ 的像与核。

像是由 $A$ 的列向量的线性组合构成的所有 $K^m$ 中向量组成的集合。它由方法 `image` 给出，返回一个向量空间，其基为简化行阶梯形。

核是由所有满足 $Ax = 0$ 的向量 $x$ 构成的 $K^n$ 的子空间。该子空间的一组基有助于描述具有无穷多解的欠定线性方程组的解集：如果 $\bar{x}$ 是 $Ax = b$ 的一个解，$V$ 是 $A$ 的核，那么 $\bar{x} + V$ 就是该方程组的全部解集。该集合由方法 `right_kernel` 计算，返回一个向量空间，其基为简化行阶梯形。左核类似地定义为满足 $x^T A = 0$ 的向量 $x \in K^m$ 的集合，它也是 $A$ 的转置矩阵的右核。它由方法 `left_kernel` 返回。按照约定，方法 `kernel` 返回左核，并且基以行向量矩阵的形式给出。

```sage
sage: a = matrix(QQ,3,5,[2,2,-1,-2,-1,2,-1,2,-1,1,2,-1/2,2,-2,-1,2,-1,2,-1/2])
sage: a.image()
Vector space of degree 5 and dimension 3 over Rational Field
Basis matrix:
[  1   0   0   1/4  -11/32]
[  0   1   0   -1   -1/8]
[  0   0   1   1/2   1/16]
sage: a.right_kernel()
Vector space of degree 5 and dimension 2 over Rational Field
Basis matrix:
[  1   0    0  -1/3   8/3]
[  0   1  -1/2  11/12  2/3]
```

核的概念自然推广到系数不再属于域而属于环的情形；此时它具有自由模的结构。特别地，对于定义在整环的分式域上的矩阵，其在基环中的核可由方法 `integer_kernel` 得到。例如，一个定义在 $\mathbb{Z}$ 上的矩阵，嵌入到域 $\mathbb{Q}$ 上的向量空间后，其核既可以是 $\mathbb{Q}^m$ 的 $\mathbb{Q}$-向量子空间，也可以是 $\mathbb{Z}^m$ 的自由 $\mathbb{Z}$-子模。

```sage
sage: a = matrix(ZZ,5,3,[1,1,122,-1,-2,1,-188,2,1,1,-10,1,-1,-1,-1])
sage: a.kernel()
Free module of degree 5 and rank 2 over Integer Ring
Echelon basis matrix:
[   1   979  -11  -279   811]
[   0  2079  -22  -569  1488]
sage: b = a.base_extend(QQ)
sage: b.kernel()
Vector space of degree 5 and dimension 2 over Rational Field
Basis matrix:
[   1       0  -121/189 -2090/189   6949/63]
[   0       1    -2/189  -569/2079   496/693]
sage: b.integer_kernel()
Free module of degree 5 and rank 2 over Integer Ring
Echelon basis matrix:
[   1   979  -11  -279   811]
[   0  2079  -22  -569  1488]
```

### 8.2.3 特征值、Jordan 标准形与相似变换

方阵 $A$ 是线性算子（即自同态）在给定基下的表示。任何基变换都对应于形如 $B = U^{-1}AU$ 的相似变换。矩阵 $B$ 表示该线性算子在新基下的表示，此时矩阵 $A$ 与 $B$ 相似。线性算子与表示基无关的性质，因而可通过研究矩阵的相似不变量来揭示，即其在相似变换下保持不变的性质。

在这些不变量中，最基本的是秩和行列式。事实上，由于矩阵 $U$ 和 $U^{-1}$ 可逆，$U^{-1}AU$ 的秩就是 $A$ 的秩。此外，$\det(U^{-1}AU) = \det(U^{-1})\det(A)\det(U) = \det(U^{-1}U)\det(A) = \det(A)$。类似地，矩阵 $A$ 的特征多项式定义为 $\chi_A(x) = \det(x\operatorname{Id} - A)$，它在相似变换下也不变：

$$\det(x\operatorname{Id} - U^{-1}AU) = \det(U^{-1}(x\operatorname{Id} - A)U) = \det(x\operatorname{Id} - A).$$

因此，矩阵的特征值——定义为其特征多项式在其分裂域中的根——也是相似不变量。

按定义，若存在非零向量 $u$ 使得 $Au = \lambda u$，则标量 $\lambda$ 是矩阵 $A$ 的特征值。与特征值 $\lambda$ 相关联的特征空间是所有满足 $Au = \lambda u$ 的向量 $u$ 的集合。它是由 $E_\lambda = \operatorname{Ker}(\lambda \operatorname{Id} - A)$ 定义的线性子空间。

特征值与特征多项式的根一致：

$$\det(\lambda \operatorname{Id} - A) = 0 \iff \dim(\operatorname{Ker}(\lambda \operatorname{Id} - A)) \ge 1 \iff \exists u \ne 0, \lambda u - Au = 0.$$

这两种观点分别对应于特征值的代数方法和几何方法。几何观点比代数观点更精确地考察线性算子 $A$ 在环境空间中对向量的作用。特别地，它们在特征值重数的概念上有所不同：代数重数是特征多项式中根的重数，而几何重数是与该特征值相关联的特征空间的维数。当矩阵可对角化时，这些概念等价；否则，几何重数小于或等于代数重数。

几何观点能给出矩阵结构的更精细细节。它还有助于设计计算特征值、特征向量以及特征多项式和极小多项式的高效算法。

#### 循环不变子空间与 Frobenius 标准形

设 $A$ 是域 $K$ 上的 $n \times n$ 矩阵，$u \in K^n$ 是一个向量。向量 $u, Au, A^2u, \ldots, A^n u$ 称为 Krylov 序列，它们是线性相关的（因为这是 $n$ 维空间中的 $n+1$ 个向量）。设 $d$ 是使得 $A^d u$ 与其前驱 $u, Au, \ldots, A^{d-1}u$ 线性相关的第一个索引。我们可以将该线性相关关系写成

$$A^d u = \sum_{i=0}^{d-1} \alpha_i A^i u.$$

因此，满足关系 $\varphi_{A,u}(A)u = 0$ 的多项式 $\varphi_{A,u}(x) = x^d - \sum_{i=0}^{d-1} \alpha_i x^i$ 是零化该 Krylov 序列的首一多项式，且次数最小。它称为向量 $u$（关于矩阵 $A$）的*极小多项式*。$u$ 的所有零化多项式构成 $K[X]$ 的一个理想，由 $\varphi_{A,u}$ 生成。

矩阵 $A$ 的极小多项式定义为零化矩阵 $A$ 的次数最小的首一多项式：$\varphi_A(A)=0$。特别地，在该方程右乘向量 $u$ 表明 $\varphi_A$ 零化 $u$ 的 Krylov 序列。因此它必然是 $u$ 的极小多项式的倍数。此外，可以证明（见练习31）总存在向量 $\bar u$ 使得

$$\varphi_{A,\bar u}=\varphi_A. \tag{8.1}$$

当随机选取向量 $u$ 时，它满足方程 (8.1) 的概率随域的大小而增加（可以证明该概率至少为 $1-\frac{n}{|K|}$）。

**练习31.** 我们将证明总存在一个向量 $\bar u$，其极小多项式与矩阵的极小多项式相同。

- 1. 设 $(e_1,\ldots,e_n)$ 是向量空间的一组基。证明 $\varphi_A$ 等于所有 $\varphi_{A,e_i}$（$1\le i\le n$）的最小公倍数。
- 2. 在 $\varphi_A$ 是某个不可约多项式的幂的情形下，证明存在索引 $i_0$ 使得 $\varphi_A=\varphi_{A,e_{i_0}}$。
- 3. 证明如果向量 $e_i$ 和 $e_j$ 的极小多项式 $\varphi_i=\varphi_{A,e_i}$ 与 $\varphi_j=\varphi_{A,e_j}$ 互素，那么 $\varphi_{A,e_i+e_j}=\varphi_i\varphi_j$。
- 4. 证明如果 $\varphi_A=P_1P_2$，其中 $P_1$ 和 $P_2$ 互素，那么存在两个非零向量 $x_1\ne 0$ 和 $x_2\ne 0$，使得对于 $i=1,2$，$P_i$ 是 $x_i$ 的极小多项式。
- 5. 利用 $\varphi_A$ 分解为不可约因式 $\varphi_A=\varphi_1^{m_1}\ldots\varphi_k^{m_k}$ 得出结论。
- 6. 示例：设 $A=\begin{bmatrix}0&0&3&0&0\\1&0&6&0&0\\0&1&5&0&0\\0&0&1&5&0\\0&0&0&1&5\end{bmatrix}$ 是 GF(7) 上的矩阵。计算 $A$ 的极小多项式的次数、标准基向量 $u=e_1$ 和 $v=e_4$ 的极小多项式的次数，以及向量 $u+v$ 的极小多项式的次数。可以对矩阵 $A$ 的转置使用方法 `maxspin(u)`，它返回向量 $u$ 的线性无关 Krylov 迭代的最大序列。

设 $P=x^k+\sum_{i=0}^{k-1}\alpha_i x^i$ 是次数为 $k$ 的首一多项式。与多项式 $P$ 相关联的友矩阵是 $k\times k$ 矩阵

$$C_P=\begin{bmatrix}0& & & -\alpha_0\\1& & & -\alpha_1\\ &\ddots& &\vdots\\ & &1&-\alpha_{k-1}\end{bmatrix}.$$

该矩阵具有性质：$P$ 等于其极小多项式，也等于其特征多项式。

**命题.** 设 $K_u$ 是由向量 $u$ 的前 $d$ 个 Krylov 迭代构成的矩阵。那么

$$AK_u=K_uC_{\varphi_{A,u}}.$$

