# 406 Applied Time Series Analysis with R

```
$$\kappa_{jh}^2(f) = \frac{|P_{jh}(f)|^2}{P_j(f)P_h(f)} \quad (10.9)$
```

It should be noted that $\kappa_{jh}^2(f)\le1$ and can be interpreted as a squared correlation-measure of the linear relationship between the random components of $X_{ij}$ and $X_{ih}$ at frequency $f$.

# 10.2.1 Estimating the Mean and Covariance for Stationary Multivariate Processes

We briefly discuss the estimation of the mean $\mu$ and the covariance matrix $\Gamma(k)$ based on a realization of length $n$ from the stationary multivariate process $[X_{ij}; t=0, \pm 1, \pm 2, \dots]$. These estimation procedures are entirely analogous to the corresponding procedures for univariate processes.

# 10.2.1.1 Estimating $\mu$

The natural unbiased estimator of the $m$-component vector $\mu$ is the $m$-component vector $\mathbf{X}$ given by

```
$$\mathbf{X} = \begin{pmatrix}\tilde{X}_1 \ \tilde{X}_2 \ \vdots \ \tilde{X}_m \end{pmatrix}, \quad (10.10)$
```

$	ilde{X}_j = \frac{1}{n}\sum_{t=1}^{n}X_{ij}$. We say that $\mathbf{X}$ is ergodic for $\mu$ if $\mathbf{X}$ converges in the mean-square as $n \to \infty$, that is, if $E[(\mathbf{X}-\mu)(\mathbf{X}-\mu)']\to 0$. Corollary 1.1 gives a sufficient condition for ergodicity in the univariate case, and by applying that to each component of $\mathbf{X}$, it follows that $\mathbf{X}$ is ergodic for $\mu$ if $\lim_{k\to\infty}\gamma_{jh}^2(k)=0$ for each $j$, $1 \le j \le m$.

# 10.2.1.2 Estimating $\Gamma(k)$

It is a common practice to estimate the covariance matrix $\Gamma(k)$ by the $m \times m$ matrix given by

```
$$\mathbf{\hat{\Gamma}}(k) = \begin{pmatrix}\hat{\gamma}_{11}(k) & & \ \vdots & & \hat{\gamma}_{m1}(k) & & \hat{\gamma}_{mm}(k) \end{pmatrix}, \quad (10.11)$
```

$\hat{\gamma}_{ij}(k)=(1/n)\sum_{t=1}^{n-k}(X_{it}-\tilde{X}_i)(X_{jt+k}-\tilde{X}_j)$. Note that the estimator in Equation 10.11 corresponds to the definition of the cross-correlation in