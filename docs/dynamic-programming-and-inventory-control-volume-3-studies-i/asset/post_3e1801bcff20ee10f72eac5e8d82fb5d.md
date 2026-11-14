
PROOF. Note that if we know that \( G_{0\alpha}(x; \sigma, \eta) < 0 \), for x < 0, then the result follows immediately from formulas (13.5.31), (13.5.32) after taking the derivative in x. To complete we consider an iterative process for equations (13.5.31), (13.5.32), starting with \( u_{0\alpha}(x; \sigma, \eta) = 0 \). We then have

\( G_{0\alpha}(x; \sigma, \eta) = cx, s_{0\alpha}(\sigma, \eta) = -\infty; \)
\( u_{1\alpha}(x; \sigma, \eta) = l^{(\sigma+\eta)}(x). \)

therefore for x < 0,

\( G_{1\alpha}(x; \sigma, \eta) = cx - \alpha px + p\bar{D}(\sigma + \eta + 1), \)

which implies \( G_{1\alpha}^*(x; \sigma, \eta) < 0 \), for x < 0. The iteration preserves the properties. This completes the proof.

We then proceed with estimates.

## Proposition 13.9. We have the estimates

\( s_\alpha^-(\sigma, \eta) \le \frac{K}{\alpha p - c(1-\alpha)} = m_\alpha, \)
\( 0 \le S_\alpha(\sigma, \eta) \le \frac{\alpha p m_\alpha + \alpha(p+h)\bar{D}(\sigma + \eta + 1)}{c(1-\alpha) + \alpha h}. \)

**PROOF.** We begin with the first inequality. It is sufficient to assume \( s_\alpha(\sigma, \eta) < 0 \). Note that from (13.5.33) and Lemma 13.2 we have

\( \chi_\alpha(x; \sigma, \eta) \le c(1-\alpha) - \alpha p, \forall s_\alpha(\sigma, \eta) < x < 0 \)

Next from (13.5.30), since \( s_\alpha(\sigma, \eta) < 0 \),

\( 0 \le K + \int_{s_\alpha(\sigma, \eta)}^0 \chi_\alpha(\xi; \sigma, \eta) d\xi, \)

and the first estimate follows immediately. Let us proceed with the second inequality.

It is useful to recall the equivalence

\( Eu_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta') = E[u_\alpha(x - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \sigma', \eta') | \sigma, \eta] \)

We also recall the optimal feedback

\( \hat{v}_\alpha(x; \sigma, \eta) = \begin{cases} S_\alpha(\sigma, \eta) - x, & \text{if } x \le s_\alpha(\sigma, \eta) \\ 0, & \text{if } x > s_\alpha(\sigma, \eta) \end{cases} \)

The Bellman equation is then

\( u_\alpha(x; \sigma, \eta) = l^{(\sigma+\eta)}(x) + K \mathbb{I}_{\hat{v}_\alpha(x; \sigma, \eta) > 0} + c \hat{v}_\alpha(x; \sigma, \eta) \)
\( + E[u_\alpha(x + \hat{v}_\alpha(x; \sigma, \eta) - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \sigma', \eta') | \sigma, \eta] \)

Let us denote

\( \breve{y}_2 = S_\alpha(\sigma, \eta) - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \quad \hat{v}_2 = \hat{v}_\alpha(x; \sigma', \eta'). \)

In \( \breve{y}_2, \hat{v}_2 \) the randomness comes from the demands and \( \sigma', \eta' \), whereas \( \sigma, \eta \) is known. Since \( s_\alpha(\sigma, \eta) > -m_\alpha \), we can write

\( u_\alpha(-m_\alpha; \sigma, \eta) = (p+c)m_\alpha + p(\sigma+\eta)D + K \)
\( + c S_\alpha(\sigma, \eta) + \alpha E[u_\alpha(\breve{y}_2; \sigma', \eta') | \sigma, \eta]. \)

On the other hand

\( u_\alpha(\hat{y}_2; \sigma', \eta') = l^{(\sigma' + \eta')}(\hat{y}_2) + K \mathbb{I}_{\hat{y}_2 > 0} + c\hat{v}_2 \)

\( + \alpha E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma', \eta']. \)

Combining these two relations and using rules of expected values we obtain

(13.5.34) \( u_\alpha(-m_\alpha; \sigma, \eta) = (p+c)m_\alpha + p(\sigma + \eta)D + K + cE_\delta(\sigma, \eta) \)

\( + \alpha E\{l^{(\sigma' + \eta')}(\hat{y}_2) + K \mathbb{I}_{\hat{y}_2 > 0} + c\hat{v}_2 \)

\( + \alpha E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma, \eta]. \)

On the other hand we can write the following two inequalities, from Bellman equation

\( u_\alpha(-m_\alpha; \sigma, \eta) \le p m_\alpha + p(\sigma + \eta)\tilde{D} \)

\( + \alpha E\left[u_\alpha(-m_\alpha - D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}, \sigma', \eta') | \sigma, \eta\right] \)

\( u_\alpha(-m_\alpha - D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}, \sigma', \eta') \le l^{(\sigma' + \eta')}(-m_\alpha - D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}) \)

\( + K + c(\hat{v}_2 + \hat{y}_2 + m_\alpha + D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}) \)

\( + \alpha E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma', \eta'], \)

hence conditioning

\( E[u_\alpha(-m_\alpha - D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}, \sigma', \eta') | \sigma, \eta] \le K + p\tilde{D}(\sigma + \eta + 1) + (p+c)m_\alpha \)

\( + cE[\hat{v}_2 + \hat{y}_2 | \sigma, \eta] + cD(\sigma + \eta + 1 - E(\sigma' + \eta' | \sigma, \eta)) \)

\( + \alpha E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma, \eta] \)

Collecting results we obtain the inequality

(13.5.35) \( u_\alpha(-m_\alpha; \sigma, \eta) \le p(m_\alpha + (\sigma + \eta)D) + \alpha K \)

\( + \alpha p\tilde{D}(\sigma + \eta + 1) + \alpha(p+c)m_\alpha + \alpha cE[\hat{v}_2 + \hat{y}_2 | \sigma, \eta] \)

\( + \alpha cD(\sigma + \eta + 1 - E(\sigma' + \eta' | \sigma, \eta)) \)

\( + \alpha^2 E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma, \eta]. \)

Comparing equation (13.5.34) and inequality (13.5.35) and canceling terms we get

\( c(1-\alpha)S_\alpha(\sigma, \eta) + K(1-\alpha) + \alpha K E[\mathbb{I}_{\hat{y}_2 > 0} | \sigma, \eta] + c(1-\alpha)E[\hat{v}_2 | \sigma, \eta] \)

\( + \alpha h E[S_\alpha(\sigma, \eta) - D^{(\sigma + \eta + 1)}]^+ + \alpha p E[S_\alpha(\sigma, \eta) - D^{(\sigma + \eta + 1)}]^- \)

\( \le (\alpha p - c(1-\alpha))m_\alpha + \alpha p\tilde{D}(\sigma + \eta + 1), \)

hence also

\( (c(1-\alpha) + \alpha h)S_\alpha(\sigma, \eta) \le (\alpha p - c(1-\alpha))m_\alpha + \alpha(p+\tilde{h})\tilde{D}(\sigma + \eta + 1), \)

and the second inequality is proven. \(\square\)

We can deduce estimates which do not depend on \(\alpha\). Since \(\alpha \to 1\) we may assume \(\alpha > \frac{1}{2}\). We state

## **Corollary 13.1.** For $\alpha > \frac{1}{2}$ we have

$|s_\alpha(\sigma, \eta)|, |S_\alpha(\sigma, \eta)| \le m_0$

with

$m_0 = \frac{\frac{2pK}{p-c} + (p+h)D(M+1)}{\min(c,h)}$

**PROOF.** It is an immediate consequence of Proposition 13.9.

We now prove estimates on $u'_\alpha(x; \sigma, \eta)$.

## **Lemma 13.3.** We shall prove the estimate

(13.5.36) 
\(\sup_{\xi < x, \sigma, \eta} |u'_\alpha(x; \sigma, \eta)| \le \frac{C}{\bar{F}((x+m_0)^+)}.\)

**PROOF.** We recall that

\(\chi_\alpha(x; \sigma, \eta) = \mu_\alpha^{(\sigma+\eta)}(x) + \alpha E X_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta'), \forall x > s_\alpha(\sigma, \eta)
= 0, \quad \forall x \le s_\alpha(\sigma, \eta)\)

with

\(\mu_\alpha^{(\sigma+\eta)}(x) = c(1-\alpha) + \alpha h - \alpha(h+p)\bar{F}(x),\)

and

\(|s_\alpha(\sigma, \eta)|, |S_\alpha(\sigma, \eta)| \le m_0\)

We use

\(E X_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta')
= E[\chi_\alpha(x - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \sigma', \eta') \mathbb{I}_{x - D^{(\sigma+\eta+1-(\sigma'+\eta'))} > s_\alpha(\sigma', \eta')}].\)

Since

\(\mathbb{I}_{x - D^{(\sigma+\eta+1-(\sigma'+\eta'))} > s_\alpha(\sigma', \eta')} \le \mathbb{I}_{x - D^{(\sigma+\eta+1-(\sigma'+\eta'))} > -m_0},\)

we deduce

\(|\chi_\alpha(x; \sigma, \eta)|_{\mathbb{I}_{x > -m_0}} \le |\mu_\alpha^{(\sigma+\eta)}(x)|
+ \alpha E[|\chi_\alpha(x - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \sigma', \eta')| \mathbb{I}_{x - D^{(\sigma+\eta+1-(\sigma'+\eta'))} > -m_0}],\)

using \(|\mu_\alpha^{(\sigma+\eta)}(x)| \le \max(h,p)\) and expanding the expectation we get

\(|\chi_\alpha(x; \sigma, \eta)|_{\mathbb{I}_{x > -m_0}} \le \max(h,p) + \alpha |\chi_\alpha(x; \sigma+1, \eta)|_{\mathbb{I}_{x > -m_0}}
+ \alpha \sum_{k=\sigma+\eta}^M \gamma(k; \alpha, \eta)
+ \alpha \sum_{k=0}^{\sigma+\eta} E|\chi_\alpha(x - D^{(\sigma+\eta+1-k)}, 0, k)| \mathbb{I}_{x - D^{(\sigma+\eta+1-k)} > -m_0} \gamma(k; \sigma, \eta).\)

Let us denote

\(w_\alpha(x) = \sup_{\xi < x, \sigma, \eta} |\chi_\alpha(\xi; \sigma, \eta)|_{\mathbb{I}_{x > -m_0}}.\)

We get from the previous inequality

\(|\chi_\alpha(x;\sigma,\eta)|_{\mathbb{I}_{x>-m_0}}\)
\(\le \max(h,p) + w_\alpha(x) \sum_{k=\sigma+\eta+1}^M \gamma(k;\sigma,\eta) + E w_\alpha(x-D) \sum_{k=0}^{\sigma+\eta} \gamma(k;\sigma,\eta)\)
\(= \max(h,p) + w_\alpha(x) - (w_\alpha(x) - E w_\alpha(x-D)) \sum_{k=0}^{\sigma+\eta} \gamma(k;\sigma,\eta),\)

and using \(w_\alpha(x) - E w_\alpha(x-D) \ge 0\), \(\sum_{k=\sigma+\eta}^{\sigma+\eta} \gamma(k;\sigma,\eta) \ge \varpi_0\), we obtain

\(|\chi_\alpha(x;\sigma,\eta)|_{\mathbb{I}_{x>-m_0}} \le \max(h,p) + w_\alpha(x) - (w_\alpha(x) - E w_\alpha(x-D))\varpi_0\)

Let \(x_0\) be fixed. For \(x < x_0\) we may also write

\(|\chi_\alpha(x;\sigma,\eta)|_{\mathbb{I}_{x>-m_0}} \le \max(h,p) + w_\alpha(x_0) - (w_\alpha(x_0) - E w_\alpha(x_0-D))\varpi_0,\)

and thus

\(w_\alpha(x_0) \le \max(h,p) + w_\alpha(x_0) - (w_\alpha(x_0) - E w_\alpha(x_0-D))\varpi_0,\)

which implies

\(w_\alpha(x) - E w_\alpha(x-D) \le \frac{\max(h,p)}{\varpi_0}\)

\(w_\alpha(x) - E w_\alpha(x-D)_{\mathbb{I}_{x>D-m_0}} \le \frac{\max(h,p)}{\varpi_0}.\)

Finally

\(w_\alpha(x) \le \frac{\max(h,p)}{\varpi_0} \frac{1}{\bar{F}((x+m_0)^+)}.\)

From this estimate the results follows immediately.

Define then

\(\Gamma_\alpha(\sigma,\eta) = u_\alpha(-m_0;\sigma,\eta).\)

Since \(-m_0 < s_\alpha(\sigma,\eta)\) we may write

\(u_\alpha(-m_0;\sigma,\eta) = (p+c)m_0 + pD(\sigma+\eta) + cs_\alpha(\sigma,\eta)\)
\(+\alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(s_\alpha(\sigma,\eta);\sigma',\eta'),\)

and thus we obtain

\(\Gamma_\alpha(\sigma,\eta) = \alpha E \Gamma_\alpha(\sigma',\eta') + \Psi_\alpha(\sigma,\eta),\)

with

\(\Psi_\alpha(\sigma,\eta) = (p+c)m_0 + pD(\sigma+\eta) + cs_\alpha(\sigma,\eta)\)
\(+\alpha E[u_\alpha(s_\alpha(\sigma,\eta) - D^{(\sigma+\eta+1-(\sigma'+\eta'))};\sigma',\eta') - u_\alpha(-m_0;\sigma,\eta)].\)

From the estimates of Proposition 13.9 and Lemma 13.3 we see immediately that

\(|\Psi_\alpha(\sigma,\eta)| \le C, \forall \alpha, \sigma, \eta.\)

Using the invariant measure \(\mu(\sigma,\eta)\) we define

\(\rho_\alpha = \sum_{\sigma,\eta} \Psi_\alpha(\sigma,\eta)\mu(\sigma,\eta),\)
