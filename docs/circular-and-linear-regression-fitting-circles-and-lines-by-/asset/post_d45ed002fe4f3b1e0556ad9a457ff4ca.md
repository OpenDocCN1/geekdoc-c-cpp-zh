
it is clear that one is more likely to observe points *outside* the true arc than *inside* it. Thus the fitted arc tends to be biased *outward*.

![](img/86db288e3c266985d1648282179ae4b5_197_0.png)

*Figure 6.5 The likelihood of observing a point outside the true arc is higher than that inside it.*

If one fits circles, then clearly the bias is toward larger circles, i.e., the radius estimate tends to exceed its true value. Werman and Keren [189] empirically demonstrate that the radius estimate may be as high as 150% of the true radius value, i.e., one may have $\mathbb{E}(\hat{R}) = 1.5R$. Such a heavy bias occurs, however, only if the noise is so large that $\sigma \approx R$.

A detailed analysis involving Taylor expansion [17] shows that

$$\mathbb{E}(\hat{R}) = R + \frac{\sigma^2}{2R} + \mathcal{O}(\sigma^4), \quad (6.43)$$

i.e., the ratio **bias:radius** is approximately $\frac{1}{2}(\sigma/R)^2$. As in most computer vision applications $\sigma/R$ stays below 0.05, cf. [17], the **bias:radius** ratio rarely exceeds 0.001. But still it is something one has to reckon with. The worst part here is perhaps that the bias does not vanish (or even decrease) when one samples more data points, i.e., when $n$ grows, see next.

**Inconsistency.** In classical statistics, an estimator $\hat{\Theta}_n$ of an unknown parameter vector $\Theta$, based on $n$ independent observations, is said to be *consistent* if $\hat{\Theta}_n \to \Theta$ in probability, as $n \to \infty$, where $\Theta$ denotes the true parameter vector. One upgrades this notion to *strong consistency* if the convergence occurs almost surely, i.e., with probability one.

Motivated by this notion, many authors examined the consistency of curve fitting algorithms and found that in nonlinear cases they are almost universally *inconsistent*. In fact, it was found that $\hat{\Theta}_n$ converges (both in probability and almost surely) to some limit $\Theta^*$, which is different from the true parameter $\Theta$.

To determine the limit $\Theta^*$ we need to specify how the true points are chosen on the true curve, in the limit $n \to \infty$. Let $\mathbb{P}_0$ denote a probability measure on the true curve $P(x,y; \Theta) = 0$. If the curve is a circle or an ellipse, then $\mathbb{P}_0$ may be a uniform measure on the entire curve, or a uniform measure on an arc.

Now we can choose $n$ true points randomly according to the measure $\mathbb{P}_0$, then we get a structural model, see Section 6.1. Alternatively, we can set $n$ true points in some specific way but make sure that their asymptotic distribution converges to $\mathbb{P}_0$. For example, if $\mathbb{P}_0$ is a uniform measure on an arc, then the true points can be positioned equally spaced along that arc, and their distribution will converge to $\mathbb{P}_0$.

Let $\mathbb{P}_{\sigma}$ denote the probability distribution of an observed point $(x,y) = (\tilde{x}, \tilde{y}) + (\delta, \varepsilon)$, where $(\tilde{x}, \tilde{y})$ has distribution $\mathbb{P}_0$, and $\delta$ and $\varepsilon$ are normal random variables with mean zero and variance $\sigma^2$, independent from each other and from $(\tilde{x}, \tilde{y})$. In the structural model, the observed points are i.i.d. random variables with distribution $\mathbb{P}_{\sigma}$. (Note that if $\sigma = 0$, then $\mathbb{P}_{\sigma}$ actually coincides with $\mathbb{P}_0$.)

Suppose the estimate $\hat{\Theta}_n$ of the unknown parameter vector $\Theta$ is obtained by minimizing

$$\mathscr{F}(\Theta) = \sum_{i=1}^{n} f^2(x_i, y_i; \Theta), (6.44)$$

where $f(x, y; \Theta)$ is a certain function. The geometric fit uses $f(x, y; \Theta) = \{$the distance from the point $(x, y)$ to the curve $P(x, y; \Theta) = 0\}$. Algebraic fits use other functions.

Then we have the following fact:

> **Theorem 11** Under certain regularity conditions, the estimator $\hat{\Theta}_n$ converges, in probability and almost surely, to the (assumed unique) value $\Theta^*$ minimizing

$$\mathscr{F}^*(\Theta) = \int f^2(x, y; \Theta) d\mathbb{P}_{\sigma}. (6.45)$$

**Proof of the theorem.** This theorem is a straightforward generalization of the one proved by Berman and Culpin [18] for circular fits. For the sake of completeness, we sketch its proof here (this subsection can be skipped without any harm for further reading). Our proof uses elements of measure theory.

Suppose we observe $n$ points $(x_1, y_1), \ldots, (x_n, y_n)$. Let $\mathbb{P}_n$ denote an atomic measure on the $xy$ plane supported by the observed points, i.e., the measure $\mathbb{P}_n$ is defined by

$$\int g(x, y) d\mathbb{P}_n = \frac{1}{n} \sum_{i=1}^{n} g(x_i, y_i)$$

for any continuous function $g$. In terms of $\mathbb{P}_n$, our estimate $\hat{\Theta}_n$ is obtained by minimizing the integral

$$\frac{1}{n} \mathscr{F}(\Theta) = \int f^2(x, y; \Theta) d\mathbb{P}_n$. (6.46)$$

It follows from the strong law of large numbers that $\mathbb{P}_n$ weakly converges to $\mathbb{P}_{\sigma}$ almost surely, i.e., with probability one. Thus the arg-minimum of the integral (6.46) converges to the (assumed unique) arg-minimum of the integral (6.45).

The mild regularity assumptions we need here are the smoothness of the curve $P(x, y; \Theta) = 0$, the compactness of the support of the measure $\mathbb{P}_0$ (which is automatically ensured for closed curves like circles or ellipses), and a certain continuity in $x, y, \Theta$ of the "cost" function $f$; we omit details.

**Inconsistency of the MLE.** In most cases, the limit value $\Theta^{*}$ specified by Theorem 11 is different from the true parameter vector $\Theta$. There are general mathematical theorems on the inconsistency of nonlinear EIV regression estimators. For example, Fazekas, Kukush, and Zwanzig [59] proved that under mild regularity and “genericity” conditions, the Maximum Likelihood Estimator (i.e., the geometric fit) is inconsistent; they also derived approximate formulas for the limit $\Theta^{*}$.

## 6.11 Consistent fit and adjusted least squares

Once statisticians realized that parameter estimators in the curve fitting problems were almost universally biased, and once they derived various approximate formulas for the bias, attempts were made to eliminate the latter. Many practitioners designed various "unbiasing" schemes and tricks, and claimed that they removed the bias.

One needs to remember, however, that truly unbiased estimation in non-linear EIV problems is practically impossible. In fact, every known "bias removal" procedure only eliminates a part of the bias; for example one can remove the leading term in an asymptotic expansion for the bias, but higher order terms will persist. We will describe several such tricks below.

**Simple bias reduction.** The bias of the radius estimate of the geometric circle fit is known to be $\frac{\sigma^2}{2R} + \mathcal{O}(\sigma^4)$, see (6.43). Thus one can construct an "unbiased" estimate by

$$\hat{R}_{\text{'unbiased'}} = \hat{R} - \frac{\sigma^2}{2\hat{R}}, \qquad (6.47)$$

Here we assume, for simplicity, that $\sigma$ is known. Squaring (6.47) and ignoring higher order terms gives another version of essentially unbiased radius estimator:

$$\hat{R}^2_{\text{'unbiased'}} = \hat{R}^2 - \sigma^2. \qquad (6.48)$$

Similar tricks are proposed by various authors, see e.g., [189]. For other tricks, see [33, 32, 195].

Amemiya and Fuller [5] develop a more sophisticated procedure eliminating the essential bias of the maximum likelihood estimators, for a general problem of fitting arbitrary curves to data (again assuming that the noise level $\sigma$ is known). One can check (we omit details) that for circles their procedure reduces to (6.48).

We note that these tricks remove most of the bias (i.e., all the terms of order $\sigma^2$), but there remain leftover terms of higher order, i.e., $\sigma^4$. They may be small, but they do not vanish as $n \to \infty$, thus the resulting estimate is not asymptotically unbiased in the large sample limit. Thus, it is not consistent either.

Several adjustments have been developed to ensure consistency as $n \to \infty$. One, designed for linear and polynomial EIV regression, is described below.

## Adjusted least squares: linear case.

To ensure not only a reduction of the bias, but an asymptotical unbiasedness and consistency in the large sample limit, one can make appropriate adjustments in the estimating procedure.

Suppose one fits a straight line $y = \alpha + \beta x$ to the observed points. The classical regression estimates (Section 1.1) are obtained by the least squares method minimizing

$$\mathscr{F}(\alpha, \beta) = \frac{1}{n} \sum (y_i - \alpha - \beta x_i)^2,$$

which reduces to a system of linear equations

$$
\begin{aligned}
&\alpha + \beta \bar{x} = \bar{y} \\
&\alpha \bar{x} + \beta \bar{x}\bar{x} = \overline{xy},
\end{aligned}
\quad (6.49)
$$

where we use our “sample mean” notation $\bar{x} = \frac{1}{n} \sum x_i,\ \overline{xy} = \frac{1}{n} \sum x_i y_i$, etc.

Now recall that both $x$ and $y$ are observed with errors, i.e., $x_i = \tilde{x}_i + \delta_i$ and $y_i = \tilde{y}_i + \epsilon_i$. In the limit $n \to \infty$, according to the central limit theorem, we have

$$
\begin{aligned}
\bar{x} &= \tilde{x} + \mathscr{O}_P(n^{-1/2}) \\
\bar{y} &= \tilde{y} + \mathscr{O}_P(n^{-1/2}) \\
\overline{xy} &= \tilde{x}\tilde{y} + \mathscr{O}_P(n^{-1/2}),
\end{aligned}
$$

i.e., three random terms in (6.49) converge to their “true” values. But the fourth one does not, because

$$
\begin{aligned}
\overline{xx} &= \frac{1}{n} \sum (\tilde{x}_i + \delta_i)^2 \\
&= \frac{1}{n} \sum \tilde{x}_i^2 + \frac{1}{n} \sum \delta_i^2 + \frac{2}{n} \sum \tilde{x}_i \delta_i \\
&= \frac{1}{n} \sum \tilde{x}_i^2 + \sigma^2 + \mathscr{O}_P(n^{-1/2}),
\end{aligned}
$$

where we used the fact $\mathbb{E}(\delta_i^2) = \sigma^2$. That extra term $\sigma^2$ is the origin of inconsistency and asymptotic biasedness. To eliminate it we adjust the system (6.49) as follows:

$$
\begin{aligned}
&\alpha + \beta \bar{x} = \bar{y} \\
&\alpha \bar{x} + \beta (\overline{xx} - \sigma^2) = \overline{xy},
\end{aligned}
\quad (6.50)
$$
