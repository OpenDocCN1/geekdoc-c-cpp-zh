
Note that the output corresponding to the G-side model contains only a single covariance parameter. The value is close to 1, which is the variance of the within-subject random effect used in the simulation data. The estimated probability of success is 0.7723. The true value set in the simulation is 0.8. Similarly for the R-side output, the estimated probability of success is 0.7480. Note that both estimates are biased low. This output consists of two covariance parameters. The labeled CS corresponds to the between-subject covariance, and the estimated Residual corresponds to the within-subject variance.

## 9.3 GEE Methodology for Binary and Count Data

For each subject $j$, $j=1,2,...,n$, let $Y_j = (Y_{j,1}, Y_{j,2},...,Y_{j,m_j})$ represent an $m_j$-dimensional column vector of responses, and let $x_j=(x_{j,1}, x_{j,2},...,x_{j,m_j})$ denote an associated $m_j \times k$ matrix of observed covariates, where $x_{j,i}=1,2,...,m_j$ represent a $k$-dimensional row vector. Let $\mu_j$ and $v(\mu_j)$ represent, respectively, the mean and the "natural variance" of $Y_{j,i}$, the latter being variance of $Y_{j,i}$ when they are independent and belong to the exponential family. If $Y_{j,i}$'s were Bernoulli or Poisson-distributed, their corresponding natural variances would be $\pi_{j,i}(1-\pi_{j,i})$ or $\lambda_{j,i}$, respectively. It is further assumed that $\mu_{j,i}$'s are related to the $x_{j,i}$'s through a link function $g()$ such that $g(\mu_j)=x_j\beta$, where $\beta$ is a $k$-dimensional column vector of unknown parameters. The canonical links for the Bernoulli and Poisson distributions as set in earlier chapters, are, the logit and logarithmic functions. Other links for the Bernoulli distribution are the "identity," "probit" and the "complementary log-log" functions. The identity function may also be used as a link function for the Poisson case.

Let $A_j$ represent the $m_j \times m_j$ diagonal matrix of natural variances of the vector $Y_j$, $A_j = \text{diag}(v(\mu_{j,1}), v(\mu_{j,2}),...,v(\mu_{j,m_j}))$. In order to apply the GEE methodology, one needs first to define the correlation structure of $Y_j = (Y_{j,1}, Y_{j,2},...,Y_{j,m_j})$ through an $m_j \times m_j$ "working" correlation matrix $R_j(\alpha)$ such that

$$A_j = A_j^{1/2}R_j(\alpha)A_j^{1/2}\phi,$$

$\alpha$ is a vector of unknown parameters, and $\phi$ is the usual dispersion parameter of distributions in the exponential family. Note that in the case of the Bernoulli, Poisson and Multinomial distributions, $\phi=1$. The variance-covariance matrix $V_j$ (above) would equal to the variance-covariance matrix of $\mathbf{y}_j$, if $\mathbf{R}(\{\alpha})$ were the true correlation matrix for the $\mathbf{y}_j$'s. Then, define the generalized estimating equations as

$$\sum_{j=1}^n \mathbf{D}_j^T \mathbf{V}_j^{-1} [\mathbf{y}_j - \boldsymbol{\mu}_j(\boldsymbol{\beta})] = \mathbf{0}, \quad (9.2)$$

Where $\boldsymbol{\mu}_j = (\mu_{j,1}, \mu_{j,2}, ..., \mu_{j,m_j})^T$, $\mathbf{D}_j$ represents the $m_j \times k$ matrix of first derivatives of $\boldsymbol{\mu}_j$ with respect to $\beta$, that is $\mathbf{D}_j = \frac{\partial\boldsymbol{\mu}_j}{\partial\beta}$, and $\mathbf{V}_j$ is defined as in equation (9.1). Both procedures, GENMOD and GLIMMIX, handle a general form of (9.1) by allowing each element of $\mathbf{Y}_j = (Y_{j,1}, Y_{j,2}, ..., Y_{j,m_j})^T$ to have its own weight. Though with each $\mathbf{y}_j$ there is an $m_j \times m_j$ diagonal matrix of weights $\mathbf{W}_j$ so that

$$\mathbf{V}_j = \mathbf{W}_j^{1/2} \mathbf{R}(\{\alpha\}) \mathbf{W}_j^{1/2}\phi, \quad (9.3)$$

The reader should be aware that numerically solving the generalized estimating equations (9.2) for $\beta$ does not yield a maximum likelihood estimator of $\beta$ but it yields a Quasi-likelihood type estimator. As mentioned in the introduction, GEE does not assume a probability distribution for the data; therefore, it does not accommodate likelihood-based inferences.

## 9.4 Estimation Methods

In SAS there are two methods for computing the model-estimators used in the calculation of the variance estimate. The GENMOD procedure uses a moment-based methodology based on seminal papers by Liang and Zeger (1986), and Zeger (1988). On the other hand, one of the two used in GLIMMIX is pseudo-likelihood estimation based on linearization (Weiss and O'Connell, 1993). We begin with the following algorithm used by GENMOD for fitting the model by GEE. Note that this is not a likelihood-based method of estimation, so inferences based on likelihood are not possible for GEE methods. The algorithm used by GENMOD can be summarized as follows:

- 1. Compute an initial estimate of $\beta$ with an ordinary linear model assuming independence among the repeated measurements, i.e., $\mathbf{R}(\{\alpha\})$ is an identity $m_j \times m_j$ matrix.
- 2. Compute the working correlations $\mathbf{R}(\{\alpha\})$ on the standardized residuals, current $\beta$, and the assumed structure of $\mathbf{R}(\{\alpha\})$.
- 3. Compute the estimate of the covariance in equation (9.3).
- 4. Update $\beta_{(s+1)} = \beta_{(s)} + (\mathbf{D}^T \mathbf{V}^{-1} \mathbf{D})^{-1} \mathbf{D}^T \mathbf{V}^{-1} (\hat{\mathbf{y}} - \hat{\boldsymbol{\mu}})$.
- 5. Repeat 2-4 until convergence is achieved.

The model-based estimator of the variance-covariance matrix of $\beta$ is $\left(\hat{\mathbf{D}}^T\hat{\mathbf{V}}^{-1}\hat{\mathbf{D}}\right)^{-1}$. This is the GEE equivalent of the inverse of the Fisher information matrix that is often used in GLMs as an estimator of the covariance of the maximum likelihood estimator of $\beta$. It is a consistent estimator of the covariance matrix of $\beta$ if the mean and the working correlation matrix are correctly specified. The "robust," "empirical," or "sandwich" variance-covariance matrix is

$$\overline{\text{Var}}(\hat{\beta}) = \hat{\mathbf{H}}^T\hat{\mathbf{G}}^{-1}\hat{\mathbf{H}}^{-1}, \quad (9.4)$$

where $\hat{\mathbf{H}} = \left(\hat{\mathbf{D}}^T\hat{\mathbf{V}}^{-1}\hat{\mathbf{D}}\right)$ and $\hat{\mathbf{G}} = \hat{\mathbf{D}}^T\hat{\mathbf{V}}^{-1}(\hat{\mathbf{y}}-\hat{\boldsymbol{\mu}})\hat{\mathbf{V}}^{-1}\hat{\mathbf{D}}$. The variance estimator (9.4) has the desirable property of being a consistent estimator of the covariance matrix of $\beta$, even if the working correlation matrix is misspecified. We refer to the "Details: GENMOD Procedure" of the SAS* documentation. For further information about robust variance estimate the reader is referred to Liang and Zeger (1986), and Zeger (1988). Additional useful references are Zeger, Liang, and Albert (1988), Royall (1986), and White (1982). See also by Hardin and Liang (2003).

If $\mathbf{y}_j = (y_{j1}, y_{j2}, \dots, y_{jm_j})^\top$ represents a realization of the random vector $\mathbf{Y}_j = (Y_{j1}, Y_{j2}, \dots, Y_{jm_j})^\top$, the GENMOD procedure currently supports the following working correlation structures $R_j(\alpha):$

| Working Correlation Structure | $R_j(\alpha)$ |
| :--- | :--- |
| Independent | $\text{Corr}(Y_{ji}, Y_{jk}) = \begin{cases} 1 & i=k \\ 0 & i \neq k \end{cases}$ |
| Exchangeable | $\text{Corr}(Y_{ji}, Y_{jk}) = \begin{cases} 1 & i=k \\ \alpha & i \neq k \end{cases}$ |
| Unstructured | $\text{Corr}(Y_{ji}, Y_{jk}) = \begin{cases} 1 & i=k \\ \alpha_{ik} & i \neq k \end{cases}$ |
| Autoregressive AR(1) | $\text{Corr}(Y_{ji}, Y_{j,i+t}) = \alpha^t$ $\text{for } t=0,1,2,\dots,m_j$ |
| m-dependent | $\text{Corr}(Y_{ji}, Y_{j,i+t}) = \begin{cases} 1 & t=0 \\ \alpha_i & t=1,2,\dots,m (m \le m_j) \\ 0 & t>m \end{cases}$ |
| Fixed | $\text{Corr}(Y_{ji}, Y_{jk}) = r_{ik}$ where $r_{ik}$ is the $(i,k)$-element of a constant, user-specified correlation matrix $R_0$ |
[/