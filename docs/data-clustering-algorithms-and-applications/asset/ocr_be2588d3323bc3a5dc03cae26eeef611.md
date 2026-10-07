# Probabilistic Models for Clustering

![](bbox=[0.21966999999999998, 0.09333, 0.7803300000000001, 0.28332999999999997])

**FIGURE 3.2 (See color insert):** (a) Plots of the univariate Gaussian distribution given by (3.8) for various parameters of $\mu$ and $\sigma$, and (b) contours of the multivariate (2-D) Gaussian distribution given by (3.9) for various parameters of $\mu$ and $\Sigma$.

where $\mu$ is the mean and $\sigma^2$ is the variance. Figure 3.2(a) shows plots of the Gaussian distribution for various values of the parameters. For a $D$-dimensional vector $x$, the multivariate Gaussian distribution takes the form

```
$$\mathcal{N}(x|\mu,\Sigma)=\frac{1}{(2\pi)^{D/2}|\Sigma|^{1/2}}\\left[-\frac{1}{2}(x-\mu)^T\Sigma^{-1}(x-\mu)\right],$ (3.9)$
```

where $\mu$ is a $D$-dimensional mean, $\Sigma$ is a $D \times D$ covariance matrix, and $|\Sigma|$ denotes the determinant of $\Sigma$. Figure 3.2(b) shows contours of the Gaussian distribution for various values of the parameters.

In the Gaussian mixture model, each component is represented by the parameters of a multivariate Gaussian distribution $p(x_k|\theta_k)=\mathcal{N}(x_k|\mu_k,\Sigma_k)$. Based on (3.1), the Gaussian mixture distribution can be written as a linear superposition of Gaussians in the

```
$p(x_n|\Theta)=\sum_{k=1}^K \pi_k\mathcal{N}(x_n|\mu_k,\Sigma_k).$ (3.10)$
```

For a set of observations $x$, the log-likelihood is given by

```
$l(\Theta)=\log p(x|\Theta)=\sum_{n=1}^N\log\sum_{k=1}^K \pi_k\mathcal{N}(x_n|\mu_k,\Sigma_k).=\sum_{n=1}^N\log\sum_{k=1}^K \gamma_{nk}.$ (3.11)$
```

To find likelihood solutions that are valid at local maxima, we compute the derivatives of $\log p(x|\mu,\Sigma)$ with respect to $\mu_k$, $\mu_k$, and $\Sigma_k$, respectively. The derivative with respect to $\mu_k$ is given by

```
$$\frac{\partial l}{\partial\mu_k}=\sum_{n=1}^N\frac{\pi_k\mathcal{N}(x_n|\mu_k,\Sigma_k)}{\sum_{j=1}^N\pi_j\mathcal{N}(x_n|\mu_j,\Sigma_j)}=\sum_{n=1}^N\gamma_{nk}\Sigma_k^{-1}(x_n-\mu_k),$
```

where we have (3.9) and (3.5) for the Gaussian distribution and the responsibilities (i.e., posterior probabilities), respectively. Setting this derivative to zero and multiplying by $\Sigma_k$, we obtain

```
$$\mu_k=\frac{\sum_{n=1}^N\gamma_{nk}x_n}{\sum_{n=1}^N\gamma_{nk}}.$ (3.12)$
```

©2014 by Taylor & Francis Group, LLC