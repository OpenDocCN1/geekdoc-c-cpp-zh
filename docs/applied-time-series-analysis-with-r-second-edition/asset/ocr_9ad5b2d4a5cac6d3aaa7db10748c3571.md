and stationary multivariate general linear process if it is given by

$$X_t - \boldsymbol{\mu} = \sum_{j=0}^{\infty} \boldsymbol{\Psi}_j \mathbf{a}_{t-j},$$ (10.6)

where $\mathbf{a}_t$ is multivariate white noise and the $\Psi'_j$s are $m \times m$ matrices, such that $\boldsymbol{\Psi}_0 = \mathbf{I}$ (the $m \times m$ identity matrix) and whose components are absolutely summable. That is, letting $\psi_j(k,l)$ denote the element in the $k$th row and $l$th column of $\Psi_j$, then $\sum_{j=0}^{\infty} |\psi_j(k,l)| < \infty$ for $1 \le k, l \le m.$

# Definition 10.5

Let $\{X_t; t = 0, \pm 1, \pm 2, \dots\}$ be a causal stationary multivariate process with covariance matrix $\boldsymbol{\Gamma}(k)$ given in Equation 10.1 and where $\sum_{k=-\infty}^{\infty} |\gamma_{jh}(k)| < \infty$ for $1 \le j, h \le m$. For $0 \le f \le 0.5$, the power spectrum of $\mathbf{X}_t$ is given by

$$\boldsymbol{P}_X(f) = \sum_{k=-\infty}^{\infty} e^{-2\pi i f k} \boldsymbol{\Gamma}(k).$$ (10.7)

Note that in the multivariate case, $\boldsymbol{P}_X(f)$ in Equation 10.7 is often called the spectral density. For consistency of notation with the univariate case, we will refer to it as the spectrum. Note also that $\boldsymbol{P}_X(f)$ is an $m \times m$ matrix for each $f$. Analogous to Equation 1.28 for the univariate case, it can be shown that

$$\boldsymbol{\Gamma}(k) = \int_{-0.5}^{0.5} e^{2\pi i f k} \boldsymbol{P}_X(f) df,$$ (10.8)

where $i = \sqrt{-1}$. The $jh$th element of $\boldsymbol{P}_X(f)$ is given by

$$P_{jh}(f) = \sum_{k=-\infty}^{\infty} e^{-2\pi i f k} \gamma_{jh}(k),$$ where $|f| \le 0.5$, and the $\gamma_{jh}(k)$'s are defined following Equation 10.1. Note that $P_{jj}(f)$ is the usual spectrum of the univariate time series $X_{tj}$, while if $j \ne h$ then