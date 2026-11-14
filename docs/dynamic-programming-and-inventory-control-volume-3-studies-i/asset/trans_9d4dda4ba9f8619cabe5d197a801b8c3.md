

因此，来自遍历理论

(13.5.37)
\[
\left| \Gamma_\alpha(\sigma, \eta) - \frac{\rho_\alpha}{1-\alpha} \right|.
\]

我们可以陈述如下

### 定理 13.4.
我们采用定理 13.3 的假设。存在一个序列 \(\rho_\alpha\)，使得当 \(\alpha \to 1\) 时，对于一个子序列

(13.5.38)
\[
u_\alpha(x; \sigma, \eta) - \frac{\rho_\alpha}{1-\alpha} \to u(x; \sigma, \eta),
\]

在 \(R\) 的任何紧集上一致收敛。我们还有 \(\rho_\alpha \to \rho\)。函数 \(u(x; \sigma, \eta)\) 是局部 Lipschitz 连续的，并满足

\[
|u'(x; \sigma, \eta)| \le \frac{C}{F((x+m_0)^+)}
\]

对 \(u(x; \sigma, \eta), \rho\) 满足

(13.5.39)
\[
u(x; \sigma, \eta) + \rho = -cx + l^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ K \mathbb{1}_{y > x} + cy + \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta) u^{(\sigma+\eta+1-k)}(y; 0, k) + \sum_{k=\sigma+\eta+1}^M \gamma(k; \sigma, \eta) u(y; \sigma+1, \eta) \right\}
\]

### 证明.
我们再次定义

\[
\bar{u}_\alpha(x; \sigma, \eta) = u_\alpha(x; \sigma, \eta) - \frac{\rho_\alpha}{1-\alpha},
\]

然后我们得到方程

\[
\bar{u}_\alpha(x; \sigma, \eta) + \rho_\alpha = -cx + l^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ K \mathbb{1}_{y > x} + cy + \alpha E \bar{u}^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\}
\]

由于下确界在 \(\max(x, S A_\alpha(\sigma, \eta))\) 处取得，我们可以认为若 \(x < X\) 则 \(y < L_X\)。因此我们还有

(13.5.40)
\[
\bar{u}_\alpha(x; \sigma, \eta) + \rho_\alpha = -cx + l^{(\sigma+\eta)}(x) + \inf_{L_X \ge y \ge x} \left\{ K \mathbb{1}_{y > x} + cy + \alpha E \bar{u}^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\}.
\]

假设 \(|x| < X\)，利用提议 13.9 和引理 13.3 的估计，并应用 Ascoli-Arzelà 定理，我们可以提取一个子序列，使得

\[
\sup_{|x|<X} |\bar{u}_\alpha(x; \sigma, \eta) - u(x; \sigma, \eta)| \to 0
\]

并且我们可以对 (13.5.40) 取极限以得到

\[
\begin{aligned}
u(x; \sigma, \eta) + \rho &= -cx + l^{(\sigma+\eta)}(x) + \inf_{L_X \ge y \ge x} \left\{ K \mathbb{1}_{y > x} + cy + \alpha E u^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\} \\
&\ge -cx + l^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ K \mathbb{1}_{y > x} + cy + \alpha E u^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\}.
\end{aligned}
\]

但相反的不等式可以轻易验证。结果随之得出。

考虑成本泛函

\[
J_{x, \alpha, \eta}^s(V) = E \sum_{t=1}^{\infty} \alpha^{t-1} (C(v_t) + l^{(\sigma_t + \eta_t)}(x_t)),
\]

那么我们将有

(13.5.41)
\[
\rho = \inf_V \lim_{\alpha \to 1} (1 - \alpha) J_{x, \alpha, \eta}^s(V)
\]

仅考虑极限存在的控制策略 \(V\)。然后下确界在由 \(s(\sigma, \eta)\)、\(S(\sigma, \eta)\) 策略表征的 \(V\) 处取得，其中

\[
s(\sigma, \eta) = \lim_{\alpha \to 1} s_\alpha(\sigma, \eta), \quad S(\sigma, \eta) = \lim_{\alpha \to 1} S_\alpha(\sigma, \eta)
\]

## 连续时间库存控制

## 14.1. 确定性模型

### 14.1.1. 连续时间冲动控制

我们描述一个连续时间模型。冲动控制是一系列时刻

\[
\theta_1 < \theta_2 < \cdots < \theta_n \cdots,
\]

在此时刻我们做出决策

\[
v_1 < v_2 < \cdots v_n \cdots .
\]

时刻 \(\theta_n\) 将是我们决定补充库存的时刻，而 \(v_n\) 将是补充水平。在这个确定性框架中，这些数字是确定性的。我们用 \(V\) 表示时刻和水平的序列，并称 \(V\) 为冲动控制。

设 \(y(t) = y_x(t; V)\) 为时刻 \(t\) 的库存状态，初始时刻 0 的初始状态为 \(x\)，并受冲动控制 \(V\) 约束。

我们有

\[
y(t) = x - \lambda t + M(t),
\]

其中

\[
M(t) = M(t; V) = \sum_{\{n|\theta_n < t\}} v_n.
\]

这些关系的含义很明确：\(x > 0\) 是初始库存，\(\lambda t\) 是截至时刻 \(t\) 的需求，\(M(t)\) 表示截至时刻 \(t\) 的总补充量。由于不允许短缺，我们施加状态约束 \(y(t) \ge 0\)。我们定义成本函数如下

\[
J_x(V) = \sum_{n=0}^\infty (K + c v_n) \exp -a\theta_n + \int_0^\infty hy(t) \exp -\alpha t dt.
\]

像往常一样，我们通过以下方式定义值函数

\[
u(x) = \inf_V J_x(V).
\]

反馈是一种决策规则，它在任何时刻 \(t\) 定义作为该时刻系统状态函数的待采取决策。在我们的情况中，在任何时刻 \(t\)，查看库存值 \(y(t)\) 后，我们决定下订单并决定订购数量。

### 14.1.2. s, S 策略

s, S 策略是一对数字，满足

\[
s \le S,
\]

这样从这两个数字可以得到如下反馈：

\[
v(x) = v_{s,S}(x) = \begin{cases} S - x, & \text{if } x \le s \\ 0, & \text{if } x > s \end{cases}
\]

反馈用于按如下方式计算冲动控制 \(V = V_{s,S}\)：在任何时刻 \(t\)，如果 \(x(t) \le s\)，则订购数量

\[
v(t) = S - x(t).
\]

如果

\[
x(t) > s,
\]

则在时刻 \(t\) 不下订单。我们称

\[
u_{s,S}(x).
\]

与一对 \(s, S\) 相关的值函数。即

\[
u_{s,S}(x) = J_x(V_{s,S}).
\]

### 14.1.3. 不等式

很容易验证 \(u(x)\) 满足的不等式。回顾 \(x\) 表示初始时刻的状态（库存水平）。如果我们强制在初始时刻做出订购数量 \(v\) 的决策，那么我们支付 \(K + cv\)，状态变为 \(x + v\)。如果从现在开始最优进行，我们能达到的最佳结果是

\[
K + cv + u(x + v).
\]

因此我们可以断言

(14.1.1)
\[
u(x) \le K + \inf_{v>0} (cv + u(x + v)).
\]

下一个不等式在于检查初始时刻不订购的决策。因此我们将决策推迟一小段时间 \(\delta\)。在此期间，我们首先支付持有成本 \(\delta h x\)，然后在时刻 \(\delta\) 时库存为

\[
x - \delta \lambda.
\]

对于小 \(\delta\)，这个数为正。假设从现在开始我们表现最优。对于寿命期 \((\delta, \infty)\)，我们能获得的最佳结果是

\[
u(x - \delta \lambda).
\]

我们对该数量进行贴现以得到时刻 0 的值。由于 \(\delta\) 很小，我们有近似值

\[
(1 - \delta \alpha) u(x - \delta \lambda).
\]

因此我们声称

\[
u(x) \le (1 - \delta \alpha) u(x - \delta \lambda) + \delta h x
\]

在 \(\delta\) 中展开我们得到

(14.1.2)
\[
\alpha u + \lambda u' \le h x, \quad x > 0
\]

下一点是声称对于任何初始库存 \(x\)，(14.1.1) 或 (14.1.2) 中至少一个成立，因为要么我们决定订购，要么我们让系统自由演化一小段时间。我们可以通过写出互补松弛条件来表达这一点

(14.1.3)
\[
(\alpha u + \lambda u' - h x)(u(x) - K - \inf_{v>0} (cv + u(x + v))) = 0 \quad \forall x > 0
\]

我们必须通过对边界和光滑性的考虑来完善条件。边界是 \(x=0\)。我们显然必须在边界处订购，否则库存将保持在 0，因为它不能为负。最终我们订购，并可以认为问题从这时开始。因此，我们可以写

(14.1.4)
\[
u(0) = K + \inf_{v>0} (cv + u(v)).
\]

关于光滑性，如果

(14.1.5)
\[
u \in C^1(0, \infty).
\]

不等式集合和互补松弛方程 (14.1.1)、(14.1.2)、(14.1.3) 以及相关的边界和光滑性条件称为 *准变分不等式*。

### 注释 14.1.
值函数 \(u(x)\) 的定义并不保证光滑性。这是一种可取的性质，远非自动成立，特别是在切换点。

现在让我们写出由 \(s, S\) 策略定义的值函数所满足的条件。注意

\[
0 \le s \le S.
\]

我们首先有

(14.1.6)
\[
u_{s,S}(x) = K + c(S - x) + u_{s,S}(S), \quad \forall x \le s.
\]

接下来

(14.1.7)
\[
\alpha u_{s,S} + \lambda u'_{s,S} - hx = 0, \quad \forall x > s.
\]

这些关系表达了 \(s, S\) 策略下的决策过程。

与定义值函数 \(u\) 的关系相比，这暗示了一种从 \(s\) 得到 \(S\) 的自然方法。让我们首先选择一个单一的正数 \(s\)，并通过以下方式定义 \(u_s(x)\)

(14.1.8)
\[
u_s(x) + cx = K + \inf_{y>s} (cy + u_y(y)), \quad x \le s
\]

(14.1.9)
\[
\alpha u_s + \lambda u'_s - hx = 0, \quad \forall x > s.
\]

那么 \(S(s)\) 简单地通过以下方式得到

(14.1.10)
\[
\inf_{y>s} (cy + u_y(y)) = cS + u_s(S)
\]

### 14.1.4. \(u_s\) 的定义

对于任何固定的 \(s\)，我们可以将微分方程 (14.1.9) 的解写成如下形式

\[
u_s(x) = u_s(s) \exp -\frac{\alpha}{\lambda}(x-s) + \frac{h}{\lambda} \int_s^x y \exp -\frac{\alpha}{\lambda}(x-y) dy,
\]

因此

(14.1.11)
\[
u_s(x) = \frac{h}{\alpha} \left( x - \frac{\lambda}{\alpha} \right) + \left( u_s(s) - \frac{h}{\alpha} s + \frac{\lambda h}{\alpha^2} \right) \exp -\frac{\alpha}{\lambda}(x-s).
\]

为了定义 \(S = S(s)\)，我们写

\[
u'_s(S) = -c,
\]

因此

\[
\alpha u_s(S) = hS + \lambda c.
\]

