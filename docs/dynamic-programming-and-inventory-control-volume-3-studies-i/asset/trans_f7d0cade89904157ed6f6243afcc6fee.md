

假设随机变量 \( D^j \) 相互独立且服从泊松分布（参数为 \( \lambda^j \)），则定义

\(\gamma^j(x) = E\psi \left( x - \sum_{i=1}^j D_i \right), \gamma^0(x) = \psi(x).\)

显然 \(\chi(x) = \gamma^j(x)\).

### 练习 11.9. 证明

\(\gamma^j(x) = E\gamma^{j-1}(x - D_j).\)

由于每个需求都服从泊松分布，可以递归地验证，存在一个 \( b \)，使得 \(\chi(x)\) 在 \((-\infty, b]\) 上单调递减，在 \([b, +\infty)\) 上 \( K \) 单调非递减。

我们现在可以求解多供应商问题了。引入如下算子比较方便，方程 (11.2.6) 中的 \( w \) 是其不动点。更准确地说，引入函数 \( v(x) \)，使得

- (11.2.12)
- \( v \) 是连续的，\( (c_M + \alpha h)x + \alpha v(x) \to +\infty \)，当 \( x \to +\infty \)
- \( (c_1 - \alpha p)x + \alpha v(x) \to +\infty \)，当 \( x \to -\infty \)
- \( v(x) + c_M x \) 在 \((-\infty, 0]\) 上单调递减
- \( v(x) + c_i x \) 在 \( R \) 上 \( K_i \) 单调非递减

注意，根据第三个条件，我们还有

\( v(x) \to +\infty, \text{ as } x \to -\infty. \)

我们引入一个算子，该算子依次将函数 \( v(x) \) 关联到函数

\( g_i(v)(x) = c_i(x + \overline{D}) + \alpha(hx^+ + px^-) + \alpha v(x), \)

和

\( G_i(v)(x) = Eg_i(v)(x - D). \)

还令

\( G_i^*(v)(x) = \inf_{y \ge x} (K_i \mathbf{1}_{y > x} + G_i(v)(y)), \)

和

\( w_i(v)(x) = -c_i x + G_i^*(v)(x), \)
\( w(v)(x) = \min_{1 \le i \le M} w_i(v)(x). \)

那么，我们可以断言

\( w(x) = w(w)(x). \)

我们从以下内容开始

### 引理 11.3. 假设 (11.2.7) 且需求 \( D \) 满足性质 \( \mathcal{P} \). 在 \( G_i(v) \) 的记号中省略 \( v \)，我们可以断言

- (11.2.13)
- \( G_i \) 是连续的，\( G_i \to +\infty, \text{ as } |x| \to +\infty \)
- \( \exists a_i \ge 0 \text{ 使得 } G_i \text{ 在 } (-\infty, a_i] \) 上单调递减
- \( G_i \) 在 \( (a_i, +\infty) \) 上 \( K_i \) 单调非递减

证明。写出

\(g_t(x) = c_t \overline{D} + (c_t - c_t)x + (c_t - \alpha c_M)x + \alpha(hx^+ + px^-) + \alpha(c_M x + v(x)),\)

我们立即从假设 (11.2.7) 和 \(v\) 的性质看出

\(g_t(x)\) 在 \((-\infty, 0)\) 上单调递减。

再写出

\(g_t(x) = c_t \overline{D} + (1-\alpha)c_t x + \alpha(hx^+ + px^-) + \alpha(c_t x + v(x)),\)

我们从 \(v\) 的性质得到

\(g_t(x)\) 在 \([0, +\infty)\) 上非 \(K_t\) 单调递减。

显然，\(g_t(x) \to +\infty\) 当 \(|x| \to +\infty\)。由此可知，由数学期望的平滑效应，\(G_t(x)\) 是连续的。\(G_t(x) \to +\infty\)，当 \(|x| \to +\infty\)，并且由于需求满足性质 \(\mathcal{P}\)，存在 \(a_t \ge 0\)，使得 (11.2.13) 得到验证。

从之前考虑的中间优化问题的一般分析，特别是推论 11.2 可知，\(w(v)\) 满足与 \(v\) 相同的性质，即 (11.2.12)。此外，最优反馈 \(\delta(v)(x)\) 由广义 s,S 政策给出。

我们将上述发展应用于多供应商问题。我们从 \(w_0(x) = -c_M x\) 开始。如果假设 (11.2.7)，则该函数满足 (11.2.12) 中通用函数 \(v\) 的性质。因此递归可以开始。这完成了定理 11.3 的证明。\(\square\)

本页故意留空

## 马尔可夫需求下的库存控制

### 12.1. 引言

在迄今考虑的所有模型中，需求都被视为一组独立同分布的随机变量。实际上，连续需求出于许多原因是相关的。建模这种关联的最简单方法是假设需求本身构成一个马尔可夫过程，或源自一个马尔可夫过程。我们在这里的目标是展示前几章中描述的方法如何适应这种情况。在 D. Beyer 等人最近的一本书 [12] 中，对这些问题进行了全面的介绍。我们也参考该书的参考文献以了解相关文献。在这项工作中，作者认为需求来自一个底层的需求状态，该状态被建模为具有有限状态数的马尔可夫链。状态数有限这一事实简化了数学论证。我们将在这里讨论需求本身是马尔可夫过程的情况。

### 12.2. 无积压且无设置成本

### 12.2.1. 模型。

设 \(\Omega, \mathcal{A}, P\) 为概率空间，其上定义了马尔可夫链 \(z_n\)。这个马尔可夫链表示需求。其状态空间为 \(R^+\)，其转移概率为 \(f(\zeta|z)\)。我们假设

- (12.2.1) \(f(\zeta|z)\) 在两个变量中一致连续且有界
- (12.2.2) \(\int_0^{+\infty} \zeta f(\zeta|z) d\zeta \le c_0 z + c_1.\)

我们可以假设 \(z_1 = z\)，一个固定常数，或者更一般地，一个具有给定概率分布的随机变量。我们定义滤流 \(\mathcal{F}^n = \sigma(z_1, \cdots, z_n).\)

一个控制策略，记为 \(V\)，是随机变量序列 \(v_n\)，使得 \(v_n\) 是 \(\mathcal{F}^n\) 可测的。当 \(z_1 = z\) 时，\(v_1\) 是确定的。同样，我们通常假设 \(v_n \ge 0\)。我们接下来将库存定义为序列，其中

- (12.2.3) \(y_{n+1} = (y_n + v_n - z_{n+1})^+, \quad y_1 = x.\)

过程 \(y_n\) 适应于滤流 \(\mathcal{F}^n\)。联合过程 \(y_n, z_n\) 也是一个马尔可夫链。

对于测试函数 \(\varphi(x, z)\)（在 \(R^+ \times R^+\) 上有界连续），我们可以写出

\(E[\varphi(y_2, z_2)|y_1 = x, z_1 = z, v_1 = v]\)
\(= E[\varphi((x + v - z)^+, z_2)|z_1 = z]\)
\(= \int_{z+v}^{+\infty} \varphi(0, z)f(\zeta|z)d\zeta + \int_0^{x+v} \varphi(x + v - \zeta, z)f(\zeta|z)d\zeta\)

这定义了一个马尔可夫链，与其关联的算子为

(12.2.4) \(\Phi^v\varphi(x, z) = \int_{z+v}^{+\infty} \varphi(0, \zeta)f(\zeta|z)d\zeta + \int_0^{x+v} \varphi(x + v - \zeta, \zeta)f(\zeta|z)d\zeta,\)

因此转移概率由

(12.2.5) \(\pi(x, z, v, d\xi, d\zeta) = \delta(\xi) \otimes f(\zeta|z)\mathbb{1}_{z+v > x}d\zeta\)
\(+\delta(\xi - (x + v - \zeta)) \otimes f(\zeta|z)\mathbb{1}_{x+v < \zeta}d\zeta.\)

给出。

我们接下来定义函数

(12.2.6) \(l(x, z, v) = cv + hx + p \int_{z+v}^{\infty} (\zeta - x - v)f(\zeta|z)d\zeta,\)

它将模拟一期成本。成本函数为

(12.2.7) \(J_{x,z}(V) = E \sum_{n=1}^{\infty} \alpha^{n-1} l(y_n, z_n, v_n).\)

我们关注的值函数为

(12.2.8) \(u(x, z) = \inf_V J_{x,z}(V).\)

我们首先注意到性质 (4.3.1)、(4.3.2) 已满足。为继续，我们需要指定一个上限函数。它对应于恒等为 0 的控制。令 \(l_u(x, z) = l(x, z, v)\)。注意不等式。

(12.2.9) \(cv + hx \le l_u(x, z) \le cv + hx + p(c_0 z + c_1),\)

和

(12.2.10) \(cv \le \Phi^v l_u(x, z) \le cv + h(x + v) + p(c_0^2 z + c_0 c_1 + c_1).\)

然后考虑函数

(12.2.11) \(w_0(x, z) = \sum_{n=1}^{\infty} \alpha^{n-1} (\Phi^0)^{n-1} l_0(x, z)\)

### 引理 12.1. 我们假设

(12.2.12) \(\alpha c_0 < 1,\)

则级数 \(w_0(x, z) < \infty\)，更精确地说

(12.2.13) \(w_0(x, z) \le \frac{hx}{1 - \alpha} + \frac{pc_0 z}{1 - \alpha c_0} + \frac{pc_1}{(1 - \alpha)(1 - c_0 \alpha)}.\)

证明。这是公式 (12.2.11) 和 (12.2.10) 的直接结果。

我们现在可以写出贝尔曼方程

(12.2.14) \(u(x, z) = \inf_{v \ge 0} [l(x, z, v) + \alpha \Phi^v u(x, z)].\)

我们陈述以下内容

### 定理 12.1. 我们假设 (12.2.1)、(12.2.2)、(12.2.6)、(12.2.12)。那么方程 (12.2.14) 存在唯一解，满足 \(0 \le u \le w_0\)。它是连续的，并与值函数 (12.2.8) 重合。存在最优反馈 \(\hat{v}(x,z)\) 和最优控制策略 \(\hat{V}\)。

证明。我们首先注意到定理 4.4 和 4.3 的条件已满足。因此方程 (12.2.14) 的解集非空。它有一个最小解和一个最大解。最小解是下半连续的（l.s.c.），最大解是上半连续的（u.s.c.）。最小解与值函数重合。存在最优反馈 \(\hat{v}(x,z)\) 和最优控制策略 \(\hat{V}\)。为证明唯一性，我们需要证明最小解和最大解重合。我们首先证明 \(\hat{v}(x,z)\) 的一个界。首先，提及 \(w_0\) 的一个稍好估计会比较方便。确实，我们可以写出

\(\text{(12.2.15)} \quad w_0(x,z) \le h \sum_{n=1}^\infty (\alpha \Phi^0)^{n-1} x(x,z) + \frac{p c_0 z}{1-c_0 \alpha} + \frac{p c_1}{(1-\alpha)(1-c_0 \alpha)},\)

并且 (12.2.13) 仅通过使用 \(\Phi^0(x,x) \le x\) 从 (12.2.15) 得出。接下来，从 (12.2.14) 出发，考虑 \(\underline{u}\)，即最小解，我们可以断言

\(\underline{u}(x,z) \ge h \sum_{n=1}^\infty (\alpha \Phi^0)^{n-1} x(x,z),\)

这源于 \(l(x,z,v) \ge hx\)，以及

\(\text{(12.2.16)} \quad \Phi^v \varphi(x,z) \ge \Phi^0 \varphi(x,z), \forall v \ge 0, \forall \varphi \text{ 在 } x \text{ 中单调递增}.\)

因此，我们可以写出

\(l(x,z,v) + \alpha \Phi^v \underline{u}(x,z) \ge c v + h \sum_{n=1}^\infty (\alpha \Phi^0)^{n-1} x(x,z).\)

因此，在对 \(v\) 求最小值时，我们可以从上方界定 \(v\) 的范围。更精确地说，我们得到

\(\text{(12.2.17)} \quad \hat{v}(x,z) \le \frac{p c_0 z}{c(1-c_0 \alpha)} + \frac{p c_1}{c(1-\alpha)(1-c_0 \alpha)}.\)

我们考虑从最优反馈得到的最优轨迹 \(\hat{y}_n, z_n\)，即

其中 \(\hat{y}_1 = x, z_1 = z\)。

根据第 4 章第 4.5 节，如果我们能验证 \(\hat{V} \in \mathcal{V}\)，即

\(\alpha^n E \hat{u}(y_{n+1}, z_{n+1}) \to 0, \text{ 当 } n \to \infty\)

则最大解将与最小解重合。将 \(\hat{u}\) 替换为 \(w_0\) 就足够了，根据估计 (12.2.13)，只需证明

\(\text{(12.2.18)} \quad \alpha^n E \hat{y}_{n+1}, \quad \alpha^n E z_{n+1} \to 0, \text{ 当 } n \to \infty.\)

然而，根据标准的马尔可夫论证，\(\alpha^n E z_{n+1} \le (\alpha c_0)^n z\)。根据假设 (12.2.12)，(12.2.18) 的第二部分立即得出。接下来我们使用

\(\hat{y}_{n+1} \le \hat{y}_n + \hat{v}_n\)
\(\le \hat{y}_n + \frac{p c_0 z_n}{c(1-c_0 \alpha)} + \frac{p c_1}{c(1-\alpha)(1-c_0 \alpha)}.\)

