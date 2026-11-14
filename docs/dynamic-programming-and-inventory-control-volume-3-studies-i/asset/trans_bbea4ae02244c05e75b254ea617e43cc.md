

### 定理 9.3.
在假设 (9.2.1) 和 (5.1.2) 下，方程 (9.2.4) 在空间 $B_1$ 中存在且仅存在一个解。该函数是下半连续的（l.s.c.）。存在一个最优反馈 $\hat{v}(x)$，满足估计

(9.2.8)
\(\hat{v}(x) \le \frac{p\bar{D}}{c(1-\alpha)}.\)

解 \(u(x) = \inf_v J_v(x)$，即值函数。存在一个最优控制策略 \(\hat{V}$，由反馈 \(\hat{v}(x)$ 得出。

## 9.2.2. 最优策略.

重要的问题是刻画最优反馈，就像我们在无固定成本 \(K = 0$ 的情况下所做的那样，参见第 5 章，第 5.1.3 节。当存在固定成本时，我们无法得到基准库存策略。我们已经在确定性情况下看到，参见第 9.1 节，最优反馈是由 s, S 策略得到的，其中 \(s = D$。我们将看到，这种结构在随机情况下依然有效，只是 s, S 的值自然不同。遵循第 8 章发展的冲动控制理论，我们将确定 s, S 的值。

我们引入算子

(9.2.9)
\(T(u)(x) = hx + pE((x - D)^-) + \alpha Eu((x - D)^+),\)

(9.2.10)
\(M(u)(x) = K + \inf_{\eta \ge x} [(c - h)(\eta - x) + u(\eta)].\)

我们现在面临与第 8.3 节类似的情况。我们注意到函数方程 (9.2.5) 等价于

\(u(x) = \min[T(u)(x), M(T(u))(x)].\)

然而，这也等价于

(9.2.11)
\(u(x) = \min[T(u)(x), M(u)(x)].\)

这种表述是 (9.2.5) 的冲动控制表述。没有“连续”控制，因此算子 \(T(u)(x)$ 是仿射的。我们处于定理 8.4 的条件下，关于成本有界性有一个重要的区别。请注意，这里的变量订购成本是 \((c - h)v$ 所以我们假设

(9.2.12)
\(p > c > h.\)

第一个不等式是必不可少的，因为否则没有订购动机。第二个不等式不那么关键，但为了与我们对冲动控制问题的一般表述保持一致而采用。此外，它对于得到 s, S 策略将是必不可少的。我们不能使用定理 8.4 来证明解的存在性和唯一性，因为函数 \((x, v)$ 不是有界的。然而，通过与表述 (9.2.5) 的等价性，我们知道情况确实如此。因此，构造一个最优反馈由 s, S 策略给出的解就足够了。

我们从一些记号开始。定义

(9.2.13)
\(g(x) = (p - \alpha(c - h))E(x - D)^+ - (p - c)x + p\bar{D}.\)

对于任何 \(s \ge 0$，接下来定义

(9.2.14)
\(g_s(x) = (g(x) - g(s)) \mathbb{1}_{x > s}.\)

让我们设定

(9.2.15)
$$H_s(x) = \sum_{n=1}^\infty \alpha^{n-1} g_s * f^{*(n-1)}(x),$$

采用 (5.1.17) 的记号。

### 引理 9.4.
函数 $H_s(x)$ 在大于或等于 $s$ 的点处取得其最小值。取最小的最小值，定义一个函数 $S(s)$ 和

(9.2.16)
$$H_s(S(s)) = \inf_{\eta \ge s} H_s(\eta).$$

证明. 我们可以将 $H_s(x)$ 写为

$$H_s(x) = g_s(x) + \alpha g_s * f + \sum_{n=2}^\infty \alpha^n g_s * f^{*(n)}(x).$$

考虑

$$F^{(n)}(x) = \int_0^x f^{(n)}(\xi) \, d\xi,$$

则 $F^{(0)}(x) = 1, F^{(1)}(x) = F(x)$。如果

$$\Gamma(x) = \sum_{n=0}^\infty \alpha^n F^{(n)}(x),$$

那么我们可以轻松验证公式

(9.2.17)
$$H_s(x) = \int_s^x \Gamma(x-\xi) \mu(\xi) d\xi,$$

其中 $\mu = g'$。为函数 $F^{(n)}(x)$ 给出概率解释是有用的。事实上，我们有

$$F^{(n)}(x) = P(D_1 + \cdots + D_n \le x),$$

其中 $D_1, \cdots, D_n$ 是 $n$ 个独立同分布的随机变量，具有相同的概率密度 $f(x)$。这样一来，很明显

$$F^{(n)}(x) \uparrow 1, \text{ 当 } x \to \infty, \quad \Gamma(x) \uparrow \frac{1}{1-\alpha}, \text{ 当 } x \uparrow \infty.$$

因此，当 $x \uparrow \infty$ 时，$H_s(x) \to +\infty$。我们可以检查

$$H'_s(s+0) = \mu(s) = c(1-\alpha) + \alpha h - (p-\alpha(c-h))\bar{F}(s).$$

由于 $p > c$，函数 $\mu(s)$ 从 $-(p-c)$ 增加到 $(c(1-\alpha)+\alpha h)$。因此它在一点 $\bar{s}$ 处消失，并且对于 $0 \le s < \bar{s}$ 严格为负。这个 $\bar{s}$ 简单地是由公式 (5.1.14) 识别的基准库存。

首先考虑 $s \in [0, \bar{s}]$。因此 $H'_s(s+0) < 0$，函数 $H_s(x)$ 在 $x$ 接近 $s$ 时变为严格负值。此外

$$\begin{aligned} H_s(x) &= \int_s^x \Gamma(x-\xi)\mu(\xi)d\xi + \int_x^\infty \Gamma(x-\xi)\mu(\xi)d\xi \\ \ge \frac{1}{1-\alpha}(g(s) - g(s)) + g(x) - g(s). \end{aligned}$$

因此，当 $x \to \infty$ 时，$H_s(x) \to \infty$。由于它是连续函数，它在 $[0, \infty)$ 上取得其最小值。通过取最小的最小值（如果有多个），我们唯一地定义数字 \( S(s) \)。还要注意，如果 \( s \ge \bar{s}$，$H_s(x)$ 在 \( x \) 中是递增的，而对于 \( s < \bar{s}$，$H_s(x)$ 在区间 \( [s, \bar{s}) \) 上在 \( x \) 中是递减的，因此 \( S(s) = s$ 如果 \( s \ge \bar{s}$，$S(s) > s$ 如果 \( s < \bar{s}$。

还可以得出，对于 \( s < \bar{s}$，\( H'_s(S(s)) = 0$。因此

\(\frac{dH_s(S(s))}{ds} = \frac{\partial}{\partial s} H_s(x)_{x=S(s)}, \text{ 如果 } s < \bar{s}.\)

所以

(9.2.18)
\(\frac{dH_s(S(s))}{ds} = -\mu(s)\Gamma(S(s) - s) > 0, \text{ 如果 } s < \bar{s}.\)

显然，对于 \( s \ge \bar{s}$，$H_s(S(s)) = 0$。属性 (9.2.16) 已经证明。

现在考虑 \( S_0 = S(0)$。我们有

\( H_0(x) = \int_0^x \Gamma(\xi)\mu(x - \xi)d\xi. \)

所以

\( H'_0(x) = \mu(0)\Gamma(x) + \int_0^x \mu'(x - \xi)\Gamma(\xi) d\xi \)
\( = (c - p)\Gamma(x) + (p - \alpha(c - h)) \int_0^x f(x - \xi)\Gamma(\xi) d\xi. \)

然而，很容易检查 \( \Gamma(x) \) 满足更新方程

(9.2.19)
\( \Gamma(x) = 1 + \alpha \int_0^x f(x - \xi)\Gamma(\xi) d\xi. \)

因此

\( H'_0(x) = \frac{1}{\alpha}[(p - \alpha(p - h))\Gamma(x) - (p - \alpha(c - h))]. \)

因此 \( S_0 \) 由以下给出

(9.2.20)
\( \Gamma(S_0) = \frac{p - \alpha(c - h)}{p - \alpha(p - h)}. \)

我们需要假设

(9.2.21)
\( H_0(S_0) = \int_0^{S_0} \Gamma(\xi)\mu(S_0 - \xi)d\xi < -K. \)

我们可以陈述以下

### 定理 9.4.
在定理 9.3 和 (9.2.12), (9.2.21) 的假设下，函数方程 (9.2.5) 的最优反馈 \( \psi(x) \) 由一个 \( s, S \) 策略给出。\( s$ 的值是唯一的值，使得

(9.2.22)
\( K + \inf_{\eta \ge s} H_s(\eta) = 0, \)

并且 \( S(s) = s$。此外，函数 \( u(x) \) 是连续的

证明. 考虑函数 \( \inf_{\eta \ge s} H_s(\eta) = H_s(S(s)) \)。

我们有 \( H_s(S(s)) = 0$ 对于 \( s \ge \bar{s}$。从假设中，我们有 \( H_0(S(0)) < -K$。从 (9.2.18) 我们知道，对于 \( s < \bar{s}$，$H_s(S(s))$ 在 \( s$ 中是严格递增的。因此，将有一个且仅有一个 \( s$，使得 (9.2.22) 得到验证。因此，对 \( s, S$ 就被明确识别。我们将构造 (9.2.11) 的一个解，其最优反馈由一个 \( s, S$ 策略定义，使用刚刚定义的 \( s, S$ 值。为了简化记号，我们省略下标 s,S。我们使用记号 H(x) 表示 H_s(x)，使用特定的 s。考虑函数

(9.2.23)
\( u(x) = H(x) + (h - c)x + \frac{g(s)}{1 - \alpha} \).

由于 H(x) 是连续的，函数 u(x) 是连续的。然后 u(x) 满足

(9.2.24)
\( u(x) = \begin{cases} (h - c)x + \frac{g(s)}{1 - \alpha}, & x \le s \\ hx + pE(x - D)^- + \alpha Eu(x - D)^+, & x \ge s \end{cases} \)

并且，从 s 的选择中

(9.2.25)
\( K + \inf_{\eta \ge s} [u(\eta) + (c - h)\eta] = \frac{g(s)}{1 - \alpha}, \)

因此也

(9.2.26)
\(\begin{aligned} u(s) + (c - h)s &= K + \inf_{\eta \ge s} [u(\eta) + (c - h)\eta] \\ &= K + u(S) + (c - h)S \end{aligned}\)

由于

\( u(x) = -(c - h)x + \frac{g(s)}{1 - \alpha}, \quad x \le s, \)

函数 u(x) + (c - h)x 在 $[0, s]$ 上是常数。因此

\(\inf_{\eta \ge x} [(c - h)\eta + u(\eta)] = \inf_{\eta \ge s} [(c - h)\eta + u(\eta)], \quad \forall x \le s.\)

因此函数 u 满足

\(\begin{aligned} u(x) &= M(u)(x), \forall x \le s \\ u(x) &= T(u)(x), \forall x \ge s \end{aligned}\)

因此，剩下要证明的是

\(\begin{aligned} u(x) \le T(u)(x), \forall x \le s \\ u(x) \le M(u)(x), \forall x \ge s \end{aligned}\)

用 H 表示，第一个不等式等于 $g_s(x) \ge 0, \forall x \le s$。这是成立的，因为 $\mu(\xi) < 0, \forall x \le \xi < s < S$。第二个不等式更复杂。用 H 表示，它等于

(9.2.27)
\( H(x) \le K + \inf_{\eta \ge x} H(\eta), \forall x \ge s. \)

要证明 (9.2.27) 我们首先注意到，对于 x \ge s 我们有 \inf_{\eta \ge x} H(\eta) \ge \inf_{\eta \ge s} H(\eta) \ge -K。所以不等式每当 H(x) \le 0 时肯定成立。然后考虑称为 x_0 的最小数，使得 H 变为正。我们有

\( H(x_0) = 0, H(x) < 0 \quad \forall x, s < x < x_0. \)

我们可以声称 $g_s(x_0) > 0$。这从关系 $g_s(x_0) = -\alpha E H(x_0 - D)$ 和 x_0 的定义所导出的性质中得出。为了继续，我们注意到关系 (9.2.15) 意味着

\( H(x) = g_s(x) + \alpha E H(x - D), \)

这对任何 x 成立，只要我们在 x \le 0 时通过将 H 的定义扩展为 0。

