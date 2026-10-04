# Parameter Estimation

option in arima is to obtain ML but conditional sums-of-squares estimates can also be obtained. See the R documentation but realize that the signs of the MA parameters estimates should be changed to match the model used in this book for the MA parameters.

# 7.3.2 ML Estimation Using the Innovations Algorithm

The exact likelihood function in the ARMA$(p,q)$ case can be expressed in terms of the innovations algorithm (see Brockwell and Davis, 1991) for calculating one-step ahead forecasts. The log-likelihood function can be written as

```
$l(\phi, \theta, \sigma_a^2) = -\frac{n}{2}\ln(2\pi\sigma_a^2) - \frac{1}{2}\sum_{t=0}^{n-1}\ln(r_t) - \frac{\sigma_a^2}{2}\sum_{t=1}^{n}\frac{(X_t - \hat{X}_{t-1}(1))^2}{r_{t-1}}, \quad (7.43)$
```

where, using the notation of Chapter 6, $\hat{X}_{t-1}(1)$ is the one-step ahead forecast for $X_t$ (using the $\phi'_j$ and $	heta'_s$)

```
$r_t = \frac{E[X_{t+1} - \hat{X}_t(1)]^2}{\sigma_a^2}$
```

Taking the partial derivative of $l(\phi, \theta, \sigma_a^2)$ with respect to $\sigma_a^2$ results in

```
$\hat{\sigma}_a^2 = \frac{1}{n}S_u(\\hat{\phi}, \hat{	heta}), \quad (7.44)$
```

where

```
$S_u(\\hat{\phi}, \hat{	heta}) = \sum_{t=1}^{n}\frac{(X_t - \hat{X}_t(1))^2}{r_{t-1}}$
```

is evaluated at the ML estimates of the $\phi'_s$ and $	heta'_s$. By inserting $\sigma^2$ in Equation 7.44 into Equation 7.43, it can be seen that the ML estimates of the $\phi'_s$ and $	heta'_s$ are those values that minimize the reduced likelihood

```
$l_r(\phi, \theta) = \ln(n^{-1}S_u(\phi, \theta)) + n^{-1}\sum_{t=1}^{n}\ln r_{t-1}$.
```