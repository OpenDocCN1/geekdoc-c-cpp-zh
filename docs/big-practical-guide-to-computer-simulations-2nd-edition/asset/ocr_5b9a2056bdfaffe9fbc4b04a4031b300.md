![](bbox=[0.15, 0.12, 0.88, 0.45])

Fig. 8.19 Probability density function of the sample mean $\overline{X}$ for large enough sample sizes $n$ where the distribution becomes Gaussian. The true expectation value is denoted by $\mu$ and $\sigma_{\overline{X}}$ is the variance of the sample mean. The probability that a random number drawn from this distribution falls outside the symmetric interval $[\mu - z\sigma_{\overline{X}}, \mu + z\sigma_{\overline{X}}]$ is $\alpha$.

# unknown variance $\sigma_{\overline{X}}$

First, one can rewrite

$1 - \alpha = P(\mu - z\sigma_{\overline{X}} \le \overline{X} \le \mu + z\sigma_{\overline{X}})$
$= P(-z\sigma_{\overline{X}} \le \overline{X} - \mu \le z\sigma_{\overline{X}})$
$= P(-\overline{X} - z\sigma_{\overline{X}} \le -\mu \le -\overline{X} + z\sigma_{\overline{X}})$
$= P(\overline{X} - z\sigma_{\overline{X}} \le \mu \le \overline{X} + z\sigma_{\overline{X}})$.

This now states the probability that the true value, which is estimated by the sample mean $\overline{X}$, lies within an interval which is symmetric about the estimate $\overline{X}$. Note that the width $2z\sigma_{\overline{X}}$ is basically given by $\sigma_{\overline{X}} = \sqrt{\text{Var}[\overline{X}]}$. This explains why the mean squared error $\text{MSE}(H) = \text{Var}[H]$, as presented in the beginning of this section, is a good measure for the statistical error made by the estimator. This will be used in Sec. 8.3.4.

To finish, we estimate the true variance $\sigma^2$ using $\frac{n}{n-1}S^2$, hence we get $\sigma_{\overline{X}} = \frac{\sigma}{\sqrt{n}} \approx \frac{S}{\sqrt{n-1}}$. To summarize we get:

$P\left(\overline{X} - z\frac{S}{\sqrt{n-1}} \le \mu \le \overline{X} + z\frac{S}{\sqrt{n-1}}\right) \approx 1 - \alpha \quad (8.62)$

Note that this confidence interval, with $l_\alpha = \overline{X} - z(\alpha)S/\sqrt{n-1}$ and $u_\alpha =$