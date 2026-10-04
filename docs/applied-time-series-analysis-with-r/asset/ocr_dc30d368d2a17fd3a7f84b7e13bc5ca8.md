# 58 Applied Time Series Analysis with R

1.15 Let X be a random variable with mean $\mu$ and variance $\sigma^2 < \infty$, Define $Z_t = X$ for all $t$ $t \in I$ where $I=1, 2, \dots$

+   a. Show that $Z_t = X$ is strictly and weakly stationary
b. Find the autocorrelation function
c. Draw a “typical” realization
d. Determine whether $ar{Z}$ is ergodic for $\mu$

+   1.16 Let $Y_t = a + bt + X$, where $X$, is a covariance stationary process
a. Is $Y_t$ covariance stationary? Why or why not?
b. Let $Z_t = Y_t - Y_{t-1}$. Is $Z_t$, covariance stationary? Why or why not?

$X_t^{(1)} = a_t - \theta_{a_{t-1}}$
nX_t^{(2)} = a_t - \frac{1}{\theta_{a_{t-1}}}$

where $a$, is a white noise process with zero mean and variance $\sigma_a^2 < \infty$.
Show that $X_t^{(1)}$ and $X_t^{(2)}$ have the same autocorrelation functions

1.18 Show that $cos(2\pi.3k) = cos(2\pi.3k)$ at the integers

1.19 Show that for a covariance stationary process $\{X_t, t=0, \pm1, \pm2, \dots\}$
the following could hold:

+   a. $P_X(-f) = P_X(f), |f| \leq 0.5$.$\nS_X(f) = S_X(-f), |f| \leq 0.5$.$\nb. $P_X(f) = \sigma_X^2 + 2\sum_{k=1}^{\infty} \gamma_k cos(2\pi fk), |f| \leq 0.5$.$\n$S_X(f) = 1 + 2\sum_{k=1}^{\infty} \gamma_k cos(2\pi fk), |f| \leq 0.5$.

+   c. $\gamma_k = \int_{-0.5}^{0.5} P_X(f)exp(2\pi ifk)df$.$\n\rho_k = \int_{-0.5}^{0.5} S_X(f)exp(2\pi ifk)df$.

+   d. $\sigma_X^2 = \int_{-0.5}^{0.5} P_X(f)df$.$\n1 = \int_{-0.5}^{0.5} S_X(f)df$.