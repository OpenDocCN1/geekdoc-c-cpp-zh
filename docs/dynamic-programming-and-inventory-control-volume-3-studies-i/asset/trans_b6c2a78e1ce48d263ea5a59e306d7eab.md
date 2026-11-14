

这定义了一个与以下算子相关的马尔可夫链

(12.3.4) 
\(\Phi^v \varphi(x, z) = \int_0^\infty \varphi(x + v - \zeta, c) f(\zeta | z) d\zeta,\)

因此过渡概率由以下给出

(12.3.5) 
\(\pi(x, z, v; d\xi, d\zeta) = \delta(\xi - (x + v - \zeta)) \otimes f(\zeta | z) d\zeta.\)

接下来我们定义函数

(12.3.6) 
\(l(x, v) = cv + hx^+ + px^-,\)

它将用于建模单期成本。成本函数则为

(12.3.7) 
\(J_{x,z}(V) = E \sum_{n=1}^\infty \alpha^{n-1} l(y_n, v_n).\)

我们关心的值函数为

(12.3.8) 
\(u(x, z) = \inf_V J_{x,z}(V).\)

我们再次注意到性质 (4.31)、(4.32) 得到满足。为继续，我们需要指定一个上限函数。它对应于恒等为 0 的控制。令 \(l_v(x) = l(x, v)\)。请注意不等式

\(\Phi^{x+} u^+(x, z) \le x^+, \quad \Phi^{x-} u^-(x, z) \le x^- + c_0 z + c_1.\)

很容易验证

(12.3.9) 
\((\Phi^0)^n x^+(x, z) \le x^+,\)

(12.3.10) 
\((\Phi^0)^n x^-(x, z) \le x^- + c_0 z \frac{1-c_0^n}{1-c_0} + (n - c_0(n+1) + c_0^{n+1}) \frac{c_1}{(1-c_0)^2}.\)

接下来考虑函数

(12.3.11) 
\(w_0(x, z) = \sum_{n=1}^\infty \alpha^{n-1} (\Phi^0)^{n-1} l_0(x)\)

### 引理 12.2.

我们假设

(12.3.12) 
\(\alpha c_0 < 1,\)

则级数 \(w_0(x, z) < \infty\)，更精确地说

(12.3.13) 
\(u_0(x, z) \le \frac{hx^+ + px^-}{1 - \alpha} + \frac{p c_0 z \alpha}{(1 - c_0 \alpha)(1 - \alpha)} + \frac{p c_1}{(1 - c_0)^2} \left( \frac{\alpha - c_0}{(1 - \alpha)^2} + \frac{c_0}{1 - \alpha c_0} \right).\)

证明. 这是公式 (13.2.10) 和 (12.3.9) 的直接结果。\(\square\)

接下来我们写出贝尔曼方程

(12.3.14) 
\(u(x, z) = \inf_{v \ge 0} [l(x, v) + \alpha \Phi^v u(x, z)].\)

我们陈述如下

### 定理 12.4.

我们假设 (13.2.1)、(12.3.2)、(12.3.6)、(13.2.11)。那么方程 (13.2.15) 存在唯一解，满足 \(0 \le u \le w_0\)。它是连续的，并与值函数 (12.3.8) 重合。存在一个最优反馈 \(v(x, z)\) 和一个最优控制策略 \(\bar{V}\)。

证明. 我们首先注意到定理 4.4 和 4.3 的条件得到满足。因此方程 (13.2.15) 的解集非空。它存在最小解和最大解。最小解是下半连续的，最大解是上半连续的。最小解与值函数重合。存在一个最优反馈 \(\hat{v}(x, z)\) 和一个最优控制策略 \(\hat{V}\)。为证明唯一性，我们需要证明最小解和最大解重合。我们首先从对 \(\hat{v}(x, z)\) 的界限开始证明。由 (13.2.15)，考虑 \(\underline{w}\)，即最小解，我们可以断言

(12.3.15) 
\(\underline{w}(x, z) \ge \frac{hx^+}{1-\alpha} + px^- - \frac{\alpha h c_0 z}{(1-\alpha)(1-\alpha c_0)} - \frac{\alpha h c_1}{(1-\alpha)^2},\)

这由 \(l(x, v) \ge hx^+ + px^-\) 得出，并且

(12.3.16) 
\(\Phi^{l,v}(x, z) \ge \Phi^{0,v}(x, z), \forall v \ge 0, \forall \varphi \text{ increasing in } x,\)

这意味着

\(\alpha E[\underline{w}(x+v-z_2, z_2)|z_1=z]\)
\(\ge \frac{\alpha h}{1-\alpha} E[(x-z_2)^+|z_1=z] - \frac{\alpha^2 h c_0 (c_0 z + c_1)}{(1-\alpha)(1-\alpha c_0)} - \frac{\alpha^2 h c_1}{(1-\alpha)^2}\)
\(\ge \frac{\alpha h}{1-\alpha} (x^+ - c_0 z - c_1) - \frac{\alpha^2 h c_0 (c_0 z + c_1)}{(1-\alpha)(1-\alpha c_0)} - \frac{\alpha^2 h c_1}{(1-\alpha)^2}\)

并且 (13.2.40) 得出，再次使用 (13.2.15)。因此也

(12.3.17) 
\(l(x, v) + \alpha \Phi^{\underline{w}}(x, z) \ge cv + \frac{hx^+}{1-\alpha} + px^- - \frac{\alpha h c_0 z}{(1-\alpha)(1-\alpha c_0)} - \frac{\alpha h c_1}{(1-\alpha)^2}.\)

接下来我们引入函数 \(w(x, z)\)，它是以下方程的解

(12.3.18) 
\(w(x, z) = hx^+ + (c+p)x^- + \alpha E[w(x^+-z_2, z_2)|z_1=z],\)

它对应于反馈 \(v(x) = x^-\)。我们注意到 \(\underline{w}(x, z) \le w(x, z)\)。我们可以断言

(12.3.19) 
\(w(x, z) \le (c+p)x^- + \frac{hx^+}{1-\alpha} + L_0 z + L_1,\)

其中

\(L_0 = \frac{\alpha(c+p)c_0}{1-\alpha c_0}, \quad L_1 = \frac{\alpha c_1(c+p)}{(1-\alpha)(1-\alpha c_0)}\)

因此，在对 \(v\) 求最小值时，我们可以从上方界定 \(v\) 的范围。更精确地说，我们得到

(12.3.20) 
\(\hat{v}(x, z) \le x^- + \frac{\alpha c_0 z}{c(1-c_0 \alpha)} \left( c+p + \frac{h}{1-\alpha} \right) + c \frac{\alpha c_1}{c(1-\alpha)} \left( \frac{h}{1-\alpha} + \frac{c+p}{1-c_0 \alpha} \right).\)

我们考虑从最优反馈得到的最优轨迹 \(\hat{y}_n, z_n\)，即

\(\hat{y}_{n+1} = \hat{y}_n + \hat{v}_n - z_{n+1}, \hat{v}_n = \hat{v}(\hat{y}_n, z_n)\)

其中 \(\hat{y}_1 = x, z_1 = z\)。

为证明唯一性，只需证明

(12.3.21) 
\(\alpha^n E[\hat{y}_{n+1}] \to 0, \text{ as } n \to \infty.\)

我们有

\(\hat{y}_{n+1} \le \hat{y}_n + \hat{v}_n\)
\(\le \hat{y}_n^+ + \frac{\alpha c_0 z_n}{c(1-c_0 \alpha)} \left( c+p+\frac{h}{1-\alpha} \right) + \frac{\alpha c_1}{c(1-\alpha)} \left( \frac{h}{1-\alpha} + \frac{c+p}{1-c_0 \alpha} \right)\)

因此

\(E\hat{y}_{n+1}^+ \le E\hat{y}_n^+ + \frac{\alpha \left( c_0^2 z + c_1 \frac{c_0 - c_0^2}{1-c_0} \right)}{c(1-c_0 \alpha)} \left( c+p+\frac{h}{1-\alpha} \right)\)
\(+ \frac{\alpha c_1}{c(1-\alpha)} \left( \frac{h}{1-\alpha} + \frac{c+p}{1-c_0 \alpha} \right)\)

我们推导出估计

\(E\hat{y}_{n+1}^+ \le x^+ + \frac{\alpha c_0}{c(1-c_0 \alpha)} \left( z \frac{1-c_0^n}{1-c_0} + c_1 \frac{n}{1-c_0 \alpha} - c_1 \frac{1-c_0^n}{(1-c_0)^2} \right) \left( c+p+\frac{h}{1-\alpha} \right)\)
\(+ \frac{n c_1}{c(1-\alpha)} \left( \frac{h}{1-\alpha} + \frac{c+p}{1-c_0 \alpha} \right),\)

因此 \(\alpha^n E\hat{y}_{n+1}^+ \to 0\)，当 \(n \to +\infty\)。接下来

\(\hat{y}_{n+1} \ge \hat{y}_n - z_{n+1},\)

很容易得出

\(E\hat{y}_{n+1}^- \le x^- + c_0 z \frac{1-c_0^n}{1-c_0} + \frac{c_1}{1-c_0} \left( n - c_0 \frac{1-c_0^n}{1-c_0} \right),\)

我们得到 \(\alpha^n E\hat{y}_{n+1}^- \le x^- \to 0\)，当 \(n \to +\infty\)。证明完成。

## 12.3.2. 基准库存策略.

我们现在想验证最优反馈 \(\hat{v}(x, z)\) 可以通过基准库存策略得到，其中基准库存取决于 \(z\) 的值。我们有

### 定理 12.5.

我们做出定理 12.4 的假设，且 \(p\alpha > c(1 - \alpha)\)、\(h + p - c > 0\)。还假设

(12.3.22) \(f(x)z \ge a_0(M) > 0, \forall x, z \le M.\)

那么函数 \(u(x, z)\) 在自变量 \(x\) 上是凸的且为 \(C^1\)，除了 \(x = 0\) 处，那里存在左导数和右导数。此外，最优反馈由以下给出

(12.3.23) \(\hat{v}(x, z) = \begin{cases} S(z) - x, & \text{if } x \le S(z) \\ 0, & \text{if } x \ge S(z) \end{cases}\)

其中 \(S(z) > 0\) 是一致连续的。

证明. 我们考虑递增过程

\(u_{n+1}(x, z) = \inf_{v \ge 0} [(f, v) + \alpha \Phi^n u_n(x, z)], \quad u_0(x) = 0\)

也可写成

\(u_{n+1}(x, z) = hx^+ + px^- - cx + \inf_{\eta \ge x} \{ c\eta + \alpha E[u_n(\eta - z_2, z_2)|z_1 = z] \}\)

我们递归地证明序列 \(u_n(x, z)\) 在 \(x\) 上是凸的且为 \(C^1\)，除了 \(x=0\)。我们首先有

(12.3.24) 
\(u_{n+1}(x, z) = hx^+ + px^- + \alpha E[u_n(x - z_2, z_2)|z_1 = z]\)

对于 \(0 \le n \le n_0\)，其中

\(\frac{\alpha p}{1 - \alpha}(1 - \alpha^{n_0+1}) > c > \frac{\alpha p}{1 - \alpha}(1 - \alpha^{n_0}).\)

确实，考虑由 (13.2.24) 定义的序列，我们有

\(u'_n(x, z) = -p \frac{1 - \alpha^n}{1 - \alpha}, \forall n \le n_0 + 1, \forall x < 0\)

因此 \(c - \alpha p \frac{1 - \alpha^n}{1 - \alpha} > 0\)，对所有 \(n \le n_0\) 成立，且函数 \(\alpha \eta + \alpha E[u_n(\eta - z_2, z_2)|z_1 = z]\) 是单调递增的，对所有 \(n \le n_0\) 成立。

定义

\(G_n(x, z) = cx + \alpha E[u_n(x - z_2, z_2)|z_1 = z],\)

那么函数 \(G_n(x, z)\) 对 \(n \le n_0\) 是单调递增的，并且对于 \(n = n_0 + 1\) 在 \(S_n(z) > 0\) 处取得其最小值，可以通过取最小的最小值来唯一确定。它是 \(C^1\) 且凸的（导数在 0 处连续，由数学期望的正则化效应）。

那么，对于 \(n \le n_0 + 1\)，我们有

\(u_{n+1}(x, z) = \left\{ \begin{array}{ll} hx^+ + px^- - cx + G_n(S_n(z), z) & \text{if } x \le S_n(z) \\ hx^+ + px^- - cx + G_n(x, z) & \text{if } x \ge S_n(z) \end{array} \right.\)

其中 \(S_n(z) = -\infty\)，对所有 \(n \le n_0\)。因此 \(u_n(x, z)\) 是 \(C^1\)，除了 \(x=0\)，且是凸的，对于 \(n \le n_0 + 2\)。通过递归，该性质对任何 \(n\) 都成立。

由此可知极限 \(u(x, z)\) 在 \(x\) 上是凸的。显然 \(u(x, z) \to +\infty\)，当 \(|x| \to +\infty\)。另外 \(S_n(z) > 0\)，对所有 \(n \ge n_0 + 1\)。而且

\(u'_n(x, z) = -p - c, \forall x < 0, \forall n \ge n_0 + 2\)

且 \(u'_n(x, z) \le \frac{h}{1 - \alpha}\)。因此极限 \(u(x, z)\) 在 \(x\) 上是 Lipschitz 连续的，并且

\(u'(x, z) = -p - c, \forall x < 0, \quad u'(x, z) \le \frac{h}{1 - \alpha}.\)

还

(12.3.25) 
\(-p - c \le u'(x, z) \le \frac{h}{1 - \alpha}.\)

函数

\(G(x, z) = cx + \alpha E[u(x - z_2, z_2)|z_1 = z],\)

是凸的，并且当 \(x \to +\infty\) 时趋向于 \(+\infty\)。对于 \(x < 0\)，我们有 \(G'(x, z) = c(1 - \alpha) - \alpha p < 0\)。因此 \(G(x, z)\) 的最小值在 \(S(z) > 0\) 处取得，可以通过取最小的最小值来唯一确定。

然后，由凸性

\(u(x, z) = \left\{ \begin{array}{ll} hx^+ + px^- - cx + G(S(z), z) & \text{if } x \le S(z) \\ hx^+ + px^- - cx + G(x, z) & \text{if } x \ge S(z) \end{array} \right.\)

