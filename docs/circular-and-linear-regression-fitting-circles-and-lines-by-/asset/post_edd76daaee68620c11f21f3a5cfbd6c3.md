
Lastly, in Step 2 the estimate of $\Theta$ is obtained by minimizing (6.6). Thus we get a curve that minimizes the sum of squares of the distances to the data points. The theorem is proved. $\square$

We denote by $\hat{\Theta}_{MLE}$ the maximum likelihood estimator. As we have just proved, in the functional model it is always obtained by the geometric fit, i.e., by minimizing the sum of squares of the distances from the data points to the curve.

### MLE in the structural model.
Though the structural model is less appropriate for image processing applications, we devote a brief discussion of the maximum likelihood estimation in its context. Quite unexpectedly, in that model the Maximum Likelihood Estimator is *different* from the geometric fit, even if the noise has a Gaussian distribution. We illustrate this fact by a rather striking example.

**Example.** Consider the problem of fitting a circle to data and suppose the distribution of the true points on the true circle is uniform (the least fanciful assumption). Let $\rho$ and $\theta$ denote the polar coordinates attached to the center of the true circle. Then, in the radial structural model, the probability density function $g(\rho, \theta)$ of an observable at the point $(\rho, \theta)$ will be

$$ g(\rho, \theta) = \frac{1}{2\pi} \frac{1}{(2\pi\sigma^2)^{1/2}} \exp\left[-\frac{(\rho - R)^2}{2\sigma^2}\right], $$

where $R$ is the circle's radius. In the $xy$ coordinates the density becomes

$$ f(x, y) = \frac{1}{2\pi(d + R)} \frac{1}{(2\pi\sigma^2)^{1/2}} \exp\left[-\frac{d^2}{2\sigma^2}\right], $$

where $d = \sqrt{(x - a)^2 + (y - b)^2} - R$ denotes the signed distance from the point to the true circle. Note that the extra factor $d + R$ comes from the Jacobian.

For simplicity, assume that $\sigma$ is known. Since the observations are independent, the negative log-likelihood function is

$$ -\log L(a, b, R) = \sum_i \ln(d_i + R) + \sum_i \frac{d_i^2}{2\sigma^2} $$

(constant terms are omitted).

Now suppose that the data points lie *on the true circle*. Then the geometric fit will return the true circle (and so does every algebraic fit discussed in Chapter 5). We will see next that the MLE picks a different circle.

For the true circle, $d_i = 0$, hence the negative log-likelihood is

$$ -\log L(\tilde{a}, \tilde{b}, \tilde{R}) = n \ln \tilde{R}. $$

![](img/86db288e3c266985d1648282179ae4b5_178_0.png)

Figure 6.3 Five data points lie on the true circle (the solid line), but the MLE returns a different circle (the dashed line).

Suppose, in addition, that the data points are clustered along a small arc on the right hand (east) side of the circle; for example let

$$ x_i = \tilde{a} + \tilde{R}\cos(\delta(i/n - 1/2)), \quad y_i = \tilde{b} + \tilde{R}\sin(\delta(i/n - 1/2)), $$

for $i=1,\ldots,n$, where $\delta>0$ is small, see Fig. 6.3. Now consider a circle with parameters $(\tilde{a}+\varepsilon, \tilde{b}, \tilde{R})$. For that circle $d_i = -\varepsilon + \mathcal{O}(\varepsilon\delta^2)$, therefore

$$ -\log L(\tilde{a}+\varepsilon, \tilde{b}, \tilde{R}) = n\ln(\tilde{R}) - \tilde{R}^{-1}n\varepsilon + \mathcal{O}(n\tilde{R}^{-1}\varepsilon\delta^2) + \mathcal{O}(n\sigma^{-2}\varepsilon^2). $$

It is clear that this function decreases when $\varepsilon$ is a small positive number and takes its minimum at $\varepsilon \sim \sigma^2/R$. Thus the MLE fails to find the true circle, even if the true points are observed without noise.

### General comments on the MLE for the structural model.
Our example may give an impression that the Maximum Likelihood Estimators for the structural model are ill-behaved, but this is actually not true. General theorems in statistics guarantee that the MLE have optimal asymptotic properties, as $n \rightarrow \infty$; they are consistent, asymptotically normal, and efficient (have asymptotically minimal possible variance).

A detailed investigation of the MLE, in the context of the structural model for the circle fitting problem, was done in a series of papers by Anderson [6] and Berman and Culpin [16, 18] in the 1980s. They performed an approximate analysis, aided by numerical experiments, which confirmed the excellent behavior of the MLE in the limit $n \rightarrow \infty$. In fact the MLE were found to have smaller variance than that of the geometric circle fit, and even more so if compared to the Kåsa algebraic fit (Section 5.1). When the noise is large (and $n$ is large), the variance of the MLE may be several times smaller than that of the geometric fit [16].

On the other hand, these studies also demonstrate difficulties in the practical computation of the MLE. Anderson [6] describes the MLE by explicit equations only in the simplest case, where the true points are uniformly distributed on the entire circle; even in that case the MLE equations involve modified Bessel functions defined by infinite power series. For other distributions of the true points on the circle, no equations describing the MLE are derived and no practical algorithms for computing the MLE are proposed.

Thus it appeared, at least back in the 1980s, that the structural model MLE, despite having superb statistical properties, were hopelessly impractical. Since then they remain abandoned. Though perhaps now, or in the near future, with more powerful computer resources and software, the structural model MLE of the circle parameters can be revisited and rehabilitated. This interesting approach promises an estimator superior to the geometric fit, at least in some situations.

## 6.4 Distribution and moments of the MLE

After adopting certain models for the distribution of observables (Sections 6.1 and 6.2) and deriving the corresponding MLE (Section 6.3), we can proceed to the main goals of our statistical analysis. In traditional statistics, estimators of unknown parameters are characterized by their probability distributions and especially by their moments; the moments provide such important characteristics as the *bias*, *variance*, and *mean squared error* of an estimate.

Unfortunately, this traditional approach runs into formidable difficulties arising from the nature of our problem; these difficulties are described and illustrated in this section. They prompt statisticians to develop alternative approaches based on various approximations, we will present them in the subsequent sections.

### Exact distribution of the MLE.
Due to the complexity of the curve fitting problems the exact distributions and moments of the maximum likelihood estimators cannot be determined in most cases. Even for the simplest task of fitting a straight line

$$ y = \alpha + \beta x $$

to observed points, the distributions of the MLE $\hat{\alpha}$ and $\hat{\beta}$ are given by overly complicated expressions, which involve doubly infinite power series whose coefficients depend on incomplete Beta functions; see [7].

Exact formulas for the density functions of $\hat{\alpha}$ and $\hat{\beta}$ were derived in 1976 by Andersson [7, 10] who readily admitted that they were “not very informative” [8] and “not very useful” [7]. Instead, Andersson employed Taylor expansion to approximate the distribution function of $\hat{\beta}$, which allowed him to investigate some practical features of this estimator; see our Chapter 2 for a more detailed account.

In the case of fitting nonlinear curves, such as circles and ellipses, there are no explicit formulas of any kind for the maximum likelihood estimators themselves, let alone their probability densities. To our best knowledge, no one has ever attempted to describe the exact distributions of the corresponding MLE (although for the circle fitting problem, some related distributions were studied in [6, 18, 31]).

Now, since exact probability distributions of the MLE are unavailable, one has to follow Anderson [7, 10] and employ the Taylor expansion to construct reasonable approximations; we will do that in Section 6.6.

### Moments of the MLE.
Because exact distributions of the MLE's are intractable, one cannot derive explicit formulas for their moments either (with a few exceptions, though, see next). For example, if one fits a straight line

$$ x \cos \varphi + y \sin \varphi + C = 0,$$

then the distribution of the MLE $\hat{\varphi}$ happens to be symmetric about its true value $\varphi$ (Section 2.4), hence $\mathbb{E}(\hat{\varphi}) = \varphi$; in this rare case the first moment can be found precisely. However, there are no explicit formulas for $\operatorname{Var}(\hat{\varphi})$ even in this case. There are no exact formulas for $\mathbb{E}(C)$ or $\operatorname{Var}(C)$ either, they can only be determined approximately, as we did in Chapter 2.

Furthermore, there is an even more disturbing fact about the moments of MLE's, which may not be easy to digest. Namely, if one describes the straight line by $y = \alpha + \beta x$, then the moments of the corresponding MLE, $\hat{\alpha}$ and $\hat{\beta}$, do not even exist, i.e.,

$$\mathbb{E}(|\hat{\alpha}|) = \mathbb{E}(|\hat{\beta}|) = \infty .$$

This means that these estimators have no mean values or variances. This fact was established by Anderson [7] in 1976, see our Section 1.6.

Anderson's discovery was rather striking; it was followed by heated discussions and a period of acute interest in the linear EIV problem. The basic question was: are the MLE $\hat{\alpha}$ and $\hat{\beta}$ statistically acceptable given that they have infinite mean squared error? (Well, not to mention infinite bias...) And what does the nonexistence of moments mean anyway, in practical terms?

To answer these questions, Anderson, Kunitomo, and Sawa [7, 10, 118] used Taylor expansions up to terms of order 3 and 4 to approximate the distribution functions of the MLE; and the resulting approximate distributions had finite moments. Those approximations remarkably agreed with numerically computed characteristics of the actual estimators (in simulated experiments), at least in all typical cases (see one exception below). Anderson and Sawa [10] noted that their approximations were "virtually exact." We will employ the approximation techniques to more general curves in Section 6.6.

### An artificial example.
To illustrate the idea of Anderson's approximative approach, consider a scalar estimate $\hat{\theta}$ whose density function $f$ is a mixture,

$$f = (1 - p) f_0 + p f_1,$$

where

$$f_0(x) = \frac{1}{\left( 2 \pi \sigma _0^2 \right) ^{1/2}} \exp \left[ -\frac{(x - \mu _0)^2}{2 \sigma _0^2} \right]$$
