  
**商代数。** 与一般理想相比，零维理想的商更容易处理，因为商代数中的计算可以归结为有限维线性代数。

如果 $J \subset K[x]$ 是一个零维理想，那么商代数作为 $K$-向量空间的维数 $\dim_K K[x]/J$ 限定了 $V(J)$ 的点的个数。（实际上，对于任何 $u \in V(J)$，存在一个系数在 $K$ 中的多项式，它在 $u$ 处等于 1，而在 $V(J)$ 的任何其他点处等于 0。这样的两个多项式模 $J$ 不可能等价。）我们可以将这个维数视为该系统在 $K$ 的代数闭包上的“带重数”的解的个数。例如，我们已经注意到 §9.2.3 中引入的系统 $(S_2)$ 的四个解分别是两条曲线的“二重”交点。这解释了以下结果：

```sage
sage: len(J2.variety(QQbar)), J2.vector_space_dimension()
(4, 8)
```

正规基方法计算一组单项式，它们在 $K[x]/J$ 上的投影构成一组基：

```sage
sage: J2.normal_basis()
[x*y^3, y^3, x*x^2*y^2, x^2*y, x*y, y, x, 1]
```

返回的基取决于构造多项式环时所选的单项式序；我们将在 §9.3.3 中更精确地描述它。

**练习 37.** 设 $J$ 是 $\mathbb{Q}[x,y]$ 的一个零维理想。设 $\chi_x$ 为线性变换的特征多项式

$$\begin{aligned}m_x :\quad \mathbb{Q}[x,y]/J &\longrightarrow \mathbb{Q}[x,y]/J \\ p+J &\longmapsto xp+J.\end{aligned}$$

在 $J=J_2=\langle x^2+y^2-1,\,4x^2y^2-1\rangle$ 的情形下计算 $\chi_x$。证明 $\chi_x$ 的每一个根都是簇 $V_{\mathbb{C}}(J)$ 中某一点的横坐标。

## 9.3 Gröbner 基

到目前为止，我们一直将 Sage 提供的用于代数消元和多项式系统求解的函数视为黑盒。本节介绍一些底层的数学和算法工具。其目的既在于能够直接调用这些工具，也在于明智地使用前面看到的高级函数。

Sage 用于理想计算和消元的方法基于 Gröbner 基的概念。我们可以将 Gröbner 基视为 $K[x]$ 的理想用主生成元表示的多元推广。本节的主要问题是为来自 $K[x]$ 的商代数的元素定义并计算一个正规形式。我们的观点仍然是用户视角：我们定义 Gröbner 基，展示如何用 Sage 获得它们以及它们如何有用，但不讨论计算它们的算法。

**主要单项式序，以 Q[x, y, z] 为例**

|  |  |
|---|---|
| lex | $x^\alpha \prec x^\beta \Leftrightarrow \alpha_1 < \beta_1$ 或 $(\alpha_1 = \beta_1$ 且 $\alpha_2 < \beta_2)$ 或 ...<br>或 $(\alpha_1 = \beta_1,\ldots,\alpha_{n-1} = \beta_{n-1}$ 且 $\alpha_n < \beta_n)$<br>$x^3 > x^2 y > x^2 z > x^2 > xy^2 > xyz > xy > xz^2 > xz > x > y^3 > y^2 z > yz^2 > yz > y > z^3 > z^2 > z > 1$ |
| invlex | $x^\alpha \prec x^\beta \Leftrightarrow \alpha_n < \beta_n$ 或 $(\alpha_n = \beta_n$ 且 $\alpha_{n-1} < \beta_{n-1})$ 或 ...<br>或 $(\alpha_n = \beta_n,\ldots,\alpha_2 = \beta_2$ 且 $\alpha_1 < \beta_1)$<br>$z^3 > yz^2 > xz^2 > y^2 z > yz > xyz > z^2 > xz > z > y^3 > y^2 > xy^2 > y > x^2 y > x^2 > x > 1$ |
| deglex | $x^\alpha \prec x^\beta \Leftrightarrow |\alpha| < |\beta|$ 或 $(|\alpha| = |\beta|$ 且 $x^\alpha \prec_{lex} x^\beta)$<br>$x^3 > x^2 y > x^2 z > xy^2 > xyz > xz^2 > y^3 > y^2 z > yz^2 > z^3 > x^2 > xy > xz > y^2 > yz > z^2 > x > y > z > 1$ |
| degrevlex | $x^\alpha \prec x^\beta \Leftrightarrow |\alpha| < |\beta|$ 或 $(|\alpha| = |\beta|$ 且 $x^\alpha \succ_{invlex} x^\beta)$<br>$x^3 > x^2 y > xy^2 > y^3 > x^2 z > xyz > y^2 z > xz^2 > yz^2 > z^3 > x^2 > xy > y^2 > xz > yz > z^2 > x > y > z > 1$ |

**构造单项式序**

|  |  |
|---|---|
| 表示 n 个变量上预定义序的对象 | TermOrder('nom', n) |
| 矩阵序：$x^\alpha &lt;_M x^\beta \Leftrightarrow M\alpha &lt;_{lex} M\beta$ | TermOrder(M) |
| 分块：$x^a y^b \prec x^{a'} y^{b'} \Leftrightarrow a &lt;_1 a'$ 或 $(a = a', b &lt;_2 b')$ | T1 + T2 |

表9.5 · 单项式序。

### 9.3.1 单项式序

单项式序或容许序是多项式环的单项式 $x^\alpha$ 上的一个全序，它满足

$$x^\alpha \prec x^\beta \Longrightarrow x^{\alpha+\gamma} \prec x^{\beta+\gamma} \qquad\text{且}\qquad \gamma \neq 0 \Longrightarrow 1 \prec x^\gamma \qquad (9.9)$$

对所有指数 $\alpha, \beta, \gamma$ 成立。等价地，我们可以将 $\prec$ 看作指数 $\alpha \in \mathbb{N}^n$ 上的序，或单项式 $c x^\alpha$ 上的序。对于当前的单项式序，多项式 $p$ 的首项单项式、首项系数和首项（参见 §1.1.3）是指数最大的那些；我们分别用 lm p、lc p 和 lt p 表示它们。

(9.9) 中的第一个条件说明单项式序应与乘积相容：乘以一个固定的单项式不改变序。第二个条件意味着 $\prec$ 是一个良序，即不存在无限递减的单项式序列。让我们注意到，$K[x]$ 上唯一的单项式序是通常的序 $x^n > x^{n-1} > \cdots > 1$。

我们在 §9.1.1 中已经看到，Sage 允许在定义多项式环时通过如下构造选择序：

```sage
sage: R.<x,y,z,t> = PolynomialRing(QQ, order='lex')
```

表9.5 列出了主要的预定义单项式序；lex 是指数的字典序，invlex 是从右向左读取指数的字典序^a，而 *deglex* 先按全次数对单项式排序，再按字典序排序。*degrevlex* 的定义稍复杂：先按全次数排序，然后按指数*从右向左读取*的*递减*字典序排序。然而，当我们省略 *order* 选项时，默认使用的正是这种奇怪的序，因为对于某些计算它比其他序更高效。

^a Sage 还允许称为“局部”的序，其中 1 是最大的单项式而不是最小的。例如，在 Q[x,y,z] 上的 neglex 序中，有 1 > z > z^2 > z^3 > y > ⋯

我们通常（但并非总是！）同时选择环的变量序和单项式序，使得 $x_1 > x_2 > \cdots > x_n$，然后我们常常说例如“满足 $x > y > z$ 的 lex 序”，而不是“$K[x,y,z]$ 上的 lex 序”。预定义的序 lex、deglex 和 degrevlex 遵循该约定；对于 $K[x,y,z]$ 上的 *invlex* 序，它也是满足 $z > y > x$ 的 lex 序，即 $K[z,y,x]$ 上的 lex 序。

### 9.3.2 多项式族的除法

固定一个单项式序 $\prec$，设 $G = \{g_1,g_2,\ldots,g_s\}$ 是来自 $K[x]$ 的有限多项式集合。我们用 $\langle G\rangle = \langle g_1,g_2,\ldots,g_s\rangle$ 表示由 $G$ 生成的 $K[x]$ 的理想。

多项式 $p \in K[x]$ 被 $G$ 除是 $K[x]$ 中欧几里得除法的多元类比。与后者一样，它给 $p$ 关联一个余式，在 Sage 中由表达式 `p.reduce(G)` 给出，它是一个“更小的”多项式，属于模 $\langle G\rangle$ 的同一个等价类：

```sage
sage: ((x+y+z)^2).reduce([x-t, y-t^2, z^2-t])
2*z*t^2 + 2*z^2*t + t^4 + 2*t^3 + t^2 + t
```

余式通过不断从 $p$ 中减去 $G$ 的元素的倍数得到，这些元素的首项在减法中消去了 $p$ 的某一项。与一元情形相反，可能发生这样的情况：我们虽然可以借此消去 $p$ 的一项，但不是首项：此时我们只要求根据单项式序消去最大的一项。

形式化地，对于 $p \in K[x]$，我们用 $\operatorname{lt}_G p$ 表示 $p$ 中指数最大的项，该项可被 $G$ 中某个元素的首项整除。我们将如下形式的每个变换称为*初等约化*

$$p \mapsto \tilde{p} = p - c x^\alpha g, \qquad \text{其中 } g \in G \text{ 且 } \operatorname{lt}_G p = c x^\alpha \operatorname{lt} g. \qquad (9.10)$$

初等约化不改变 $p$ 模 $\langle G\rangle$ 的等价类，并使 $p$ 中被约化的最大单项式消失：我们有

$$\tilde{p} - p \in \langle G\rangle \qquad\text{且}\qquad \operatorname{lt}_G \tilde{p} < \operatorname{lt}_G p.$$

由于 $\prec$ 是良序，不可能对多项式进行无限多次连续的初等约化。每个初等约化序列都终止于一个局部序，该局部序在定义 (9.9) 的意义下不是良序，我们在本书中不使用它们；然而，好奇的读者可以使用 §9.1.1 中定义的 test_poly 函数来完善表9.5。

