
|  | $\sigma^{2}/n$ | $\sigma^{4}$ | $\sigma^{4}/n$ | $\sigma^{6}$ |
|:---|:---:|:---:|:---:|:---:|
| small samples ($n \sim 1/\sigma$) | $\sigma^{3}$ | $\sigma^{4}$ | $\sigma^{5}$ | $\sigma^{6}$ |
| large samples ($n \sim 1/\sigma^{2}$) | $\sigma^{4}$ | $\sigma^{4}$ | $\sigma^{6}$ | $\sigma^{6}$ |

Table 6.1: The order of magnitude of the four terms in (6.23).

The cross-product expansion (6.26) has a similar structure:
\[\mathbb{E}\bigl((\Delta\hat{\boldsymbol{\theta}}_{m})(\Delta\hat{\boldsymbol{\theta}}_{m'})\bigr) = \mathscr{O}(\sigma^{2}/n)+\mathscr{O}(\sigma^{4})+\mathscr{O}(\sigma^{4}/n)+\mathscr{O}(\sigma^{6}), \tag{6.29}\]
i.e., the fourth-order term coming from the biases is larger (hence more significant) than the one coming from the covariance.

**Example.** In typical computer vision applications, $\sigma$ does not exceed 5% of the size of the image, see [17] (the value $\sigma=0.05$ was used in most of our simulated examples). The number of data points normally varies between 10–20 (on the low end) and a few hundred (on the high end). For simplicity, we can set $n \sim 1/\sigma$ for smaller samples and $n \sim 1/\sigma^{2}$ for larger samples. Then Table 6.1 presents the corresponding typical magnitudes of each of the four terms in (6.23). We see that for larger samples the fourth order term coming from the bias may be just as big as the leading second-order term, hence it would be unwise to ignore it.

Some earlier studies, see e.g., [17, 42, 66, 95], focused on the leading, i.e., second-order terms only, disregarding all the fourth-order terms, and this is where our analysis is different. We make one step further — we keep all the terms of order $\mathscr{O}(\sigma^{2}/n)$ and $\mathscr{O}(\sigma^{4})$. The less significant terms of order $\mathscr{O}(\sigma^{4}/n)$ and $\mathscr{O}(\sigma^{6})$ would be discarded.

**Complete MSE expansion.** Combining (6.26) for all $1 \le m,m' \le k$ gives a matrix formula for the (total) mean squared error (MSE)
\[\mathbb{E}\Bigl[\bigl(\Delta\hat{\boldsymbol{\Theta}}\bigr)\bigl(\Delta\hat{\boldsymbol{\Theta}}\bigr)^{T}\Bigr]=\sigma^{2}\mathbf{G}\mathbf{G}^{T}+\sigma^{4}\mathbf{B}\mathbf{B}^{T}+\cdots, \tag{6.30}\]
where $\mathbf{G}$ is the $k \times 2n$ matrix of first order partial derivatives of $\hat{\boldsymbol{\Theta}}(\mathbf{X})$, its rows are $\mathbf{G}^{T}_{m}$, $1 \le m \le k$, and
\[\mathbf{B}=\tfrac{1}{2}\bigl[\mathrm{tr}\mathbf{H}_{1},\ldots,\mathrm{tr}\mathbf{H}_{k}\bigr]^{T}\]
is the $k$-vector that represents the leading term of the bias of $\hat{\boldsymbol{\Theta}}$, cf. (6.22). Our previous analysis shows that $\mathbf{G}\mathbf{G}^{T}=\mathscr{O}(1/n)$ and $\mathbf{B}\mathbf{B}^{T}=\mathscr{O}(1)$, hence both terms explicitly shown in (6.30) are significant, by our adopted rules; the trailing dots stand for all insignificant terms (those of order $\sigma^{4}/n$ and $\sigma^{6}$).

We call the first (main) term $\pmb{\sigma}^2\mathbf{G}\mathbf{G}^T$ in (6.30) the variance term, as it characterizes the variance (more precisely, the covariance matrix) of the estimator $\hat{\pmb{\Theta}}$, to the leading order. The second term $\pmb{\sigma}^4\mathbf{B}\mathbf{B}^T$ comes from the bias $\pmb{\sigma}^2\mathbf{B}$ of the estimator, again to the leading order.

For brevity we denote the variance term by $\mathbf{V}=\mathbf{G}\mathbf{G}^T$.

**Essential bias.** A more detailed analysis of many particular estimators (see [104] and our Chapter 7) reveal that the bias $\pmb{\sigma}^2\mathbf{B}$ is the sum of terms of two types: some of them are of order $\pmb{\sigma}^2$ and some others are of order $\pmb{\sigma}^2/n$, i.e.

$\mathbb{E}(\Delta\hat{\pmb{\Theta}})=\pmb{\sigma}^2\mathbf{B}+\mathcal{O}(\pmb{\sigma}^4)=\pmb{\sigma}^2\mathbf{B}_1+\pmb{\sigma}^2\mathbf{B}_2+\mathcal{O}(\pmb{\sigma}^4)$,

where $\mathbf{B}_1=\mathcal{O}(1)$ and $\mathbf{B}_2=\mathcal{O}(1/n)$.

We call $\pmb{\sigma}^2\mathbf{B}_1$ the essential bias of the estimator $\hat{\pmb{\Theta}}$. This is its bias to the leading order, $\pmb{\sigma}^2$. The other terms (i.e., $\pmb{\sigma}^2\mathbf{B}_2$, and $\mathcal{O}(\pmb{\sigma}^4)$) constitute nonessential bias; they can be dropped according to our adopted rules. Then (6.30) can be reduced to

$\mathbb{E}\left[\left(\Delta\hat{\pmb{\Theta}}\right)\left(\Delta\hat{\pmb{\Theta}}\right)^T\right]=\pmb{\sigma}^2\mathbf{V}+\pmb{\sigma}^4\mathbf{B}_1\mathbf{B}_1^T+\cdots, \qquad\qquad\qquad\qquad\qquad\qquad(6.31)$

where we only keep significant terms of order $\pmb{\sigma}^2/n$ and $\pmb{\sigma}^4$ and drop the rest (remember also that $\mathbf{V}=\mathbf{G}\mathbf{G}^T$).

## 6.8 Variance and essential bias of the MLE

Our approximate error analysis in Sections 6.6 and 6.7 is developed for general parameter estimators, under a very mild assumption of geometric consistency (6.19). In the circle and ellipse fitting case, our analysis applies to all geometric and algebraic fits. In this section we focus on the geometric fit only, i.e., on the Maximum Likelihood Estimators. For the MLE, explicit formulas can be derived for the asymptotic variance matrix $\mathbf{V}$ and the essential bias vector $\mathbf{B}_1$ in (6.31).

In fact, such formulas were obtained in the 1980s by Amemiya, Fuller, and Wolter [5, 192]. They studied the Maximum Likelihood Estimators for general curve parameters in the context of the Cartesian functional model. Their assumptions on $n$ and $\sigma$ were similar to ours, see below.

**Amemiya-Fuller-Wolter asymptotic model.** In their studies, Amemiya, Fuller, and Wolter assume that both $\sigma$ and $n$ are variable, so that $\sigma \rightarrow 0$ and $n \rightarrow \infty$. Precisely, they consider a sequence of independent experiments, indexed by $m=1,2,\ldots$. In each experiment $n=n_m$ points are observed along a true curve (the same for all experiments), with the noise level $\sigma=\sigma_m>0$. They put

$\sigma_m^{-2} n_m = m, \qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad(6.32)$

which simply gives a precise meaning to their index $m$. The reason for this notation is as follows: suppose there are $n_m$ distinct true points on the true curve, and each is observed independently $k_m$ times, i.e., we have $k_m$ replicated observations of each true point, all with unit variance $\sigma^2 = 1$. Then averaging those $k_m$ observations of each true point gives a single observation with variance $\sigma_m^2 = 1/k_m$. Now $m = k_m n_m = \sigma_m^{-2} n_m$ represents the total number of the original (replicated) observations.

Next they assume that $n_m \to \infty$ and $\sigma_m \to 0$, as $m \to \infty$, so that

$$\sigma_m^2 n_m \to 0 \qquad \text{as } m \to \infty,$$

i.e., $n$ grows more slowly than $1/\sigma^2$. In the strict mathematical sense, these assumptions are effectively equivalent to ours in Section 6.7, though we prefer to treat $n$ as a (moderately large) constant, and not as a variable.

**Asymptotic variance of the MLE.** Amemiya, Fuller and Wolter [5, 192] investigate the Maximum Likelihood Estimator (i.e., the estimator obtained by the geometric fit); they prove asymptotic normality and explicitly compute the asymptotic covariance matrix, to the leading order (see Theorem 1 in [5]). In our notation, their main result is

$$m^{-1} \left( \widehat{\Theta}_{\text{MLE}} - \widetilde{\Theta} \right) \to_L N(0, \mathbf{V}_{\text{MLE}}^*), \qquad \qquad (6.33)$$

where

$$\mathbf{V}_{\text{MLE}}^* = \left( \lim_{m \to \infty} \frac{1}{n_m} \sum_{i=1}^{n_m} \frac{P_{\Theta i} P_{\Theta i}^T}{\|P_{x i}\|^2} \right)^{-1}, \qquad \qquad \qquad (6.34)$$

assuming that the limit exists. Here

$$P_{\Theta i} = \left( \partial P(\check{x}_i; \widetilde{\Theta}) / \partial \theta_1, \dots, \partial P(\check{x}_i; \widetilde{\Theta}) / \partial \theta_k \right)^T$$

stands for the gradient of $P$ with respect to the model parameters $\theta_1, \dots, \theta_k$ and

$$P_{x i} = \left( \partial P(\check{x}_i; \widetilde{\Theta}) / \partial x, \partial P(\check{x}_i; \widetilde{\Theta}) / \partial y \right)^T$$

for the gradient with respect to the spatial variables $x$ and $y$; both gradients are taken at the true point $\check{x}_i$.

Given the equation of a curve $P(x, y; \Theta) = 0$, both gradients can be computed easily. For example in the case of fitting circles defined by

$$P = (x-a)^2 + (y-b)^2 - R^2,$$

we have

$$P_{\Theta i} = -2 \left( (\check{x}_i - \check{a}), (\check{y}_i - \check{b}), \check{R} \right)^T$$
