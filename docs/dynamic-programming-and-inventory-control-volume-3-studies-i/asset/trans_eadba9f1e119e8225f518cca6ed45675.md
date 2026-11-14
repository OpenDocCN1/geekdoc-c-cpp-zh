

证明. 注意，如果我们知道 \( G_{0\alpha}(x; \sigma, \eta) < 0 \)，当 \( x < 0 \) 时，则结果立即从公式 (13.5.31)、(13.5.32) 在 \( x \) 上求导后得出。为了完整性，我们考虑方程 (13.5.31)、(13.5.32) 的迭代过程，起始于 \( u_{0\alpha}(x; \sigma, \eta) = 0 \)。我们有

\( G_{0\alpha}(x; \sigma, \eta) = cx, s_{0\alpha}(\sigma, \eta) = -\infty; \)
\( u_{1\alpha}(x; \sigma, \eta) = l^{(\sigma+\eta)}(x). \)

因此，当 \( x < 0 \) 时，

\( G_{1\alpha}(x; \sigma, \eta) = cx - \alpha px + p\bar{D}(\sigma + \eta + 1), \)

这意味着 \( G_{1\alpha}^*(x; \sigma, \eta) < 0 \)，当 \( x < 0 \) 时。迭代保持这些性质。证明完成。

我们接着进行估计。

## 提议 13.9. 我们有如下估计

\( s_\alpha^-(\sigma, \eta) \le \frac{K}{\alpha p - c(1-\alpha)} = m_\alpha, \)
\( 0 \le S_\alpha(\sigma, \eta) \le \frac{\alpha p m_\alpha + \alpha(p+h)\bar{D}(\sigma + \eta + 1)}{c(1-\alpha) + \alpha h}. \)

**证明.** 我们从第一个不等式开始。只需假设 \( s_\alpha(\sigma, \eta) < 0 \)。注意，由 (13.5.33) 和引理 13.2 可得

\( \chi_\alpha(x; \sigma, \eta) \le c(1-\alpha) - \alpha p, \forall s_\alpha(\sigma, \eta) < x < 0 \)

接下来，由 (13.5.30)，因为 \( s_\alpha(\sigma, \eta) < 0 \),

\( 0 \le K + \int_{s_\alpha(\sigma, \eta)}^0 \chi_\alpha(\xi; \sigma, \eta) d\xi, \)

第一个估计立即得出。让我们继续处理第二个不等式。

回顾以下等价关系很有用：

\( Eu_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta') = E[u_\alpha(x - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \sigma', \eta') | \sigma, \eta] \)

我们还回顾最优反馈

\( \hat{v}_\alpha(x; \sigma, \eta) = \begin{cases} S_\alpha(\sigma, \eta) - x, & \text{if } x \le s_\alpha(\sigma, \eta) \\ 0, & \text{if } x > s_\alpha(\sigma, \eta) \end{cases} \)

贝尔曼方程如下

\( u_\alpha(x; \sigma, \eta) = l^{(\sigma+\eta)}(x) + K \mathbb{I}_{\hat{v}_\alpha(x; \sigma, \eta) > 0} + c \hat{v}_\alpha(x; \sigma, \eta) \)
\( + E[u_\alpha(x + \hat{v}_\alpha(x; \sigma, \eta) - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \sigma', \eta') | \sigma, \eta] \)

令

\( \breve{y}_2 = S_\alpha(\sigma, \eta) - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \quad \hat{v}_2 = \hat{v}_\alpha(x; \sigma', \eta'). \)

在 \( \breve{y}_2, \hat{v}_2 \) 中，随机性来自需求和 \( \sigma', \eta' \)，而 \( \sigma, \eta \) 是已知的。由于 \( s_\alpha(\sigma, \eta) > -m_\alpha \)，我们可以写出

\( u_\alpha(-m_\alpha; \sigma, \eta) = (p+c)m_\alpha + p(\sigma+\eta)D + K \)
\( + c S_\alpha(\sigma, \eta) + \alpha E[u_\alpha(\breve{y}_2; \sigma', \eta') | \sigma, \eta]. \)

另一方面

\( u_\alpha(\hat{y}_2; \sigma', \eta') = l^{(\sigma' + \eta')}(\hat{y}_2) + K \mathbb{I}_{\hat{y}_2 > 0} + c\hat{v}_2 \)

\( + \alpha E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma', \eta']. \)

结合这两个关系并利用期望的运算法则，我们得到

(13.5.34) \( u_\alpha(-m_\alpha; \sigma, \eta) = (p+c)m_\alpha + p(\sigma + \eta)D + K + cE_\delta(\sigma, \eta) \)

\( + \alpha E\{l^{(\sigma' + \eta')}(\hat{y}_2) + K \mathbb{I}_{\hat{y}_2 > 0} + c\hat{v}_2 \)

\( + \alpha E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma, \eta]. \)

另一方面，我们可以从贝尔曼方程写出以下两个不等式

\( u_\alpha(-m_\alpha; \sigma, \eta) \le p m_\alpha + p(\sigma + \eta)\tilde{D} \)

\( + \alpha E\left[u_\alpha(-m_\alpha - D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}, \sigma', \eta') | \sigma, \eta\right] \)

\( u_\alpha(-m_\alpha - D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}, \sigma', \eta') \le l^{(\sigma' + \eta')}(-m_\alpha - D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}) \)

\( + K + c(\hat{v}_2 + \hat{y}_2 + m_\alpha + D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}) \)

\( + \alpha E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma', \eta'], \)

因此，条件下

\( E[u_\alpha(-m_\alpha - D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}, \sigma', \eta') | \sigma, \eta] \le K + p\tilde{D}(\sigma + \eta + 1) + (p+c)m_\alpha \)

\( + cE[\hat{v}_2 + \hat{y}_2 | \sigma, \eta] + cD(\sigma + \eta + 1 - E(\sigma' + \eta' | \sigma, \eta)) \)

\( + \alpha E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma, \eta] \)

汇总结果，我们得到不等式

(13.5.35) \( u_\alpha(-m_\alpha; \sigma, \eta) \le p(m_\alpha + (\sigma + \eta)D) + \alpha K \)

\( + \alpha p\tilde{D}(\sigma + \eta + 1) + \alpha(p+c)m_\alpha + \alpha cE[\hat{v}_2 + \hat{y}_2 | \sigma, \eta] \)

\( + \alpha cD(\sigma + \eta + 1 - E(\sigma' + \eta' | \sigma, \eta)) \)

\( + \alpha^2 E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma, \eta]. \)

比较方程 (13.5.34) 和不等式 (13.5.35) 并消去项，我们得到

\( c(1-\alpha)S_\alpha(\sigma, \eta) + K(1-\alpha) + \alpha K E[\mathbb{I}_{\hat{y}_2 > 0} | \sigma, \eta] + c(1-\alpha)E[\hat{v}_2 | \sigma, \eta] \)

\( + \alpha h E[S_\alpha(\sigma, \eta) - D^{(\sigma + \eta + 1)}]^+ + \alpha p E[S_\alpha(\sigma, \eta) - D^{(\sigma + \eta + 1)}]^- \)

\( \le (\alpha p - c(1-\alpha))m_\alpha + \alpha p\tilde{D}(\sigma + \eta + 1), \)

因此也有

\( (c(1-\alpha) + \alpha h)S_\alpha(\sigma, \eta) \le (\alpha p - c(1-\alpha))m_\alpha + \alpha(p+\tilde{h})\tilde{D}(\sigma + \eta + 1), \)

第二个不等式已证得。\(\square\)

我们可以推导出不依赖于 \(\alpha\) 的估计。由于 \(\alpha \to 1\)，我们可以假设 \(\alpha > \frac{1}{2}\)。我们陈述

## **推论 13.1.** 对于 $\alpha > \frac{1}{2}$，我们有

$|s_\alpha(\sigma, \eta)|, |S_\alpha(\sigma, \eta)| \le m_0$

其中

$m_0 = \frac{\frac{2pK}{p-c} + (p+h)D(M+1)}{\min(c,h)}$

**证明.** 这是提议 13.9 的直接结果。

我们现在证明关于 \( u'_\alpha(x; \sigma, \eta) \) 的估计。

## **引理 13.3.** 我们将证明估计

(13.5.36) 
\(\sup_{\xi < x, \sigma, \eta} |u'_\alpha(x; \sigma, \eta)| \le \frac{C}{\bar{F}((x+m_0)^+)}.\)

**证明.** 我们回顾

\(\chi_\alpha(x; \sigma, \eta) = \mu_\alpha^{(\sigma+\eta)}(x) + \alpha E X_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta'), \forall x > s_\alpha(\sigma, \eta)
= 0, \quad \forall x \le s_\alpha(\sigma, \eta)\)

其中

\(\mu_\alpha^{(\sigma+\eta)}(x) = c(1-\alpha) + \alpha h - \alpha(h+p)\bar{F}(x),\)

并且

\(|s_\alpha(\sigma, \eta)|, |S_\alpha(\sigma, \eta)| \le m_0\)

我们使用

\(E X_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta')
= E[\chi_\alpha(x - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \sigma', \eta') \mathbb{I}_{x - D^{(\sigma+\eta+1-(\sigma'+\eta'))} > s_\alpha(\sigma', \eta')}].\)

由于

\(\mathbb{I}_{x - D^{(\sigma+\eta+1-(\sigma'+\eta'))} > s_\alpha(\sigma', \eta')} \le \mathbb{I}_{x - D^{(\sigma+\eta+1-(\sigma'+\eta'))} > -m_0},\)

我们推断

\(|\chi_\alpha(x; \sigma, \eta)|_{\mathbb{I}_{x > -m_0}} \le |\mu_\alpha^{(\sigma+\eta)}(x)|
+ \alpha E[|\chi_\alpha(x - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \sigma', \eta')| \mathbb{I}_{x - D^{(\sigma+\eta+1-(\sigma'+\eta'))} > -m_0}],\)

利用 \(|\mu_\alpha^{(\sigma+\eta)}(x)| \le \max(h,p)\) 并展开期望，我们得到

\(|\chi_\alpha(x; \sigma, \eta)|_{\mathbb{I}_{x > -m_0}} \le \max(h,p) + \alpha |\chi_\alpha(x; \sigma+1, \eta)|_{\mathbb{I}_{x > -m_0}}
+ \alpha \sum_{k=\sigma+\eta}^M \gamma(k; \alpha, \eta)
+ \alpha \sum_{k=0}^{\sigma+\eta} E|\chi_\alpha(x - D^{(\sigma+\eta+1-k)}, 0, k)| \mathbb{I}_{x - D^{(\sigma+\eta+1-k)} > -m_0} \gamma(k; \sigma, \eta).\)

令

\(w_\alpha(x) = \sup_{\xi < x, \sigma, \eta} |\chi_\alpha(\xi; \sigma, \eta)|_{\mathbb{I}_{x > -m_0}}.\)

由前面的不等式得到

\(|\chi_\alpha(x;\sigma,\eta)|_{\mathbb{I}_{x>-m_0}}\)
\(\le \max(h,p) + w_\alpha(x) \sum_{k=\sigma+\eta+1}^M \gamma(k;\sigma,\eta) + E w_\alpha(x-D) \sum_{k=0}^{\sigma+\eta} \gamma(k;\sigma,\eta)\)
\(= \max(h,p) + w_\alpha(x) - (w_\alpha(x) - E w_\alpha(x-D)) \sum_{k=0}^{\sigma+\eta} \gamma(k;\sigma,\eta),\)

并利用 \(w_\alpha(x) - E w_\alpha(x-D) \ge 0\)，\(\sum_{k=\sigma+\eta}^{\sigma+\eta} \gamma(k;\sigma,\eta) \ge \varpi_0\)，我们得到

\(|\chi_\alpha(x;\sigma,\eta)|_{\mathbb{I}_{x>-m_0}} \le \max(h,p) + w_\alpha(x) - (w_\alpha(x) - E w_\alpha(x-D))\varpi_0\)

令 \(x_0\) 固定。对于 \(x < x_0\)，我们也可以写出

\(|\chi_\alpha(x;\sigma,\eta)|_{\mathbb{I}_{x>-m_0}} \le \max(h,p) + w_\alpha(x_0) - (w_\alpha(x_0) - E w_\alpha(x_0-D))\varpi_0,\)

因此

\(w_\alpha(x_0) \le \max(h,p) + w_\alpha(x_0) - (w_\alpha(x_0) - E w_\alpha(x_0-D))\varpi_0,\)

这意味着

\(w_\alpha(x) - E w_\alpha(x-D) \le \frac{\max(h,p)}{\varpi_0}\)

\(w_\alpha(x) - E w_\alpha(x-D)_{\mathbb{I}_{x>D-m_0}} \le \frac{\max(h,p)}{\varpi_0}.\)

最后

\(w_\alpha(x) \le \frac{\max(h,p)}{\varpi_0} \frac{1}{\bar{F}((x+m_0)^+)}.\)

由此估计，结果立即得出。

定义

\(\Gamma_\alpha(\sigma,\eta) = u_\alpha(-m_0;\sigma,\eta).\)

由于 \(-m_0 < s_\alpha(\sigma,\eta)\)，我们可以写出

\(u_\alpha(-m_0;\sigma,\eta) = (p+c)m_0 + pD(\sigma+\eta) + cs_\alpha(\sigma,\eta)\)
\(+\alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(s_\alpha(\sigma,\eta);\sigma',\eta'),\)

因此我们得到

\(\Gamma_\alpha(\sigma,\eta) = \alpha E \Gamma_\alpha(\sigma',\eta') + \Psi_\alpha(\sigma,\eta),\)

其中

\(\Psi_\alpha(\sigma,\eta) = (p+c)m_0 + pD(\sigma+\eta) + cs_\alpha(\sigma,\eta)\)
\(+\alpha E[u_\alpha(s_\alpha(\sigma,\eta) - D^{(\sigma+\eta+1-(\sigma'+\eta'))};\sigma',\eta') - u_\alpha(-m_0;\sigma,\eta)].\)

由提议 13.9 和引理 13.3 的估计可立即看出

\(|\Psi_\alpha(\sigma,\eta)| \le C, \forall \alpha, \sigma, \eta.\)

利用不变测度 \(\mu(\sigma,\eta)\)，我们定义

\(\rho_\alpha = \sum_{\sigma,\eta} \Psi_\alpha(\sigma,\eta)\mu(\sigma,\eta),\)

