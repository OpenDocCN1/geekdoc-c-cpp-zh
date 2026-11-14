

令 \(\mu_\alpha(x) = g'_\alpha(x)\)，则

(10.2.5) \(H_{\alpha, s}(x) = \int_s^x \Gamma_\alpha(x - \xi) \mu_\alpha(\xi) d\xi,\)

其中 \(\Gamma_\alpha(x)\) 是更新方程的解

(10.2.6) \(\Gamma_\alpha(x) = 1 + \alpha \int_0^x f(x - \xi) \Gamma_\alpha(\xi) d\xi.\)

我们定义函数 \(S_\alpha(s)\) 使得

(10.2.7) \(\inf_{\eta \ge s} H_{\alpha, s}(\eta) = H_{\alpha, s}(S_\alpha(s)),\)

且对 \(s_\alpha, S_\alpha\) 由关系式定义

(10.2.8) \(\inf_{\eta \ge s_\alpha} H_{\alpha, s_\alpha}(\eta) + K = 0, \quad S_\alpha = S_\alpha(s_\alpha).\)

我们知道

(10.2.9) \(0 \le s_\alpha \le \bar{s}_\alpha,\)

其中

(10.2.10) \(c(1 - \alpha) + \alpha h - (p - \alpha(c - h))\bar{F}(\bar{s}_\alpha) = 0.\)

最后

(10.2.11) \(u_\alpha(x) = H_{\alpha, s_\alpha}(x) + (h - c)x + \frac{g_\alpha(s_\alpha)}{1 - \alpha}.\)

我们希望研究当 \(\alpha \uparrow 1\) 时 \(u_\alpha(x)\) 的行为。

## 10.2.2. 收敛.

我们做如下假设

(10.2.12) \(F(x) < 1, \forall x.\)

得益于假设 (10.2.12)，函数 \(\Gamma_\alpha(x)\) 收敛到 \(\Gamma(x)\)，其中

\(\Gamma(x) = \sum_{n=0}^\infty F^{(n)}(x).\)

我们注意到

\(\Gamma(x) \le \frac{1}{1 - F(x)};\)

且 \(\Gamma(x)\) 是更新方程的解

(10.2.13) \(\Gamma(x) = 1 + \int_0^x f(x - \xi) \Gamma(\xi) d\xi.\)

接下来有

(10.2.14) \(\mu_\alpha(x) \to \mu(x) = h - (p - c + h)\bar{F}(x).\)

同样

(10.2.15) \(\begin{aligned} g_\alpha(x) \to g(x) &= hx + p\bar{D} - (p - c + h) \int_0^x \bar{F}(\xi) d\xi \\ &= hx + (c - h)D + (p - c + h)E(x - D)^- \end{aligned}\)

函数

(10.2.16) \(H_{\alpha, s}(x) \to H_s(x) = \int_s^x \Gamma(x - \xi) \mu(\xi) d\xi.\)

假设 (9.2.12)，我们定义 \(\bar{s}\) 使得 \(\mu(\bar{s}) = 0\)，且 \(\mu(s) < 0, \forall 0 \le s < \bar{s}\)，\(\mu(s) > 0, \forall s > \bar{s}\)。

**引理 10.1.** 对 \(x \ge s\) 的 \(H_s(x)\) 的最小值在严格大于 \(\bar{s}\) 的点处取得。而且 \(\min_{x \ge s} H_s(x) < 0\)。

证明. 与对 \(H_{\alpha,s}(x)\) 所做的不同，我们不能依赖于 \(H_{\alpha,s}(x) \to +\infty\) 当 \(x \to +\infty\) 的事实。这是因为 \(\Gamma(x)\) 不像 \(\Gamma_\alpha(x)\) 那样先验有界。对于 \(s < \bar{s}\)，我们可以假设 \(s \le \bar{s}_\alpha\)。因此我们有

\(s \le \bar{s}_\alpha < S_\alpha(s) < S_\alpha(0).\)

回顾

\(\Gamma_\alpha(S_\alpha(0)) = \frac{p - \alpha(c - h)}{p - \alpha(p - h)},\)

我们可以断言 \(S_\alpha(0) \to S(0)\) 是

(10.2.17) \(\Gamma(S(0)) = \frac{p - c + h}{h}.\)

的解。因此我们可以提取 \(S_\alpha(s)\) 的一个子序列，它收敛到 \(S^*_s\)。显然 \(s < \bar{s} \le S^*_s \le S(0)\)。

显然 \(H_{\alpha,s}(S_\alpha(s)) \to H_s(S^*_s)\)。由于 \(H_{\alpha,s}(S_\alpha(s)) \le H_{\alpha,s}(x), \forall x \ge s\)，我们也得到 \(H_s(S^*_s) \le H_s(x), \forall x \ge s\)。因此 \(H_s(S^*_s) = \inf_{x \ge s} H_s(x)\)。所以下确界被取得。由于 \(H_s(\bar{s}+) < 0\)，下确界不在 \(s\) 处取得且严格为负。注意 \(S^*_s\) 是方程的解

(10.2.18) \(\Gamma(S - s)\mu(s) + (p - c + h) \int_s^{S^*} \Gamma(S - \xi) f(\xi) d\xi = 0,\)

因此如果 \(s < \bar{s}\)，我们不能有 \(S^*_s = s\)。

我们然后唯一地定义最小值，称为 \(S(s)\) 且 \(S(s) > \bar{s}\)。而且 \(S(s) = s, \forall s \ge \bar{s}\)。

我们又有

\(\frac{d}{ds} H_s(S(s)) = -\Gamma(S(s) - s)\mu(s) > 0, 0 \le s < \bar{s}.\)

函数 \(H_s(S(s))\) 从 \(H_0(S(0))\) 增加到 0，当 \(s\) 从 0 到 \(\bar{s}\)。

假设

(10.2.19) \(H_0(S(0)) < -K,\)

则存在唯一的 \(s\) 使得

(10.2.20) \(H_s(S(s)) = -K.\)

**定理 10.2.** 我们假设 (9.2.12), (10.2.12), (10.2.19)，则我们有

(10.2.21) \(s_\alpha \to s, \quad S_\alpha \to S;\)

(10.2.22) \(u_\alpha(x) = \frac{g_\alpha(s_\alpha)}{1-\alpha} \to u(x) = H(x) + (h-c)x.\)

**证明.** 我们再次使用 \(S_\alpha(s)\) 是递减的事实，见命题 9.3。因此 \(S_\alpha = S_\alpha(s_\alpha) \le S_\alpha(0)\)，它保持有界。我们有 \(S_\alpha(0) \to S(0) = S_0\)（为了简化记号）。而且 \(H_\alpha(0, S_\alpha(0)) \to H_0(S_0)\)。因此，从假设 (10.2.19)，我们可以假设，对于 \(\alpha\) 足够接近 1，\(H_\alpha(0, S_\alpha(0)) < -K\)。因此对 \(s_\alpha, S_\alpha\) 定义良好，且这些数保持有界。所以我们可以提取一个收敛到 \(s^*, S^*\) 的子序列。从 \(H_\alpha(x)\) 的表达式，我们容易推断出 \(H_{\alpha, s_\alpha}(S_\alpha) = -K \to H_{s^*}(S^*)\)。由此得到 \(s^* = s, S^* = S\)，由方程 (10.2.20), (10.2.18) 定义。

我们注意到

(10.2.24) \(g(x) = hx + p \int_x^\infty F(\xi) d\xi + (c-h) \int_0^x F(\xi) d\xi,\)

所以它是正函数，得益于假设 (9.2.12)。因此 \(\rho > 0\)。显然 \((1-\alpha)u_\alpha(x) - g_\alpha(s_\alpha) \to 0, \text{ 当 } \alpha \uparrow 1,\)

因此

\((1-\alpha)u_\alpha(x) \to \rho = g(s).\)

我们回顾我们还有

\(H(x) + \rho = g(x) + EH((x-D)^+), \forall x \ge s; H(x) = 0, \forall x \le s,\)

其中 \(H(x) = H_s(x)\)，由 (10.2.16) 定义，针对特定的 \(s\)，即 \(s_\alpha\) 的极限。让我们检查这些条件是否可以总结为

(10.2.25) \(H(x) + \rho = + \inf_{\eta \ge x} [K \mathbf{1}_{\eta > x} + g(\eta) + EH((\eta - D)^+)].\)

如果 (10.2.25) 满足，那么 \(u\) 的方程 (10.2.23) 立即得出，使用 \(g(x)\) 的定义。

让我们检查 (10.2.25)。首先取 \(x \le s\)。那么 \(H(x) = 0\)。如果我们表示 (10.2.25) 的右边，那么我们必须考虑 \(\eta = x\) 和 \(\eta > x\) 的情况。对于 \(\eta = x\) 我们有

\(-\rho + g(x) + EH((x-D)^+) = g(x) - g(s) > 0,\)

因为 \(x < s < \bar{s}\)。另一方面对于 \(x < \eta < s\) 我们有

\(-\rho + K + g(\eta) + EH((\eta - D)^+) = -\rho + K + g(\eta),\)

它是递减的。因此

\(-\rho + K + \inf_{\eta \ge x} [g(\eta) + EH((\eta - D)^+)]\)
\(= -\rho + K + \inf_{\eta \ge x} [g(\eta) + EH((\eta - D)^+)]\)
\(= -\rho + K + \inf_{\eta \ge x} [H(\eta) + g(s)] = 0.\)

因此 (10.2.25) 对 \(x \le s\) 得到验证。假设 \(x > s\)。那么

(10.2.26) \(-\rho + \inf_{\eta \ge x} [K \mathbf{1}_{\eta > x} + g(\eta) + EH((\eta - D)^+)] = \inf_{\eta \ge x} [K \mathbf{1}_{\eta > x} + H(\eta)].\)

但是，从 (12.5.3) 我们有，记 \(H_\alpha(x) = H_{\alpha, s_\alpha}(x)\)

\(H_\alpha(x) \le K + \inf_{\eta \ge x} H_\alpha(\eta), \forall x \ge s_\alpha.\)

但是 \( H_{\alpha, s_\alpha}(x) \to H(x) \)。我们取极限并得到

\( H(x) \le K + \inf_{\eta \ge x} H(\eta), \forall x \ge s \)

并且 (10.2.26) 的右边是 \( H(x) \)。这完成了定理的证明。

## 10.2.3. 概率解释.

我们现在给出 \(\rho\) 和 (10.2.23) 的解 \(u(x)\) 的解释。我们首先将 \(s, S\) 策略与一个不变量度 \(m_{s, S}(dx)\) 关联起来。而且方程 (10.2.23), (10.2.25) 中的下确界由与 \(s, S\) 策略关联的反馈 \(\hat{v}(x)\) 取得。我们仍将其记为 \(s, S\) 以节省记号。

注意到以下内容很方便

(10.2.27) \( l(x, v) = p\bar{D} + (h - p)x + \mathbb{I}_{v > 0}(K + (c - p)v) + pE(x + v - D)^+, \text{和} \)

和

(10.2.28) \( l(x, \hat{v}(x)) = p\bar{D} + (h - p)x + \mathbb{I}_{x \le S}(K + (c - p)(S - x)) + p[\mathbb{I}_{x \le S}E(S - D)^+ + \mathbb{I}_{x > S}E(x - D)^+], \)

并且 (10.2.23) 读作

(10.2.29) \( u(x) = l(x, \hat{v}(x)) - \rho + Eu(x + \hat{v}(x) - D). \)

让我们用 \( m_{h_c(x)}(dx) \) 表示不变量度 \( m_{s, S}(dx) \)，为了记号的一致性。从 (10.2.29) 得出

(10.2.30) \( \rho = \int l(x, \hat{v}(x))m_{h_c(x)}(dx). \)

注意 \( m_{h_c(x)}(dx) \) 的状态空间是 \( [0, S] \) 但可以取为 \( [0, \infty) \) 以使用固定状态空间。现在定义反馈集合 \( \mathcal{U}_b \) 使得

(10.2.31) \( \mathcal{U}_b = \{v(.) \ge 0 | \exists M \text{ 使得 } x + v(x) \le \max(x, M)\} . \)

如果 \( v(.) \in \mathcal{U}_b \)，必然 \( v(x) = 0 \)，如果 \( x \ge M \)。由反馈 \( v(.) \) 控制的马尔可夫链是遍历的，状态空间为 \( [0, M] \)。我们用 \( m_{v(.)}(dx) \) 表示相应的不变量度。注意由 \( s, S \) 策略定义的反馈属于 \( \mathcal{U}_b \)。我们然后有

**定理 10.3.** 我们做定理 10.2 的假设。我们有

(10.2.32) \( \rho = \inf_{v(.) \in \mathcal{U}_b} \int l(x, v(x))m_{v(.)}(dx), \)

并且存在一个由 \( s, S \) 策略定义的最优反馈。这个 \( s, S \) 策略已在定理 10.2 中定义。

证明. 考虑 \( \mathcal{U}_b \) 中的一个反馈 \( v(.) \)。从 (10.2.23) 我们可以陈述

(10.2.33) \( u(x) + \rho \le l(x, v(x)) + Eu(x + v(x) - D)^+. \)

对不变量度 \( m_{v(.)}(dx) \) 积分得到

\( \rho \le \int l(x, v(x))m_{v(.)}(dx). \)

考虑到 (10.2.30) 结果立即得出。

