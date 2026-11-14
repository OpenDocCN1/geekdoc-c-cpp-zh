

## 13.5.3. 情况 $K=0$ 的极限行为

现在可以给出 (13.5.39) 的极限。

### 定理 13.3. 假设 (13.5.1) 且

$$
(13.5.17) \quad \bar{F}(x) > 0, \forall x < \infty, \quad p > c.
$$

存在一个序列 \(\rho_\alpha\)，使得当 \(\alpha \to 1$ 时，对于一个子序列

$$
(13.5.18) \quad u_\alpha(x;\sigma,\eta) - \frac{\rho_\alpha}{1-\alpha} \to u(x;\sigma,\eta),
$$

在 \(R$ 的任何紧集上一致收敛。我们还有 \(\rho_\alpha \to \rho$。函数 \(u(x;\sigma,\eta)$ 是局部利普希茨连续的，并满足

$$
|u'(x;\sigma,\eta)| \le \frac{C}{F(x)}.
$$

对 \(u(x;\sigma,\eta), \rho$ 满足

$$
(13.5.19) \quad u(x;\sigma,\eta) + \rho = -cx + \ell^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ cy + \sum_{k=0}^{\sigma+\eta} \gamma(k;\sigma,\eta) u^{(\sigma+\eta+1-k)}(y,0,k) + \sum_{k=\sigma+\eta+1}^M \gamma(k;\sigma,\eta) u(y;\sigma+1,\eta) \right\}.
$$

### 证明

考虑 \(u_\alpha(0; \sigma, \eta)$。由于 \(S_\alpha(\sigma, \eta) > 0$，我们可以写出，注意到 \(\ell^{(\sigma+\eta)}(0) = p\bar{D}(\sigma + \eta)\)

$$
\begin{aligned}
u_\alpha(0; \sigma, \eta) &= p\bar{D}(\sigma + \eta) + cS_\alpha(\sigma, \eta) \\
&\quad + \alpha \sum_{k=\sigma+\eta+1}^M \gamma(k; \sigma, \eta) u_\alpha(S_\alpha(\sigma, \eta); \sigma + 1, \eta) \\
&\quad + \alpha \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta) E u_\alpha(S_\alpha(\sigma, \eta) - D^{(\sigma+\eta+1-k, 0; k)}).
\end{aligned}
$$

令

$$
\begin{aligned}
G_\alpha(\sigma, \eta) &= u_\alpha(0; \sigma, \eta) - \alpha \sum_{k=\sigma+\eta+1}^M \gamma(k; \sigma, \eta) u_\alpha(0; \sigma + 1, \eta) \\
&\quad - \alpha \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta) u_\alpha(0; 0, k).
\end{aligned}
$$

利用 \(u_\alpha(0; \sigma, \eta)$ 的值，我们可以得出

$$
\begin{aligned}
G_\alpha(\sigma, \eta) &= p\bar{D}(\sigma + \eta) + cS_\alpha(\sigma, \eta) \\
&\quad + \alpha \sum_{k=\sigma+\eta+1}^M \gamma(k; \sigma, \eta) (u_\alpha(S_\alpha(\sigma, \eta); \sigma + 1, \eta) - u_\alpha(0; \sigma + 1, \eta)) \\
&\quad + \alpha \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta) E (u_\alpha(S_\alpha(\sigma, \eta) - D^{(\sigma+\eta+1-k, 0; k)}) - u_\alpha(0; 0, k)).
\end{aligned}
$$

利用估计 (13.5.14) 和 (13.5.15)，我们很容易推导出 \(|G_\alpha(\sigma, \eta)| \le C$。\(G_\alpha(\sigma, \eta)$ 的定义也可以写成

$$
(13.5.20) \quad u_\alpha(0; \sigma, \eta) - \alpha \sum_{\sigma', \eta'} \pi(\sigma, \eta; \sigma', \eta') u_\alpha(0; \sigma', \eta') = G_\alpha(\sigma, \eta)
$$

链 \(\pi(\sigma, \eta; \sigma', \eta')$ 是遍历的，其不变测度为 \(\mu(\sigma, \eta)$。定义

$$
\rho_\alpha = \sum_{\sigma, \eta} \mu(\sigma, \eta) G_\alpha(\sigma, \eta).
$$

由于 \(\mu(\sigma, \eta)$ 是不变的，我们还有

$$
\sum_{\sigma, \eta} \mu(\sigma, \eta) u_\alpha(0; \sigma, \eta) = \frac{\rho_\alpha}{1 - \alpha}.
$$

根据遍历理论，我们还可以断言

$$
(13.5.21) \quad \left| u_\alpha(0; \sigma, \eta) - \frac{\rho_\alpha}{1 - \alpha} \right| \le C,
$$

其中常数与 \(\alpha, \sigma, \eta$ 无关。接下来定义

$$
\bar{u}_\alpha(x; \sigma, \eta) = u_\alpha(x; \sigma, \eta) - \frac{\rho_\alpha}{1 - \alpha}.
$$

结合 (13.5.21) 和 (13.5.15)，我们可以给出以下估计

$$
(13.5.22) \quad |\bar{u}_\alpha(x; \sigma, \eta)| \le C + C \frac{|x|}{F(x)};
$$

$$
(13.5.23) \quad |(\tilde{u}_\alpha)'(x;\sigma,\eta)| \le \frac{C}{F(x)}.
$$

更一般地

$$
(13.5.24) \quad |(\tilde{u}_\alpha)^{(\beta)}(x;\sigma,\eta)| \le C + C \frac{|x| + \beta D}{F(x)};
$$

$$
(13.5.25) \quad |((\tilde{u}_\alpha)^{(\beta)})'(x;\sigma,\eta)| \le \frac{C}{F(x)}.
$$

根据 Ascoli-Arzelà 定理，我们可以找到一个子序列，使得

$$
\begin{aligned}
\rho_\alpha &\to \rho, \\
\sup_{|x| \le X} |\tilde{u}_\alpha(x;\sigma,\eta) - u(x;\sigma,\eta)| &\to 0, \\
\sup_{|x| \le X} |(\tilde{u}_\alpha)^{(\beta)}(x;\sigma,\eta) - u^{(\beta)}(x;\sigma,\eta)| &\to 0 \\
&\forall \ \sigma, \eta, \beta, X \text{ as } \alpha \to 1.
\end{aligned}
$$

根据估计 (13.5.25)，极限满足

$$
|u'(x;\sigma,\eta)| \le \frac{C}{F(x)}.
$$

回到 (13.5.27) 并回顾 \(y$ 中的下确界在 \(\max(x, S_\alpha(\sigma,\eta))$ 处取得，只要 \(x < X$，我们可以将 \(y$ 限制为 \(y \le L_X$。因此我们可以使用 \(\tilde{u}_\alpha(x;\sigma,\eta)$ 写出

$$
\begin{aligned}
\tilde{u}_\alpha(x;\sigma,\eta) + \rho_\alpha &= -cx + \ell^{(\sigma+\eta)}(x) \\
&\quad + \inf_{L_X \ge y \ge x} \left\{ cy + \alpha E \tilde{u}_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(y;\sigma',\eta') \right\},
\end{aligned}
$$

因此利用 \(R$ 紧集上的一致收敛，我们得到

$$
\begin{aligned}
u(x;\sigma,\eta) + \rho &= -cx + \ell^{(\sigma+\eta)}(x) \\
&\quad + \inf_{L_X \ge y \ge x} \left\{ cy + E u^{(\sigma+\eta+1-(\sigma'+\eta'))}(y;\sigma',\eta') \right\} \\
&\ge -cx + \ell^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ cy + E u^{(\sigma+\eta+1-(\sigma'+\eta'))}(y;\sigma',\eta') \right\}.
\end{aligned}
$$

另一方面，对于任何 \(y > x$，我们还有

$$
u(x;\sigma,\eta) + \rho \le -cx + \ell^{(\sigma+\eta)}(x) + E u^{(\sigma+\eta+1-(\sigma'+\eta'))}(y;\sigma',\eta'),
$$

因此得到了 (13.5.19)。证明完成。

考虑成本函数

$$
J^\alpha_{\sigma,\eta}(V) = E \sum_{t=1}^\infty \alpha^{t-1} (c v_t + \ell^{(\sigma+\eta_t)}(x_t)),
$$

那么我们将有

$$
(13.5.26) \quad \rho = \inf_V \lim_{\alpha \to 1} (1-\alpha) J^\alpha_{\sigma,\eta}(V),
$$

仅考虑使极限存在的控制策略 \(V$。然后下确界在由基准库存特征的 \(V$ 处取得

$$
S(\sigma,\eta) = \lim_{\alpha \to 1} S_\alpha(\sigma,\eta).
$$

## 13.5.4. 情况 \(K > 0\)。

方程写作如下

$$
(13.5.27) \quad u_\alpha(x; \sigma, \eta) = -cx + \ell^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ K \mathbb{1}_{y > x} + cy + \alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\}.
$$

解由 \(s_\alpha(\sigma, \eta)$、\(S_\alpha(\sigma, \eta)$ 策略控制。因此

$$
x \le s_\alpha(\sigma, \eta) \Rightarrow u_\alpha(x; \sigma, \eta) = -cx + \ell^{(\sigma+\eta)}(x) + K + C_{\alpha, \sigma, \eta},
$$

且

$$
x \ge s_\alpha(\sigma, \eta) \Rightarrow u_\alpha(x; \sigma, \eta) = \ell^{(\sigma+\eta)}(x) + \alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta').
$$

我们还有连续性条件

$$
C_{\alpha, \sigma, \eta} = \inf_{y > s_\alpha(\sigma, \eta)} \left\{ cy + \alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\}.
$$

函数 \(u_\alpha(x; \sigma, \eta)$ 是连续的但不是连续可微的。导数的唯一不连续点是 \(s_\alpha(\sigma, \eta)$。然而我们可以考虑不连续函数 \(u_\alpha(x; \sigma, \eta)$ 并写出

$$
u'_\alpha(x; \sigma, \eta) = -c + \ell^{(\sigma+\eta)}(x) + \chi_\alpha(x; \sigma, \eta).
$$

经过一些计算，我们可以写出方程

$$
(13.5.28) \quad \chi_\alpha(x; \sigma, \eta) = \begin{cases} \mu_\alpha^{(\sigma+\eta)}(x) + \alpha E \chi_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta'), & x \ge s_\alpha(\sigma, \eta) \\ 0, & x \le s_\alpha(\sigma, \eta) \end{cases}
$$

且

$$
(13.5.29) \quad \mu_\alpha(x) = c(1 - \alpha) + \alpha h - \alpha(h + p)\bar{F}(x).
$$

连续性条件则表示如下

$$
(13.5.30) \quad 0 = K + \inf_{y > s_\alpha(\sigma, \eta)} \int_{s_\alpha(\sigma, \eta)}^y \chi_\alpha(\xi; \sigma, \eta) d\xi
$$

如果定义

$$
(13.5.31) \quad G_\alpha(x; \sigma, \eta) = cx + \alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta'),
$$

那么我们可以写出

$$
(13.5.32) \quad u_\alpha(x; \sigma, \eta) = -cx + \ell^{(\sigma+\eta)}(x) + G_\alpha(\max(x, s_\alpha(\sigma, \eta)); \sigma, \eta),
$$

因此

$$
(13.5.33) \quad \chi_\alpha(x; \sigma, \eta) = G'_\alpha(x; \sigma, \eta) \mathbb{1}_{x > s_\alpha(\sigma, \eta)}.
$$

我们现在陈述一个重要性质

### 引理 13.2. 假设 \(\alpha p > c$。我们有以下性质

$$
\begin{aligned}
u'_\alpha(x; \sigma, \eta) &\le -(c+p)\lambda, \quad \chi'_\alpha(x; \sigma, \eta) \le 0 \quad \forall x < 0, \\
G'_\alpha(x; \sigma, \eta) &\le c(1-\alpha) - \alpha p \quad \forall x < 0.
\end{aligned}
$$

