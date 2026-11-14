

过程 $x_t$ 是可观测的。

证明。库存位置可观测的事实直接从其定义得出。第二个关系来自

$x_t = y_{\beta_t} + \sum_{j=\beta_t}^{t-1} v_j$

$y_t = y_{\beta_t} + \sum_{j=\beta_t}^{t-1} v_j - \sum_{j=\beta_t}^{t-1} D_j$

要证明第一个，首先注意

$z_{t+1} - z_t = y_{\beta_{t+1}} - y_{\beta_t}$

$= \sum_{j=\beta_t}^{\beta_{t+1}-1} (v_j - D_j), \text{if } \beta_t < \beta_{t+1}$

通过考虑所有情况，(13.4.7) 很容易得出。

现在考虑一期成本

$c(x, v) = C(v) + l(x),$

其中

$C(v) = K \mathbf{1}_{v>0} + cv, l(x) = hx^+ + px^-,$

以及一个控制

$V = (v_1, \cdots, v_t, \cdots), v_t \text{ is } \mathcal{Z}^t \text{ measurable.}$

目标函数是

$J(V) = E \sum_{t=1}^{\infty} \alpha^{t-1} c(y_t, v_t),$

从 (13.4.8) 得到

$c(y_t, v_t) = c \left( x_t - \sum_{j=\beta_t}^t D_j, v_t \right) = C(v_t) + l \left( x_t - \sum_{j=\beta_t}^t D_j \right),$

其中当 $\beta_t = t$ 时求和消失。过程 $\beta_t$ 与需求过程独立。由于需求是独立随机变量，很容易检查 $D_{\beta_t}, \cdots, D_t$ 与 $\mathcal{Z}^t$ 独立。因此，如果我们引入如下记号

$l^{(i)}(x) = E l \left( x - \sum_{j=1}^i D_j \right), i \ge 1, l^{(0)}(x) = l(x),$

那么我们可以将目标函数重写为

(13.4.9) \( J(V) = E \sum_{t=1}^{\infty} \alpha^{t-1} (C(v_t) + l^{(t-\beta_t)}(x_t)). \)

这种写法的重要属性在于三个过程 $x_t, v_t, \beta_t$ 都是 $\mathcal{Z}^t$ 可测的。然而 $\beta_t$ 不是马尔可夫链，因此用这个过程不方便。我们将引入一个新的马尔可夫链，从中可以轻松推导出 $\beta_t$。

### 13.4.3. 新马尔可夫链。

我们引入日历时间，即在 $t$ 之前观察到延迟的最大时间。因此

$\tau_t = \max_{1 \le j \le t} \{j : \beta_{j-1} < \beta_j\},$

因此

$\beta_{\tau_t} = \tau_t - \theta_{\tau_t};$  
$\beta_{\tau_t+1} = \dots = \beta_t = \beta_{\tau_t}.$

我们然后设置

$\sigma_t = t - \tau_t, \quad \eta_t = \theta_{\tau_t},$

因此，对 $\beta_t, \tau_t$ 可以通过公式从对 $\sigma_t, \eta_t$ 轻松推导

(13.4.10)  
$\beta_t = t - \sigma_t - \eta_t, \quad \tau_t = t - \sigma_t.$

由于 $\beta_t \ge t - \theta_t$，我们得到 $\sigma_t + \eta_t \le \theta_t, \sigma_t \ge 0, \eta_t \ge 0$。因此过程 $\sigma_t, \eta_t$ 取值于 $\mathcal{M} \times \mathcal{M}$。而且

$\sigma_t + \eta_t \le M, \quad \sigma_t \le t - 1.$

重要结果是

**提议 13.5。** 对 $\sigma_t, \eta_t$ 是在状态空间 $\mathcal{M} \times \mathcal{M}$ 上的马尔可夫链，具有性质 $\sigma_t + \eta_t \le M$。它是相对于滤流 $\mathcal{Z}^t$ 的过程。

证明。我们首先定义转移。假设 $\sigma_t = \sigma, \eta_t = \eta$，其中 $\sigma, \eta$ 是两个满足 $\sigma \ge 0, \eta \ge 0, \sigma + \eta \le M$ 的数。假设 $\sigma + \eta = M$。那么如果 $\beta_{t+1} = \beta_t$，我们有

$\tau_{t+1} = \tau_t = t - \sigma, \quad \sigma_{t+1} = t + 1 - \tau_{t+1} = \sigma + 1.$

另一方面 $\eta_{t+1} = \eta$ 且我们得到 $\sigma_{t+1} + \eta_{t+1} = M + 1$，这是不可能的。因此 $\beta_{t+1} > \beta_t$，这意味着 $\tau_{t+1} = t + 1$，因此 $\sigma_{t+1} = 0$。变量 $\eta_{t+1}$ 可以取值 $0, \cdots, M$。接下来假设 $\sigma + \eta < M$。我们可能有 $\beta_{t+1} = \beta_t$，在这种情况下 $\sigma_{t+1} = \sigma + 1$ 且 $\eta_{t+1} = \eta$。否则 $\beta_{t+1} > \beta_t$，这意味着 $\sigma_{t+1} = 0$。但此时

$\eta_{t+1} = t + 1 - \beta_{t+1} < t + 1 - \beta_t = \sigma + \eta + 1.$

因此 $\eta_{t+1}$ 可以取值 $0, \cdots, \sigma + \eta$。转移总结如下：

如果 $\sigma + \eta < M$

(13.4.11)  
$\sigma, \eta \Rightarrow \begin{cases} \sigma' = \sigma + 1, \eta' = \eta \\ \sigma' = 0, \eta' = k, \quad 0 \le k \le \sigma + \eta \end{cases}$

如果 $\sigma + \eta = M$

(13.4.12)  
$\sigma, \eta \Rightarrow \sigma' = 0, \eta' = k, \quad 0 \le k \le M$

我们现在可以定义转移概率矩阵。我们首先注意到 $\theta_{t-\sigma} = \eta$，且

$\beta_{\tau_t+1} = t - \sigma - \eta = \max(t - \sigma + 1 - \theta_{\tau_t+1}, \beta_{\tau_t})$  
$= \max(t - \sigma + 1 - \theta_{t-\sigma+1}, t - \sigma - \eta),$

由此可得 $\theta_{t-\sigma+1} \ge \eta + 1$。类似地

$\theta_{t-\sigma+2} \ge \eta + 2, \cdots, \theta_t \ge \eta + \sigma.$

因此如果 \(\sigma + \eta < M\)，我们有

\(P(\sigma_{t+1} = \sigma + 1, \eta_{t+1} = \eta | \sigma_t = \sigma, \eta_t = \eta)\)
\(= P(\beta_t \ge t + 1 - \theta_{t+1} | \sigma_t = \sigma, \eta_t = \eta)\)
\(= P(\theta_{t+1} \ge \sigma + \eta + 1 | \theta_{t-\sigma} = \eta, \theta_{t-\sigma+1} \ge \eta + 1, \cdots, \theta_t \ge \eta + \sigma)\)

接下来对于 \(0 \le k \le \sigma + \eta\)

\(P(\sigma_{t+1} = 0, \eta_{t+1} = k | \sigma_t = \sigma, \eta_t = \eta)\)
\(= P(\beta_{t+1} = t + 1 - \theta_{t+1}, \theta_{t+1} = k | \sigma_t = \sigma, \eta_t = \eta)\)
\(= P(\theta_{t+1} = k | \theta_{t-\sigma} = \eta, \theta_{t-\sigma+1} \ge \eta + 1, \cdots, \theta_t \ge \eta + \sigma)\)

我们然后定义函数 \(\gamma(k; \sigma, \eta)\)，其参数为 \(0 \le k \le M, \sigma + \eta \le M, \sigma \ge 0, \eta \ge 0, \sigma \le t-1\)

(13.4.13) \(\gamma(k; \sigma, \eta) = P(\theta_{t+1} = k | \theta_{t-\sigma} = \eta, \theta_{t-\sigma+1} \ge \eta + 1, \cdots, \theta_t \ge \eta + \sigma)\)

该函数由马尔可夫链 \(\theta_t\) 及其转移概率函数唯一确定。事实上，它可以通过递归定义

(13.4.14) \(\gamma(k; \sigma, \eta) = \frac{\sum_{j=\sigma+\eta}^M p_{jk}(j; \sigma-1, \eta)}{\sum_{j=\sigma+\eta}^M \gamma(j; \sigma-1, \eta)}, \sigma \ge 1; \gamma(k; 0, \eta) = p_{\eta k}\)

马尔可夫链 $\sigma_t, \eta_t$ 的转移概率矩阵由以下给出：

如果 $\sigma + \eta < M$

(13.4.15) \(\pi(\sigma, \eta; \sigma', \eta') = \begin{cases} \gamma(k; \sigma, \eta), & \text{if } \sigma' = 0, \eta' = k, 0 \le k \le \sigma + \eta \\ \sum_{k=\sigma+\eta+1}^M \gamma(k; \sigma, \eta), & \text{if } \sigma' = \sigma + 1, \eta' = \eta \\ 0, & \text{otherwise} \end{cases}\)

如果 $\sigma + \eta = M$

(13.4.16) \(\pi(\sigma, \eta; \sigma', \eta') = \begin{cases} \gamma(k; \sigma, \eta), & \text{if } \sigma' = 0, \eta' = k, 0 \le k \le M \\ 0, & \text{otherwise} \end{cases}\)

$\sigma_t, \eta_t$ 相对于 $\mathcal{Z}^t$ 可适应的事实源于过程的定义。

事实上，马尔可夫链 $\sigma_t, \eta_t$ 从 $t=1$ 开始不是平稳的，因为约束 $\sigma_t \le t-1$。它从 $t \ge M+1$ 开始变得平稳。在后续内容中，我们将舍弃这个暂态阶段，并认为从一开始就处于平稳情况。从 (13.4.7) 和 (13.4.9) 我们可以写出

(13.4.17) \(J(V) = E \sum_{t=1}^\infty \alpha^{t-1} (C(v_t) + [l^{\sigma_t, \eta_t}(x_t)]),\)

以及

(13.4.18) \(x_{t+1} = x_t + v_t - \mathbb{I}_{\sigma_{t+1} + \eta_{t+1} \le \sigma_t + \eta_t} \sum_{j=\sigma_t + \eta_t + 1}^{\sigma_t + \eta_t} D_{t,j}\)

其中我们设置 $D_{t,j} = D_{t-j}$。存在一个暂态期，其中 $\sigma_t + \eta_t < t$。当 $t \ge M+1$ 时结束。在 (13.4.18) 中，随机变量 $D_{t,j}$ 同分布，独立于 $\mathcal{Z}^t$ 且相互独立。我们舍弃暂态期，并在 (13.4.17)、(13.4.18) 中从 $t=1$ 考虑马尔可夫链 $\sigma_t, \eta_t$，并通过以下方式固定初始条件

(13.4.19) \(x_1 = x, \sigma_1 = \sigma, \eta_1 = \eta, \sigma, \eta \ge 0, \sigma + \eta \le M\)

我们然后将函数 \( J(V) \) 称为 \( J_{x,\sigma,\eta}(V) \)，以强调初始条件。我们定义

(13.4.20) \( u(x, \sigma, \eta) = \inf_V J_{x,\sigma,\eta}(V) \).

如果 \( M=0 \)，则 \( \sigma_t = 0, \eta_t = 0\)，问题退化为第 9 章第 9.3 节中研究的无信息延迟的标准问题。

### 13.4.4. 动态规划。

与值函数 (13.4.20) 相关的贝尔曼方程很容易写出。我们将按以下方式写出

(13.4.21) \( u(x; \sigma, \eta) = -cx + l^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ K \mathbf{1}_{y > x} + cy \right. \left. + \alpha \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta) u^{(\sigma+\eta+1-k)}(y, 0, k) + \sum_{k=\sigma+\eta+1}^{M} \gamma(k; \sigma, \eta) u(y; \sigma+1, \eta) \right\} \)

其中当 \( \sigma + \eta = M \) 时最后一项求和被舍去。以等价且方便的方式写出此方程为

(13.4.22) \( u(x; \sigma, \eta) = -cx + l^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ K \mathbf{1}_{y \ge x} + cy + \alpha E u^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\} \)

其中括号中的期望是指随机变量 \( \sigma', \eta'\)，其概率分布为 \( \pi(\sigma, \eta; \sigma', \eta')\)，其中 \( \sigma, \eta\) 固定。

### 定理 13.2。我们假设

(13.4.23) \( c(1 - \alpha) - \alpha p < 0, \)

那么 (13.5.9) 的解在空间 \( B_1 \) 中是唯一的，连续，当 \( |x| \to \infty \) 时趋于 \( +\infty\)，并且是 \( K\)-凸的。最优反馈由 \( s(\sigma, \eta)\)、\( S(\sigma, \eta)\) 策略定义。

证明。证明使用第 9 章的方法，此处不再重复。

## 13.5. 带信息延迟的遍历控制

我们想在这里研究 \( \alpha \to 1\) 的情况。我们遵循文献 [7]。

### 13.5.1. 遍历性质

马尔可夫链 \( \theta_t \) 我们对以下内容做出假设

(13.5.1) \( \varpi_0 = \min_{j \in M} p_{j0} > 0. \)

该假设保证马尔可夫链 \( \theta_t \) 是遍历的，参见第 3 章，公式 (3.6.8)。我们将推导出

### 提议 13.6。假设 (13.5.1)，则马尔可夫链 \( \sigma_t, \eta_t \) 是遍历的。

证明。只需证明

(13.5.2) \( \min_{\sigma, \eta} \pi(\sigma, \eta; 0,0) > 0. \)

但是

\( \pi(\sigma, \eta; 0,0) = \gamma(0; \sigma, \eta), \)

