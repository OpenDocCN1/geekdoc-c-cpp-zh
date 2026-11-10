

| 理想 | |
| --- | --- |
| 理想 \((p_1,p_2) \subset R\) | `R.ideal(p1, p2)` 或 `(p1, p2)*R` |
| 和、积、幂 | `I + J`、`I * J`、`I^k` |
| 交 \(I \cap J\) | `I.intersection(J)` |
| 商 \(I : J = \{p \mid pJ \subset I\}\) | `I.quotient(J)` |
| 根 \(\sqrt{I}\) | `I.radical()` |
| 模 \(I\) 约化 | `I.reduce(p)` 或 `p.mod(I)` |
| \(R \to R/I\) 的截面 | `p.lift(I)` |
| 商环 \(R/I\) | `R.quo(I)` 或 `R.quotient(I)` |
| 齐次化理想 | `J.homogenize()` |
| **一些预定义理想** | |
| 无关理想 \((x_1,\ldots,x_n)\) | `R.irrelevant_ideal()` |
| 雅可比理想 \((\partial p/\partial x_i)\) | `p.jacobian_ideal()` |
| 循环根（9.11） | `sage.rings.ideal.Cyclic(R)` |
| 域方程 \(x_i^q = x_i\) | `sage.rings.ideal.FieldIdeal(GF(q)['x1,x2'])` |

**表 9.3 — 理想。**

### 理想的根与解

理想与代数簇之间的主要对应关系在于希尔伯特零点定理，也称为*零点定理*。设 \(\overline{K}\) 为 \(K\) 的代数闭包。

**定理（零点定理）。** 设 \(p_1,\ldots,p_s \in K[\mathbf{x}]\)，并设 \(Z \subset \overline{K}^n\) 为 \(p_i\) 的公共零点集。多项式 \(p \in K[\mathbf{x}]\) 在 \(Z\) 上恒为零，当且仅当存在整数 \(k\) 使得 \(p^k \in \langle p_1,\ldots,p_s\rangle\)。

这一结果提供了一个代数判据，用于检验一个多项式系统是否有解。常数多项式 \(1\) 在 \(Z\) 上恒为零当且仅当 \(Z\) 为空，因此系统 \(p_1(x)=\cdots=p_s(x)=0\) 在 \(\overline{K}\) 中有解当且仅当理想 \(\langle p_1,\ldots,p_s\rangle\) 不包含 \(1\)。例如，以 \((0,0)\) 和 \((4,0)\) 为圆心、半径为 1 的两个圆有一个复交点：

```sage
sage: 1 in ideal(x^2+y^2-1, (x-4)^2+y^2-1)
False
```

然而，在添加条件 \(x = y\) 之后，该系统没有任何解。通过把方程的一个组合作为*证书*展示出来——若这些方程被满足，该组合就约化为 \(1 = 0\)——我们可以给出一个说明它不相容的简单证明。计算

```sage
sage: R(1).lift(ideal(x^2+y^2-1, (x-4)^2+y^2-1, x-y))
[-1/28*y + 1/14, 1/28*y + 1/14, -1/7*x + 1/7*y + 4/7]
```

得到关系式

\[
\frac{1}{28}\left((-y+2)(x^2+y^2-1)+(y+2)\left((x-4)^2+y^2-1\right)\right)
+(-4x+4y+16)(x-y)=1.
\]

用理想的语言来说，*零点定理*表明，在理想 \(J\) 所关联的簇 \(V_K(J)\) 上恒为零的多项式集合，就是该理想的*根*，定义为

\[
\sqrt{J}=\{p\in K[\mathbf{x}]\mid \exists k\in\mathbb{N}, p^k\in J\}.
\]

我们有

\[
V_K(\sqrt{J})=V_K(J)
\]

但直观地说，转到根会“忘记重数”。因此，理想 \(J_1\) 是它自身的根（我们说它是根理想），而关联到 \((S_2)\) 的理想 \(J_2\) 满足 \(J_2 \subsetneq \sqrt{J_2}\)。

```sage
sage: J1 = (x^2 + y^2 - 1, 16*x^2*y^2 - 1)*R
sage: J2 = (x^2 + y^2 - 1,  4*x^2*y^2 - 1)*R
sage: J1.radical() == J1
True
sage: J2.radical()
Ideal (2*y^2 - 1, 2*x^2 - 1) of Multivariate Polynomial
Ring in x, y over Rational Field
sage: 2*y^2 - 1 in J2
False
```

> **系统、理想与密码学**
>
> 一些特定的模块 `sage.rings.polynomial.multi_polynomial_sequence` 和 `sage.crypto.mq` 提供了处理多项式系统的工具，这些工具会考虑方程的特殊形式，而不仅仅是它们生成的理想。这对于处理大型结构化系统很有用，例如密码学中出现的系统。模块 `sage.crypto` 还定义了几个与经典密码学构造相关联的多项式系统。

### 理想上的运算

也可以直接对理想本身进行计算。让我们回顾两个理想之和的定义：

\[
I+J=\{p+q\mid p\in I \text{ and } q\in J\}=\langle I\cup J\rangle.
\]

它在几何上对应代数簇的交：

\[
V(I+J)=V(I)\cap V(J).
\]

因此，关联到 \((S_1)\) 的理想 \(J_1\) 是 \(C=\langle x^2+y^2-1\rangle\) 与 \(H=\langle 16x^2y^2-1\rangle\) 的和，它们分别定义圆和双曲线。在 Sage 中：

```sage
sage: C = ideal(x^2 + y^2 - 1); H = ideal(16*x^2*y^2 - 1)
sage: C + H == J1
True
```

这个相等性测试同样基于计算 Gröbner 基。

类似地，理想的交、积和商满足

| \(I \cap J = \{p \mid p \in I \text{ and } p \in J\}\) | \(V(I \cap J) = V(I) \cup V(J)\) |
| \(I \cdot J = \{pq \mid p \in I,\ q \in J\}\) | \(V(I \cdot J) = V(I) \cup V(J)\) |
| \(I : J = \{p \mid pJ \subset I\}\) | \(V(I : J) = V(I) \setminus V(J)\) |

这些运算按表 9.3 所示计算。这里记号 \(\overline{X}\) 表示 \(X\) 的 Zariski 闭包，即包含 \(X\) 的最小代数簇。例如，图 9.1a 中的曲线是来自 \(C \cap H\) 的多项式的零点集，而商 \((C \cap H) : (4xy-1)\) 对应于圆与两条双曲线之一的并：

```sage
sage: CH = C.intersection(H).quotient(ideal(4*x*y-1)); CH
Ideal (4*x^3*y + 4*x*y^3 + x^2 - 4*x*y + y^2 - 1) of
Multivariate Polynomial Ring in x, y over Rational Field
sage: CH.gen(0).factor()
(4*x*y + 1) * (x^2 + y^2 - 1)
```

然而，从 \(V(H)\) 中删去有限个点后得到的曲线不是代数子簇，因此：

```sage
sage: H.quotient(C) == H
True
```

### 维数

每个理想 \(J \subset K[x]\) 还关联一个*维数*，直观上它对应于代数闭域上簇 \(V(J)\) 的“分量”的最大“维数”⁵。例如我们有：

```sage
sage: [J.dimension() for J in [J1, J2, C, H, H+J2, J1+J2]]
[0, 0, 1, 1, 1, -1]
```

事实上，\(V(J_1)\) 和 \(V(J_2)\) 有有限个点，\(V(C)\) 和 \(V(H)\) 是曲线，\(V(H \cdot J_2)\) 是曲线与孤立点的并，而 \(V(J_1 + J_2)\) 为空。*零维系统*，即生成零维理想的系统，或等价地，在 \(K\) 的代数闭包上有有限个解的系统，将在本章剩余部分特别研究，因为它们是我们能够最显式地“求解”的系统。

⁵ 我们在 §9.3.3 给出一个更严格（但不一定更清晰）的定义。建议读者参阅本章开头给出的参考文献，以获得更好的解释。

## 9.2.4 消元

在方程组中，*消去*一个变量意味着找到该系统的“推论”，或者更确切地说“所有推论”，且这些推论与该变量无关。换句话说，我们希望找到任何解都满足、但不包含被消去变量的方程，这通常使它们更易于分析。

| 操作 | Sage 命令 |
| --- | --- |
| **一般多项式系统：消元、几何** | |
| 消元理想 \(J \cap K[z,t] \subseteq K[x,y,z,t]\) | `J.elimination_ideal(x,y)` |
| 结式 \(\operatorname{Res}_x(p,q)\) | `p.resultant(q,x)` |
| 维数 | `J.dimension()` |
| 亏格 | `J.genus()` |
| **零维系统** | |
| \(L \supseteq K\) 中的解 | `J.variety(L)` |
| 商在 \(K\) 上的维数 | `J.vector_space_dimension()` |
| 商基 | `J.normal_basis()` |
| 三角分解 | `J.triangular_decomposition()` |

**表 9.4 — 求解多项式系统。**

例如，我们可以从线性系统

\[
\begin{cases}
2x + y - 2z = 0\\
2x + 2y + z = 1
\end{cases}
\qquad (9.4)
\]

中消去 \(x\)，方法是第二式减去第一式。得到 \(y + 3z = 1\)，这说明 (9.4) 的任意解三元组 \((x,y,z)\) 都具有形式 \((x,1-3z,z)\)。然后我们可以验证，每个“部分解” \((1-3z,z)\) 都能提升为 (9.4) 的一个（唯一）解 \(\left(\frac{5z-1}{2},1-3z,z\right)\)。这说明高斯主元消去算法通过消元来求解线性系统，而不是例如使用克拉默公式。

### 消元理想

在多项式系统的语境中，方程 \(p_1(x)=\cdots=p_s(x)=0\) 的“推论”是理想 \(\langle p_1,\ldots,p_s\rangle\) 的元素。如果 \(J\) 是 \(K[x_1,\ldots,x_n]\) 的一个理想，我们称 \(J\) 的第 \(k\) 个*消元理想*为集合

\[
J_k = J \cap K[x_{k+1},\ldots,x_n] \tag{9.5}
\]

其中元素属于 \(J\)，且只包含最后 \(n-k\) 个变量。这是 \(K[x_{k+1},\ldots,x_n]\) 的一个理想。

在 Sage 中，方法 `elimination_ideal` 以要消去的变量列表为输入。注意：它返回的不是 \(J_k \subset K[x_{k+1},\ldots,x_n]\)，而是它在 \(K[x_1,\ldots,x_n]\) 中生成的理想 \(\langle J_k\rangle\)。对于线性系统 (9.4)，我们得到

```sage
sage: R.<x,y,z> = QQ[]
sage: J = ideal(2*x + y - 2*z, 2*x + 2*y + z - 1)
sage: J.elimination_ideal(x)
Ideal (y + 3*z - 1) of Multivariate Polynomial Ring in x, y, z
over Rational Field
sage: J.elimination_ideal(x,y)
Ideal (0) of Multivariate Polynomial Ring in x, y, z over Rational Field
```

从数学上，我们如下解释这些结果：我们有 \(J \cap \mathbb{Q}[y,z] = \langle y+3z-1\rangle \subseteq \mathbb{Q}[y,z]\) 以及 \(J \cap \mathbb{Q}[z] = \langle 0\rangle\)，即 \(\mathbb{Q}[z] \not\subseteq J\)。（事实上，理想 \(\langle 0\rangle\)

