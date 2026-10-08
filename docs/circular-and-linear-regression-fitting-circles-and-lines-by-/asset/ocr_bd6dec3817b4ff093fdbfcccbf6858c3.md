The remainder term $\mathscr{O}_{P}(\sigma^{3})$ in (6.18) is a random variable $\mathscr{R}$ such that $\sigma^{-3} \mathscr{R}$ is bounded in probability; this means that for any $\varepsilon>0$ there exists $A_{\varepsilon}>0$ such that $\mathrm{Pr}\left\{\left|\sigma^{-3} \mathscr{R}\right|>A_{\varepsilon}\right\}<\varepsilon$ for all $\sigma>0$. For instance, the remainder term may have infinite moments, but its typical values are of order $\sigma^{3}$, so we will ignore it in our analysis. The first and second order terms in (6.18) have typical values of order $\sigma$ and $\sigma^{2}$, respectively, and their moments are always finite (because $\mathbf{E}$ is a Gaussian vector).

If we do the expansion (6.18) for the whole vector $\hat{\Theta}$, then $\mathbf{G}_{m}$ would be replaced by an $m \times n$ matrix of the first order partial derivatives, but $\mathbf{H}_{m}$ would become a 3D tensor of the second partial derivatives; to avoid notational complications related to tensor products we deal with each component $\hat{\theta}_{m}$ separately.

**Geometric consistency**. Expansion (6.18) shows that Expansion (6.18) shows that $\hat{\Theta}(\mathbf{X}) \rightarrow \hat{\Theta}(\tilde{\mathbf{X}})$ in probability, as $\sigma \rightarrow 0$. It is convenient to assume that

```
$$\hat{\Theta}(\tilde{\mathbf{X}})=\hat{\Theta} . \quad(6.19)$$
```

Precisely (6.19) means that whenever $\sigma=0$, i.e., the true points are observed without noise, then the estimator returns the true parameter vector, i.e., finds the true curve. Geometrically, (6.19) implies that if there is a curve of type (6.1) that interpolates the data points, then the algorithm finds it.

With some degree of informality, one can assert that whenever (6.19) holds, the estimate $\hat{\Theta}$ is consistent in the limit $\sigma \rightarrow 0$. We call this property *geometric consistency*.

The assumption (6.19) is sometimes regarded a minimal requirement for any sensible fitting algorithm. For example, if the observed points lie on one circle, then every algorithm that we have discussed in Chapters 4 and 5 finds that circle uniquely. Kanatani [100] remarks that algorithms which do not enjoy this property “are not worth considering.”

We recall, however, that the Maximum Likelihood Estimators of the circle parameters, in the context of the structural model, are *not* geometrically consistent (Section 6.3), thus (6.19) is not automatically ensured for every estimator of interest. But we will assume (6.19) in all that follows.

**Bias and variance**. Under our assumption (6.19) we rewrite (6.18) as

```
$$\Delta \hat{\theta}_{m}(\mathbf{X})=\mathbf{G}_{m}^{T} \mathbf{E}+\frac{1}{2} \mathbf{E}^{T} \mathbf{H}_{m} \mathbf{E}+\mathscr{O}_{P}\left(\sigma^{3}\right) \quad(6.20)$$
```

where $\Delta \hat{\theta}_{m}(\mathbf{X})=\hat{\theta}_{m}(\mathbf{X})-\hat{\theta}_{m}$ is the statistical error of the parameter estimate.

The first term in (6.20) is a linear combination of i.i.d. normal random variables (the components of $\mathbf{E}$) that have zero mean, hence it is itself a normal random variable with zero mean.

The second term is a quadratic form of i.i.d. normal variables (such forms have been studied in probability, see e.g., [64, 88, 153, 154]). Since $\mathbf{H}_{m}$ is a