

I13. \(I\) 是一个连续函数。

这类蕴含式最重要的两个族要么与布尔逻辑的形式主义相关，要么与直觉主义逻辑中的剩余概念相关。对于上述提到的概念，下面引入了合适的定义 [11]、[22]、[27]、[28]：

**Definition 11.2.** 与 t-余范数 \(S\) 和强否定 \(N\) 相关联的 S-蕴含式定义为
\[
\forall_{x,y\in[0,1]}\; I_{S,N}(x,y)=N(x)\ast_S y. \tag{11.2}
\]

**Definition 11.3.** 与 t-范数 \(T\) 相关联的 R-蕴含式定义为
\[
\forall_{x,y\in[0,1]}\; I_T(x,y)=\sup_z\{z\mid x\ast_T z\le y\}. \tag{11.3}
\]

上式可由以下经典集合论恒等式证明 [11]：
\[
\overline{A}\cup B=\overline{A\setminus B}=\bigcup\{Z\mid A\cap Z\subseteq B\}, \tag{11.4}
\]
其中 \(\setminus\) 表示集合差运算。

我们可以看到，对于任意 t-范数 \(T\)、t-余范数 \(S\) 和强否定 \(N\)，\(I_{S,N}\) 和 \(I_T\) 都满足条件 I1-I5；因此它们是模糊蕴含式。

为完整起见，我们提及量子逻辑中使用的第三种类型的蕴含式：

**Definition 11.4.** 与 t-范数 \(T\)、t-余范数 \(S\) 和强否定 \(N\) 相关联的 QL-蕴含式定义为
\[
\forall_{x,y\in[0,1]}\; I_{T,S,N}(x,y)=N(x)\ast_S(x\ast_T y). \tag{11.5}
\]

一般而言，\(I_{T,S,N}\) 违反性质 I1。然而，QL-蕴含式满足 I1 的条件可在 [9] 中找到。

考虑到蕴含式与否定的联系，我们注意到 \(I(\cdot,0)\) 是非递增且连续的。然而，它通常既不是严格递减也不是连续的。蕴含式的连续性足以但不是必要条件来通过剩余运算获得强否定。作为示例，[9]、[16] 中考虑并在下面回顾的一种特定 t-范数（称为幂零最小）和 t-余范数（称为幂零最大）：
\[
x\wedge_0 y=\min_0(x,y)=\begin{cases}0, & \text{if }x\le N(y),\\ \min(x,y), & \text{if }x>N(y).\end{cases} \tag{11.6}
\]
和
\[
x\vee_1 y=\max_1(x,y)=\begin{cases}1, & \text{if }x\le N(y),\\ \max(x,y), & \text{if }x>N(y).\end{cases} \tag{11.7}
\]

那么剩余蕴含式具有如下形式：
\[
I_{\min_0}(x,y)=I_{\mathrm{Fodor}}(x,y)=\begin{cases}1, & \text{if }x\le y,\\ \max(1-x,y), & \text{if }x>y.\end{cases} \tag{11.8}
\]

尽管 \(I_{\min_0}\) 不是连续的，但 \(I_{\min_0}(x,0)=1-x\)，\(x\in[0,1]\)，是标准的强否定。模糊蕴含式 (11.8) 由 Fodor [9]、[11] 引入，并在后续考虑中也会被考虑。

由于 t-范数（例如 M-、Π-、W-、Z-范数）、t-余范数（例如 M'-、Π'-、W'-、Z'-余范数）和强否定（例如 \(N(x)=1-x\)）是表示 AND、OR、NOT 的成熟模型，模糊蕴含式应被视为与这些模型密切相关。代表上述讨论的模糊蕴含式类别的最重要模糊蕴含式并列于表 11.1。

Table 11.1 Selected fuzzy implications

| Impl. Name | Implication Form | Imp. Type | Prop. |
|---|---|---|---|
| Łukasiewicz | \(\min(1-x+y,1)\) | R with T = W<br>S with S = W'<br>QL with T = min<br>S = W' | I1-I13 |
| Fodor | \(\begin{cases}1 & x\le y\\ \max(1-x,y) & x>y\end{cases}\) | R with T = min₀<br>S with S = max₁<br>QL with T = min<br>S = max₁ | I1-I12 |
| Reichenbach | \(1-x+xy\) | S with S = Π' | I1-I7, I9, I10, I12, I13 |
| Kleene-Dienes | \(\max(1-x,y)\) | S with S = max<br>QL with T = W<br>S = W' | I1-I7, I9, I10, I12, I13 |
| Zadeh | \(\max[1-x,\min(x,y)]\) | QL with T = min<br>S = max | I2, I3, I5, I6, I9, I13 |

我们还可以使用从 \([0,1]\) 区间内模糊蕴含式相对于模糊运算的位置获得的综合指标对模糊蕴含式进行分类和排序。

设 \(\star_1,\star_2:[0,1]^2\to[0,1]\) 为可测函数，被视为 \([0,1]\) 中的二元运算。运算 \(\star_1\) 和 \(\star_2\) 相对于其参数值的距离计算如下 [6]：
\[
d(\star_1,\star_2)=\int_0^1\int_0^1 |x\star_1 y-x\star_2 y|\,dx\,dy, \tag{11.9}
\]
其中 \(d\) 在此处为伪度量距离。

对于常数运算，即对于所有 \(x,y\in[0,1]\) 有 \(x\star_1 y=0\)，\(x\star_2 y=1\)，我们得到 \(d(\star_1,\star_2)=1\)。由于常数运算仅在边界条件下与剧烈运算不同，剧烈运算的距离如下获得：
\[
d(\sqcap,\sqcup)=1, \tag{11.10}
\]
其中 \(\sqcap\) 和 \(\sqcup\) 分别表示剧烈乘积（Z-范数）和剧烈和（Z'-余范数）。

考虑到 min (\(\wedge\))（M-范数）和 max (\(\vee\))（M'-余范数）运算，我们可以将 \([0,1]\) 区间划分为三个基本类如下：

- 乘积 \((\sqcap\le\star_T\le\wedge)\in[0,1/3]\)，
- 平均值 \((\wedge\le\star_A\le\vee)\in[1/3,2/3]\)，
- 和 \((\vee\le\star_S\le\sqcup)\in[2/3,1]\)。

作为示例，让我们根据伪度量距离在 \([0,1]\) 区间内定位两个乘积（代数乘积 \(x\cdot y=xy\) 和有界乘积 \(x\odot y=0\vee(x+y-1)\)）。对于代数乘积，计算出的距离为 \(d(\sqcap,\cdot)=1/4\)，对于有界乘积我们得到 \(d(\sqcap,\odot)=1/6\)。通过类比，我们得到代数和 \(x\dotplus y=x+y-xy\) 和有界和 \(x\oplus y=1\wedge(x+y)\) 的位置，它们相对于 \([0,1]\) 区间中的 \(1/2\) 与相应的乘积对称。这些以及一些额外的已知结果在图 11.1(A) 中进行了说明。

我们还可以对使用代数乘积和有界乘积获得的其他运算族进行排序，例如 Yager 运算、Schweizer 和 Sklar 运算、Frank 运算、Hamacher 运算等。

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_380_0.png)

Figure 11.4 Graphical illustration of Reichenbach fuzzy implication

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_380_1.png)

Figure 11.5 Graphical illustration of Kleene-Dienes fuzzy implication

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_381_0.png)

Figure 11.6 Graphical illustration of Zadeh fuzzy implication

## 11.3 Reasoning using fuzzy implications and generalized modus ponens

模糊蕴含式主要用作对具有模糊前件和/或模糊后件的 if-then 规则的解释方式。此类规则构成了表达知识片段的便捷形式，一组 if-then 规则构成模糊规则库。让我们考虑模糊 if-then 规则 \(R^{(k)}\) 的规范形式，该形式在 (MISO) 形式中包含了其他类型的模糊规则和模糊命题作为特例：
\[
R^{(k)}:\ \text{if }X_1\text{ is }A_1^{(k)}\text{ and }\ldots\text{ and }X_n\text{ is }A_n^{(k)}\text{ then }Y\text{ is }B^{(k)}, \tag{11.11}
\]
其中 \(X_i\) 和 \(Y\) 表示前件和后件的语言变量，\(A_i^{(k)}, B^{(k)}\) 是论域 \(X_i\subset\mathbb{R}\)，\(Y\subset\mathbb{R}\) 中的模糊集。

这种模糊 if-then 规则的语言形式也可以表示为模糊关系：
\[
R^{(k)}=(A_1^{(k)}\times\cdots\times A_n^{(k)}\Rightarrow B^{(k)})=(A^{(k)}\Rightarrow B^{(k)}), \tag{11.12}
\]
其中 \(A^{(k)}=A_1^{(k)}\times\cdots\times A_n^{(k)}\) 是 \(X=X_1\times\cdots\times X_n\) 中的模糊关系，定义为
\[
(A_1^{(k)}\times\cdots\times A_n^{(k)})(x_1,\ldots,x_n)=A_1^{(k)}(x_1)\ast_T\cdots\ast_T A_n^{(k)}(x_n)=A^{(k)}(x), \tag{11.13}
\]
其中 \(\ast_T\) 表示相应的 t-范数 \(T\)。

模糊 if-then 规则可以有两种解释：作为前件和后件的合取（Mamdani 组合）或作为模糊蕴含式 [6]、[7]、[8]、[28]、[30]。本章主要利用第二种解释。

近似推理通常在模糊推理系统中执行，该系统通过模糊规则库将 \(X\) 中的输入模糊集 \(A'\) 映射到 \(Y\) 中的模糊集 \(B'\)。可以使用两种近似推理方法：基于组合的推理（先聚合后推理 - FATI）和基于单个规则的推理（先推理后聚合 - FITA）。

在基于组合的推理中，有限数量的规则 \(k=1,\ldots,K\) 通过交集或平均运算进行聚合，即：
\[
R=\bigcap_{k=1}^{K}{}_{T,\Sigma}R^{(k)}, \tag{11.14}
\]
其中 \(\bigcap_{T,\Sigma}\) 表示使用 t-范数 \(T\) 或平均值（例如归一化算术和）聚合相应隶属函数的聚合运算符号：
\[
R(x,y)=R^{(1)}(x,y)\begin{bmatrix}\ast_T\\ +\end{bmatrix}\cdots\begin{bmatrix}\ast_T\\ +\end{bmatrix}R^{(K)}(x,y). \tag{11.15}
\]

考虑到 \(X\) 中的任意输入模糊集 \(A'\) 并使用广义 modus ponens，我们得到模糊推理的输出（FATI）：
\[
B'=A'\circ R=A'\circ\bigcap_{k=1}^{K}{}_{T,\Sigma}R^{(k)}=A'\circ\bigcap_{k=1}^{K}{}_{T,\Sigma}\left(A^{(k)}\Longrightarrow B^{(k)}\right) \tag{11.16}
\]
或以隶属函数表示：
\[
B'(y)=\sup_{x\in X}\left[A'(x)\ast_T R(x,y)\right]=\sup_{x\in X}\left[A'(x)\ast_T\begin{bmatrix}\displaystyle\bigwedge_{k=1}^{K}{}_T\\[2pt]\displaystyle\sum_{k=1}^{K}\end{bmatrix}R^{(k)}(x,y)\right]. \tag{11.17}
