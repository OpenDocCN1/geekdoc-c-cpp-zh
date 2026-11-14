

然而我们具有性质

$$ \int_0^{ +\infty } \Gamma (\xi ) d\xi = +\infty . $$

确实，若考虑 \(\pi < 0\)

$$ \hat{\Gamma} (\pi ) = \int_0^{ +\infty } \exp \xi \pi \Gamma (\xi ) d\xi , $$

由方程 (15.5.14) 推得

$$ \hat{\Gamma} (\pi ) = \frac{\sigma ^2 \pi - \beta _2}{2 - \chi (\pi )}. $$

当 \(\pi \uparrow 0\) 时，我们知道 \(\chi (\pi ) \to 0\)，故 \(\hat{\Gamma} (\pi ) \uparrow +\infty\)，这蕴含 (15.5.17)。我们可以定义唯一的 \(B(\bar{s})\) 使得

$$ \int_0^{B(\bar{s})} \Gamma (\xi ) d\xi = \frac{p(x_0 - \bar{s})}{h}, $$

故

$$ S^M(\bar{s}) \le B(\bar{s}), $$

并令 \(M \uparrow +\infty\)，我们得到性质 (15.5.16)。

取 \(s < x_0\)。对于足够小的 \(\alpha\)，我们还可假设 \(s < x_{0\alpha}\)。因此 \(H_\alpha (s, S_\alpha (s)) = 0\)。由估计 (15.5.16)，对于足够小的 \(\alpha\)，我们可假设 \(S_\alpha (s)\) 被 \(2B(\bar{s})\) 所界定。通过提取满足 \(S_\alpha (s) \to S^*\) 的子序列，我们容易得到 \(H_1(S^*) = 0\) 且

$$ \gamma_\alpha (s) \to \gamma (s) = \inf_{\eta > s} \int_s^\eta H_s (\xi ) d\xi = \int_s^{S^*} H_s (\xi ) d\xi $$

我们再次令 \(S(s)\) 为使得 \(H_1(S(s)) = 0\) 的第一个点。

我们在上面，定理 15.1 的证明中已经表明

$$ \gamma'_\alpha (s) \ge - \frac{Q_\alpha (s_1)}{\beta_{0\alpha }} (1 - \exp -\beta_{0\alpha } (x_{0\alpha } - s_1)) > 0, $$

只要 \(s < s_1 < x_{0\alpha}\)。固定 \(s_1 < x_0\)。对于足够小的 \(\alpha\)，我们可假设 \(s_1 < x_{0\alpha}\)，且对 \(s < s_1\)

$$ \gamma'_\alpha (s) \ge - \frac{Q(s_1)}{2\beta _0} (1 - \exp -\beta _0 (x_0 - s_1)) = a(s_1) > 0, $$

故

$$ \gamma_\alpha (s_1) - \gamma_\alpha (s) \ge (s_1 - s)a(s_1). $$

由于 \(\gamma_\alpha (s_1) < 0\)，事实上

$$ -\gamma_\alpha (s) \ge (s_1 - s)a(s_1). $$

现在考虑 \(s_\alpha\)。要么 \(s_\alpha \ge s_1\)，要么 \(s_\alpha < s_1\)，在此情况下由上述不等式

$$ K \ge (s_1 - s_\alpha )a(s_1). $$

因此在所有情况下

(15.5.18) 
$$ s_\alpha \ge s_1 - \frac{K}{a(s_1)} = \bar{s}, $$

但随后由 (15.5.16) 我们还可断言

(15.5.19) 
$$ S_\alpha = S_\alpha (s_\alpha ) \le 2B(\bar{s}), $$

对于足够小的 \(\alpha\)。因此我们可以提取一个子序列使得 \(s_\alpha \to s, S_\alpha \to S\)。另外 \(\gamma(s) = -K\)。然而，出于与 \(s_\alpha\) 相同的理由，存在唯一的 \(s\) 满足此关系。故整个序列 \(s_\alpha \to s\)。定义

(15.5.20) 
$$ \rho_\alpha = \alpha G_{\sigma_\alpha}(s_\alpha) \to \rho = \frac{\sigma^2}{2} Q(s) + f(s) + c\nu + c\lambda \tilde{\xi}, $$

我们可以设

$$ \tilde{G}_\alpha(x) = G_\alpha(x) - \frac{\rho_\alpha}{\alpha}, $$

并声称以下遍历结果

**定理 15.3。** 我们假设 (15.2.4)。函数 \(G_\alpha(x)\)，（及其导数）在紧集上一致收敛到 \(G(x)\)，（及其导数），且对 \(G(x), \rho\) 是 Q.V.I. 的解。

(15.5.21) 
$$ \begin{aligned} AG(x) + \rho \le l(x) \\ G(x) \le K + \inf_{\eta > x} G(\eta) \\ (AG(x) + \rho - l(x))(G(x) - K + \inf_{\eta > x} G(\eta)) = 0, \end{aligned} $$

其中

\(l(x) = f(x) + cv + c\lambda \tilde{\xi}.\)

函数 \(G(x)\) 是 \(C^1\)，其导数具有线性增长。它由一个 \(s, S\) 策略给出

(15.5.22) 
$$ \begin{aligned} AG(x) + \rho = l(x), \quad x > s \\ G(x) = K + \inf_{\eta > x} G(\eta), \quad x \le s \end{aligned} $$

## 15.6. 概率诠释

本节将发展前几节 Q.V.I 方法的概率对偶。我们将 [32] 的方法扩展到扩散和泊松情况。其思想是在 \(s, S\) 策略类中进行优化，并表明我们以这种方式求解 Q.V.I。

### 15.6.1. 带有 \(s, S\) 控制的过程研究

设 \(s < S\) 为两个给定数。我们将定义在 \(s, S\) 策略下、初始值为 \(x\) 的过程 \(y_x^{s,S}(t)\)。回顾需求

$$ D(t) = \nu t + N(t) + \sigma \omega(t), $$

在区间 \(0, t\) 中我们定义

$$ \tau_x^s = \inf \{t \ge 0 \mid x - D(t) \le s\}, $$

且若 \(x > s\)

$$ y_x^{s,S}(t) = x - D(t), \forall t < \tau_x^s. $$

接下来设

$$ y_x^{s,S}(\tau_x^s) = S. $$

设

$$ \tau_{x,n}^{s,S} = \tau_x^s, $$

并假设我们已定义 \(\tau_{x,n}^{s,S}\) 且 \(y_x^{s,S}(\tau_{x,n}^{s,S}) = S\)。我们接着定义

$$ \tau_{x,n+1}^{s,S} = \tau_{x,n}^{s,S} + \inf \{t \ge 0 \mid S - D(\tau_{x,n}^{s,S} + t) + D(\tau_{x,n}^{s,S}) \le s\}. $$

显然 \(\tau_{x,n+1}^{s,S} > \tau_{x,n}^{s,S}\)。我们接下来设

$$ y_x^{s,S}(\tau_{x,n}^{s,S} + t) = S - D(\tau_{x,n}^{s,S} + t) + D(\tau_{x,n}^{s,S}), \forall t < \tau_{x,n+1}^{s,S} - \tau_{x,n}^{s,S}, $$

并再次 \(y_x^{s,S}(\tau_{x,n+1}^{s,S}) = S\)。我们以这种方式定义了由 s, S 策略控制的过程：它在时刻 \(\tau_{x,n}^{s,S}\) 处有跳跃，即冲击时刻，在时刻 \(\tau_{x,n}^{s,S}\) 处的冲击大小为 \(S - y_x^{s,S}(\tau_{x,n}^{s,S}, 0)\)。注意该冲击大于或等于 \(S - s\)。过程 \(y_x^{s,S}(t)\) 还由于需求的复合泊松部分而有跳跃。这是一个马可夫过程，我们将描述其无穷小生成元。

回顾，无穷小生成元是定义在函数 \(\varphi(x)\) 集合上的线性算子，使得极限

$$ \lim_{\epsilon \to 0} \frac{E\varphi(y_x^{s,S}(\epsilon)) - \varphi(x)}{\epsilon} = \mathcal{A}^{s,S}\varphi(x), $$

存在。

由于

$$ y_x^{s,S}(s) = y_S^{s,S}(\epsilon), \forall x \le s, $$

我们需要有

(15.6.1) \(\quad \varphi(x) = \varphi(S), \forall x \le s.\)

执行与第 15.2 节中相同的近似推理，我们容易得到

$$ \mathcal{A}^{s,S}\varphi(x) = \begin{cases} -A\varphi(x), & \text{if } x > s \\ -A\varphi(s), & \text{if } x \le s \end{cases} $$

其中 \(A\) 是方程 (17.2.4) 中定义的二阶微分算子。其定义域是一阶和二阶导数有界且满足 (15.6.1) 的有界函数集合。只需假设函数 \(\varphi\) 和 \(A\varphi\) 有界且 (15.6.1) 满足即可。尽管我们提到 \(\mathcal{A}\) 的定义域，但谈论 \(A\) 的定义域会更方便。

### 15.6.2. 不变量度

我们将表明以下结论

**定理 15.4。** 过程 \(y_x^{s,S}(t)\) 具有如下定义的唯一不变量度

$$ m^{s,S}(x) = \frac{\tilde{m}^{s,S}(x)}{\int_s^{+\infty} \tilde{m}^{s,S}(\xi) d\xi}, $$

其中

(15.6.2) \(\quad \tilde{m}^{s,S}(x) = \begin{cases} 0, & \text{if } x \le s \\ \exp \beta_2 x \int_x^S \exp -\beta_2 \xi \Gamma(S-\xi) d\xi, & \text{if } s \le x \le S \\ \exp \beta_2 x \int_s^S \exp -\beta_2 \xi \Gamma(S-\xi) d\xi, & \text{if } S \le x \end{cases}\)

其中 \(\Gamma(x)\) 是下式的唯一解

(15.6.3) \(\quad -\frac{\sigma^2}{2} \Gamma''(x) + \mu \Gamma'(x) + \lambda \Gamma(x) - \lambda \int_0^x \Gamma(x-\xi) \mu(\xi) d\xi = 0\)

\(\Gamma(0) = 1 \quad 0 \le \Gamma(x) \le 1\)

且 \(\beta_2\) 是下式的唯一负根

\(-\frac{\sigma^2}{2} \beta_2^2 - \nu \beta_2 - \lambda - \lambda \hat{\mu}(\beta_2) = 0.\)

此外，对任何有界的 \(\varphi(x)\)

(15.6.4) 
$$ \Phi_\alpha^{s,S}(x) = E \int_0^{+\infty} \exp - \alpha t \varphi(y_x^{s,S}(t))dt, $$

满足

(15.6.5) 
$$ \alpha \Phi_\alpha^{s,S}(x) \to \int_s^{+\infty} \varphi(x) m^{s,S}(x) dx. $$

证明。我们注意到公式 (15.6.2) 中的 \(\tilde{m}^{s,S}(x)\) 是连续的但不是 \(C^1\)。导数在 \(S\) 处不连续。我们开始证明 \(m^{s,S}(x)\) 是一个不变量度且是唯一的，它是连续的且在 \(S\) 处除外是 \(C^1\)。我们首先证明 \(m^{s,S}(x)\) 必须在区间 \((-\infty, s)\) 上消失。确实，不变量度必须满足

$$ \int m^{s,S}(x)\varphi(x)dx = \int m^{s,S}(x)E\varphi(y_x^{s,S}(\varepsilon))dx, \forall \varepsilon $$

取一个在 \(s, +\infty\) 上消失的测试函数 \(\varphi(x)\)。由前述关系得到

$$ \int_{-\infty}^s m^{s,S}(x)\varphi(x)dx = E\varphi(y_S^{s,S}(\varepsilon)) \int_{-\infty}^s m^{s,S}(x)dx + \int_s^{+\infty} m^{s,S}(x)E\varphi(y_x^{s,S}(\varepsilon))dx $$

令右边 \(\epsilon \to 0\)，我们得到

$$ \varphi(S) \int_{-\infty}^s m^{s,S}(x)dx + \int_s^{+\infty} m^{s,S}(x)\varphi(x)dx = 0, $$

由 \(\varphi\) 的选取得出。现在取 \(\varphi(x)\) 在无穷小生成元的定义域中。不变量度必须满足

$$ \int_s^{+\infty} m^{s,S}(x)A\varphi(x)dx = 0. $$

为简化记号，我们将 \(m(x)\) 写作 \(m^{s,S}(x)\)。我们回顾 \(m\) 的正则性性质并进行分部积分。我们得到

$$
\begin{aligned}
&-\frac{\sigma^2}{2} [\varphi(S)(m'(S+0) - m'(S-0)) + \varphi(s)m'(s)] \\
&\quad -\lambda \varphi(S) \int_s^{+\infty} m(x) \left( \int_{x-s}^{+\infty} \mu(\xi)d\xi \right) dx + \int_s^{+\infty} \varphi(x) \left( \frac{\sigma^2}{2}m''(x) - \nu m'(x) + \lambda m(x) \right) dx \\
&\quad -\lambda \int_s^{+\infty} m(x) \left( \int_0^{x-s} \varphi(x - \xi) \mu(\xi)d\xi \right) dx = 0.
\end{aligned}
$$

利用 \(\varphi\) 满足 \(\varphi(s) = \varphi(S)\) 并整理后，我们得到

$$
\begin{aligned}
&-\varphi(S) \left[ \frac{\sigma^2}{2} (m'(S+0) - m'(S-0) + m'(s)) \right. \\
&\quad \left. + \lambda \int_s^{+\infty} m(x) \left( \int_{x-s}^{+\infty} \mu(\xi)d\xi \right) dx \right] + \int_s^{+\infty} \varphi(x) \left( \frac{\sigma^2}{2}m''(x) - \nu m'(x) \right. \\
&\quad \left. + \lambda m(x) - \lambda \int_0^{+\infty} m(x + \xi) \mu(\xi)d\xi \right) dx = 0.
\end{aligned}

