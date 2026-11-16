

变形梯度，混合变分公式分为两类，即 \( F \)-公式和 \( \bar{F} \)-公式 [99]。在本节中，我们回顾 \( F \)-公式；对于 \( \bar{F} \)-公式，读者可参阅 [17, 99, 188] 及其中的参考文献。

基本思想是引入一个函数 \( \widehat{W} \)，使得当 \( J = \det F \) 时有 \( W(x, F) = \widehat{W}(x, F, J) \)，以及其部分Legendre变换，

```
\(\widehat{W}^*(x, F, \bar{q}) = \max_{\bar{q}} \{ \bar{q}(J - 1) - \widehat{W}(x, F, J) \}.\)
```

只要 \( \widehat{W} \) 关于自变量 \( J \) 是凸的，则以下对偶关系成立：

```
\(\widehat{W}(x, F, J) = \max_{\bar{q}} \{ \bar{q}(J - 1) - \widehat{W}^*(x, F, \bar{q}) \}.\) (12.4)
```

将关系 (12.4) 直接代入最小势能原理 (12.1)-(12.2)，得到以下替代混合变分原理：

```
\(\widehat{\Pi}(u, \bar{p}) = \min_{v \in \mathcal{K}} \max_{\bar{q} \in \mathcal{Q}} \widehat{\Pi}(v, \bar{q}),\) (12.5)
```

其中

```
\(\begin{aligned} \widehat{\Pi}(v, \bar{q}) &= \int_{\Omega} \{ -\widehat{W}^*(x, F(v), \bar{q}) + \bar{q}[\det F(v) - 1] \} \, dx \\ &\quad - \int_{\Omega} f \cdot v \, dx - \int_{\Gamma^u} t \cdot v \, ds. \end{aligned}\) (12.6)
```

在上述表达式中，\( \mathcal{Q} \) 表示平方可积标量函数的集合，极大化标量场 \( \bar{p} \) 通过 [99] 与平衡柯西静水压力场 \( p := \text{tr } \sigma \) 直接相关：

```
\( p = \bar{p} - \frac{1}{3 \det F} \frac{\partial \widehat{W}^*}{\partial F}(x, F, \bar{p}) : F.\)
```

与变分原理 (12.5)-(12.6) 相关的欧拉-拉格朗日方程的弱形式如下：

```
\(\begin{aligned} G^u(v, \bar{q}; \delta v) = \int_{\Omega} \left[ -\frac{\partial \widehat{W}^*}{\partial F}(x, F(v), \bar{q}) + \bar{q} \, \text{adj}(F^T(v)) \right] : \nabla(\delta v) \, dx \\ \quad - \int_{\Omega} f \cdot \delta v \, dx - \int_{\Gamma^u} t \cdot \delta v \, ds = 0 \quad \forall \delta v \in \mathcal{K}^0, \end{aligned}\)
```

```
\( G^{\bar{q}}(v, \bar{q}; \delta \bar{q}) = \int_{\Omega} \left[ \det F(v) - 1 - \frac{\partial \widehat{W}^*}{\partial \bar{q}}(x, F(v), \bar{q}) \right] \delta \bar{q} \, dx = 0 \quad \forall \delta \bar{q} \in \mathcal{Q},\)
```

其中，试验场 \( \delta \bar{q} \) 是 \( \bar{q} \) 的变分，\( \text{adj}(\cdot) \) 表示伴随算子。

## 12.3 多边形和多面体近似

本节讨论多边形和多面体有限元近似的位移空间和压力空间。在2D中，我们介绍线性和二次多边形有限元的符合有限维位移空间和压力空间的构造。在3D中，我们介绍凸多面体上的线性位移有限元空间的构造。

### 12.3.1 2D多边形上的位移空间

让我们从2D设置开始，考虑在未变形配置中具有n条边和顶点 v1, ..., vn 的一般多边形 P。我们使用广义重心坐标作为P上线性多边形有限元空间的基，记为 V1(P)，自由度与P的顶点相关联。

文献中可以找到相当多的重心坐标 [15, 34, 149, 193, 215, 265, 275, 372]（详情见第1章），其中本章采用了平均值坐标 [144]。平均值坐标，记为 phi_1^(1), ..., phi_n^(1)，可以在任意多边形上构造。定义在非凸多边形上的平均值坐标的等值线图如图 12.2(a) 所示。

P上的二阶空间，记为 V2(P)，可以通过广义重心坐标的两两乘积构造 [380]。V2(P) 是一个 2n 维空间，在P的每个顶点以及每条边的中点处具有自由度。其插值函数 phi_i^(2) ... phi_2n^(2) 表示为：

```
\phi_i^{(2)}(\boldsymbol{x}) = \sum_{j=1}^n \sum_{l=1}^n c_{jl}^i \phi_j^{(1)}(\boldsymbol{x}) \phi_l^{(1)}(\boldsymbol{x}),
```

其中 \phi_j^{(1)} 是平均值坐标。系数 c_{jl}^i 的计算方式使得

![](img/4913dd83a2a14bc205a0a92cce102c82_239_0.png)

图 12.2 (a) 凹多边形上平均值基 \phi_i^{(1)} 的等值线图。(b) 凹多边形上与顶点相关的二次基 \phi_i^{(2)} 的等值线图。(c) 凹多边形上与中边节点相关的二次基 \phi_i^{(2)} 的等值线图。参见彩色插页。

使得任何二次函数都可以由 $\phi_i^{(2)}$ 精确插值：

$q(\boldsymbol{x}) = \sum_{i=1}^n [q(\boldsymbol{v}_i)\phi_i^{(2)}(\boldsymbol{x}) + q(\dot{\boldsymbol{v}}_i)\phi_{i+n}^{(2)}(\boldsymbol{x})] \quad \forall q \in \mathcal{P}_2(E),$

以及克罗内克-德尔塔性质

$\phi_i^{(2)}(\boldsymbol{v}_j) = \phi_{i+n}^{(2)}(\dot{\boldsymbol{v}}_j) = \delta_{ij}, \quad \phi_i^{(2)}(\dot{\boldsymbol{v}}_j) = \phi_{i+n}^{(2)}(\boldsymbol{v}_j) = 0 \quad \forall i,j = 1, \dots, n,$

得到满足，其中 $\dot{\boldsymbol{v}}_i = (\boldsymbol{v}_i + \boldsymbol{v}_{i+1})/2$ 表示中边节点。

虽然上述构造是基于多边形元素严格凸的假设推导出来的 [320]，但我们也发现，当从平均值坐标构造时，它在凹多边形上也是有效的。凹多边形上顶点节点和中边节点的基函数图分别见图 12.2(b) 和 12.2(c)。

### 12.3.2 3D多面体上的位移空间

设 $P \in \mathbb{R}^3$ 为一个多面体，其边界在未变形配置中由平面多边形面组成，其 $n$ 个顶点位于 $\boldsymbol{v}_1, \dots, \boldsymbol{v}_n$。与2D情况一样，可以定义广义重心坐标 $\phi_1^{(1)}, \dots, \phi_n^{(1)}$ 作为基于顶点自由度的 $P$ 上线性多面体有限元空间的基。

本章考虑了在 [413] 中定义并在 [147] 中分析的瓦赫斯普坐标，这些坐标适用于简单多面体。这意味着对于每个 $i = 1, \dots, n$，包含 $\boldsymbol{v}_i$ 的面集恰好由三个面组成。与之前一样，我们用 $\mathcal{V}_i(P) = \text{span}\{\phi_i^{(1)}, \dots, \phi_n^{(1)}\}$ 表示 $P$ 上的有限元空间，由于瓦赫斯普坐标的线性精度，该空间包含 $\mathcal{P}_1(P)$。我们指出，本章后面描述的梯度修正方案也适用于线性和二次多面体上的其他类型坐标，尽管其实现和数值模拟中的性能的某些方面需要单独研究。

### 12.3.3 2D多边形上的压力空间

关于双字段混合有限元，需要近似额外的压力场。本章仅考虑2D中的混合多边形元素；我们将混合多面体元素留作未来工作的主题。对于 $\mathcal{Q}$ 的符合近似，可以采用不连续或连续近似。对于不连续近似，离散压力空间 $\mathcal{Q}_{h,k-1}^D$ 可定义为：

$\mathcal{Q}_{h,k-1}^D = \{ \hat{q}_h \in \mathcal{Q} : \hat{q}_h|_P \in \mathcal{P}_{k-1}(P) \forall P \in \Omega_h \},$

其中 $k$ 是元素的阶次。如上述定义所示，近似压力场可能在元素边界处不连续。这种类型

![](img/4913dd83a2a14bc205a0a92cce102c82_241_0.png)

图 12.3 不同混合多边形元素的位移场和压力场自由度示意图。(a) \(M_1 - \mathcal{P}_0^D\) 元素，(b) \(M_2 - \mathcal{P}_1^D\) 元素，(c) \(M_2 - M_1\) 元素。

的混合元素与流体问题中的Crouzeix-Raviart (C-R) 元素相似 [110]。在本章余下部分，我们采用 [100] 的缩写，并将这一族混合元素表示为 \(\mathcal{M}_k - \mathcal{P}_{k-1}^D\) 元素。因此，\(M_1 - \mathcal{P}_0^D\) 元素的压力空间由分段常数函数组成，即在每个元素上为常数。同样，\(M_2 - \mathcal{P}_1^D\) 元素的压力空间包含分段线性函数，在每个元素上线性变化。或者，压力空间的连续近似可以定义如下：

\(\mathcal{Q}_{h,k-1}^C = \{ \hat{q}_h \in C^0(\Omega) : \hat{q}_h|_P \in \mathcal{M}_{k-1}(P) \forall P \in \Omega_h \}.\)

这一类元素类似于流体问题中的Taylor-Hood (T-H) 元素 [395]，此后表示为 \(\mathcal{M}_k - \mathcal{M}_{k-1}\) 元素 (\(k \ge 2\))。这里我们考虑最高到二阶的两种混合多边形有限元。作为示例，这些混合多边形元素的位移场和压力场的自由度（DOFs）如图 12.3 所示。

## 12.4 积分规则与精度要求

在一般多边形和多面体元素上，广义重心坐标通常是非多项式函数。如 [100, 388, 393] 中所讨论，使用现有积分方案计算涉及重心坐标及其梯度的弱形积分会导致在网格细化下持续存在的误差。为了控制积分误差并恢复多项式

