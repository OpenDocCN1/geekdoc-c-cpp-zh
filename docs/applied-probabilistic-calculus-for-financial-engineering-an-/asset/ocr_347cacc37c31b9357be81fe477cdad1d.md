following formula:

$r \sim N(\mu, \Sigma)$  (3.75)

$\mu = \pi + \varepsilon$  (3.77)

These prior returns are normally distributed around $\pi$ with a disturbance value $\varepsilon$. Figure 3.27 shows the distribution of the actual mean about the estimated mean of 5% with a standard deviation of 2% (or a variance of 0.0004). Clearly, this is not a precise estimate from the width of the peak. One may complete the reference model by defining $\Sigma_r$ as the variance of the returns about the initial estimate $\pi$.

From (3.77) and the assumption above that $\varepsilon$ and $\mu$ are not correlated, the formula for calculating $\Sigma_\pi$ is

$\Sigma_r = \Sigma + \Sigma_\pi$  (3.78)

(3.78) shows that the proper relationship between the variances is ($\Sigma_r \ge \Sigma$, $\Sigma_\pi \ge 0$).

One may check the reference model at the boundary conditions to ensure that it is correct. In the absence of estimation error, that is, $\varepsilon = 0$, $\Sigma_r = \Sigma$. As the estimate gets worse, if $\Sigma_\pi$ increases, then $\Sigma_r$ also increases.

For the Black–Litterman model expected return, the canonical reference model is

$r \sim N(\pi, \Sigma_r)$  (3.79)

![](bbox=[0.15, 0.78, 0.85, 0.92])

Figure 3.27 The estimated mean and the distribution of the actual mean about the estimated mean $\varepsilon_r$ which is normally distributed with mean 0 and variance $\Sigma_\pi$ and is assumed to be uncorrelated with $\mu$.