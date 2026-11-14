

是一个 $\mathcal{Y}^n, P^{V,x}$ 鞅。还需验证

$$
\alpha^n u(y_n) + \sum_{j=1}^{n-1} \alpha^j (u(y_j) - \alpha \Phi^{v_j}(y_1, \cdots, y_j) u(y_j)),
$$

是一个 $\mathcal{Y}^n, P^{V,x}$ 鞅。

**注.** 我们可以将确定性情况视为马尔可夫链的一种特例，其中

$$
\pi(x, v, d\eta) = \delta_{g(x,v)}
$$

为点 $g(x, v)$ 处的迪拉克测度。然而，控制必须以闭环方式定义。我们无法以这种方式恢复开环控制。这就是为什么通过这条路径来考虑确定性问题是不必要地复杂。

## 4.2.2. 问题设定。

考虑

(4.2.1) $$l(x, v) \ge 0,$$

且 $U$ 是度量空间的一个子集。

我们考虑一个由转移概率 $\pi(x, v, \Gamma)$ 描述的受控马尔可夫链。考虑一个控制策略 $V$，并为标准过程 $y_n$ 构造相应的概率 $P^{V,x}$。控制中出现的函数 $v_n(x_1, \cdots, x_n)$ 必须取值于 $U$。

我们定义代价泛函

(4.2.2) $$
J_x(V) = E^{V,x} \sum_{n=1}^{\infty} \alpha^{n-1} l(y_n, v_n).
$$

如果接受值 $+\infty$，则该量定义良好。值函数定义为

$$
u(x) = \inf_V J_x(V).
$$

一个重要的问题是，值函数是否满足一个函数方程，如同在确定性情况下那样，遵循代数论证。这变得高度非平凡，但我们将证明这是可能的，在一个对应用有用且在某种程度上模拟确定性情况的情况下。在上述一般情况下，我们将通过使用分析论证而非代数论证来避免这一困难。

## 4.2.3. 直接方法。

我们考虑动态系统演化描述如下的情况。考虑一个概率空间 $(\Omega, \mathcal{A}, P)$，在其上定义了一个由独立同分布随机变量组成的随机过程 $D_1 \cdots D_n \cdots$。符号 $D$ 唤起需求过程，该过程将在库存控制的应用中不断出现。我们用 $h(\xi)$ 表示一个通用 $D$ 的概率密度，为明确起见，它位于 $R^k$。过程 $y_n$ 由以下定义

$$
y_{n+1} = g(y_n, v_n, D_n) \quad y_1 = x.
$$

我们将假设需求是可观测的。在时刻 $n+1$，我们已观察到 $D_1 \cdots D_n$ 的值。所以

$$
v_n = v_n(D_1, \cdots, D_{n-1}) \quad n \ge 2,
$$

且 $v_1$ 是确定性的。这比 $v_n = v_n(y_1, \cdots, y_n)$ 更一般，并且自然地源于每个时刻可用的信息。如果 $U$ 依赖于 $x$，则我们有约束

$v_n(D_1, \cdots, D_{n-1}) \in U(y_n),$

且 $y_n$ 也是 $D_1, \cdots, D_{n-1}$ 的一个函数。算子 $\Phi^v f(x)$ 由以下给出

(4.2.3) $\Phi^v f(x) = E f(g(x, v, D)) = \int f(g(x, v, y)) \eta(dy).$

令 $V = \{v_1, \cdots, v_n, \cdots \}$ 为上述定义的控制。收益由以下给出

(4.2.4) $J_x(V) = E \sum_{n=1}^\infty \alpha^{n-1} l(y_n, v_n).$

需要注意的是，期望是相对于固定概率 $P$ 取的，不像公式 (4.2.2) 那样依赖于控制策略。我们定义值函数

$u(x) = \inf_V J_x(V).$

**命题 4.3.** *值函数满足函数方程（贝尔曼方程）*

(4.2.5) $u(x) = \inf_{v \in U(x)} [l(x, v) + \alpha E u(g(x, v, D))].$

证明。令

$K(x, v_1, \cdots, v_n, \cdots ; D_1, \cdots, D_n, \cdots) = \sum_{n=1}^\infty \alpha^{n-1} l(y_n, v_n),$

这是关于 $D_1, \cdots, D_n \cdots$ 的一个泛函。得益于随机变量的独立性，我们有

$EK(x, v_1, \cdots, v_n, \cdots ; D_1, \cdots, D_n, \cdots) = E_{D_1 D_2 \cdots} K(x, v_1, \cdots, v_n, \cdots ; D_1, \cdots, D_n, \cdots),$

其中右侧作为下标的期望意味着必须依次取期望。我们从后往前开始。期望数量无限这一点不是问题，因为 $K$ 表达式中的每一项仅依赖于有限个需求。注意关系式

$K(x, v_1, \cdots, v_n, \cdots ; D_1, \cdots, D_n, \cdots) = l(x, v_1) + \alpha K(g(x, v_1, D_1), v_2, \cdots, v_n, \cdots ; D_2, \cdots, D_n, \cdots).$

因此，对于固定的 $x, v_1, D_1$，我们可以写出

(4.2.6) $\inf_{v_2 \cdots v_n \cdots} E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2, \cdots, v_n, \cdots ; D_2, \cdots, D_n, \cdots) = u(g(x, v_1, D_1)).$

现在关键点是验证

(4.2.7) $E_{D_1} \inf_{v_2 \cdots v_n \cdots} E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2, \cdots, v_n, \cdots ; D_2, \cdots, D_n, \cdots) = \inf_{v_2 \cdots v_n \cdots} E_{D_1 D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2, \cdots, v_n, \cdots ; D_2, \cdots, D_n, \cdots).$

换句话说，我们可以交换两个算子 $E_{D_1}$ 和 inf。其原因是决策变量 $v_2 \cdots, v_n \cdots$ 是所有随机变量（包括 $D_1$）的函数。更具体地说，我们首先可以断言

$E_{D_1} \inf_{v_2 \cdots v_n \cdots} E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots, \cdots) \le E_{D_1 D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots, \cdots)$

其中，在右侧，决策变量是任意的。因此，方程 (4.2.7) 的左侧小于其右侧。另一方面，对于任何 $\epsilon$ 和任何固定的 $D_1$，我们可以找到一个依赖于 $D_1$ 的策略 $v_2^\epsilon, \cdots, v_n^\epsilon \cdots$，使得

$E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2^\epsilon, \cdots, v_n^\epsilon, \cdots ; D_2 \cdots, D_n \cdots, \cdots) \le \inf_{v_2 \cdots v_n \cdots} E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots, \cdots) + \epsilon.$

因此

$E_{D_1 D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2^\epsilon, \cdots, v_n^\epsilon, \cdots ; D_2 \cdots, D_n \cdots, \cdots) \le E_{D_1} \inf_{v_2 \cdots v_n \cdots} E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots) + \epsilon.$

因此也

$\inf_{v_2 \cdots v_n \cdots} E_{D_1 D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots, \cdots) \le E_{D_1} \inf_{v_2 \cdots v_n \cdots} E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots) + \epsilon,$

由于 $\epsilon$ 任意，(4.2.7) 的右侧小于左侧。故关系式 (4.2.7) 成立。该关系还意味着

$E u(g(x, v_1, D_1)) = \inf_{v_2 \cdots v_n \cdots} E K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots).$

但那么

$u(x) = \inf_v [l(x, v_1) + \alpha \inf_{v_2 \cdots v_n \cdots} E K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots)],$

这蕴含了结果。

## 4.3. 函数方程

我们从假设开始。空间 $X = R^d$。控制集 $U$ 是 $R^k$ 的一个闭子集。如果 $\phi(x, v)$ 是两个变量的函数，我们写 $\phi_v(x) = \phi(x, v)$。我们将假设

(4.3.1) 若 $\phi_v(x) = \phi(x, v)$ 在 $x, v$ 中一致连续且有界，则 $\Phi^* \phi_v(x)$ 在 $v, x$ 中一致连续。

我们还假设

(4.3.2) $l_v(x) = l(x, v)$ 为下半连续且 $\ge 0$；$l(x, v)$ 在有界集上有界；$\Phi^* l_v(x)$ 在有界集上有界；$\{ v \in U \mid l(x, v) \le L, |x| \le M \} \subset \{ |v| \le K_{LM} \}$。

### 4.3.1. 技术结果。

我们首先回顾几个重要的技术结果。一些证明在附录中。

**引理 4.1.** 设 $f$ 是从度量空间 $X$ 到 $(-\infty, +\infty]$ 的一个映射，它是下半连续且下有界的。存在一个序列 $f_n(x) \in C(X)$（$X$ 上一致连续有界函数的空间），使得 $f_n(x)$ 逐点上升到 $f(x)$。

**引理 4.2.** 在假设 (4.3.1) 下，如果 $l_v(x) = l(x, v)$ 是下半连续且下有界的，那么关于对 $(v, x)$ 的函数 $\Phi^* l_v(x)$ 是下半连续且下有界的。

**引理 4.3.** 设 $F(x, v)$ 在两个变量中均为下半连续且下有界。如果 $U$ 是度量紧的，那么

$G(x) = \inf_{v \in U} F(x, v),$

也是下半连续且下有界的。

一个关键结果是，对于每个 $x$，存在一个极小值，它是 $x$ 的可测函数。

**定理 4.1.** 在引理 4.3 的假设下，存在一个博雷尔函数 $\hat{v}(x) : X \to U$，使得

$G(x) = F(x, \hat{v}(x)), \forall x.$

$U$ 是紧的这一事实在某些应用中可能不成立。我们在此介绍一种在应用中出现的情况，其中去掉了 $U$ 的紧性假设。假设

- $U$ 是 $R^d$ 的一个闭子集；
- $F(x, v)$ 是下半连续且下有界的；
- $\{v \mid F(x, v) \le F(x, v_0)\} \subset \{v \mid |v| \le \gamma(x)\}$；
- $\gamma(x)$ 在有界集上有界。

我们陈述

**定理 4.2.** 在引理 4.3 的假设下（$U$ 紧除外），且如果假设 (4.3.3) 成立，那么 $G(x)$ 是下半连续且下有界的，并且存在一个博雷尔映射 $\hat{v}(x)，它对任何 $x$ 都取得极小值。

### 4.3.2. 天花板函数。

我们首先考虑将固定控制 $v_0 \in U$ 作为参数的情况。引入方程

(4.3.4) $w_0(x) = l(x, v_0) + \alpha \Phi^{v_0} w_0(x).$

更精确地，我们考虑函数

(4.3.5) $w_0(x) = \sum_{n=1}^\infty \alpha^{n-1} (\Phi^{v_0})^{n-1} l_{v_0}(x),$

其中我们已记 $l_v(x) = l(x, v)$。

函数 $w_0(x)$ 定义为当 $N \uparrow +\infty$ 时的极限

$w_{0N}(x) = \sum_{n=1}^N \alpha^{n-1} (\Phi^{v_0})^{n-1} l_{v_0}(x).$

