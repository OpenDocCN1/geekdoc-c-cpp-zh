# Applied Time Series Analysis with R

$\Theta(B^{12})$. The coefficients for $\phi_i(B)$, $\lambda_i(B)$, and $	heta(B)$ may need to be obtained using mult.wge before calling gen.arima.wge. For more details, see Appendix 3A.

# 5.4 Random Walk Models

Random walk models have been used for describing the behavior of the stock market, the path traveled by a molecule as it moves through a liquid, and many other applications. In this section, we will define random walk and random walk with drift models and briefly discuss their properties.

# 5.4.1 Random Walk

Let $X_t = 1, 2, \dots$ be defined by

```
$X_t = X_{t-1} + a_t, \quad (5.20)$
```

where $X_0=0$ and $a_t, t=1, 2, \dots$ is a sequence of independent and identically distributed random walk with mean zero and variance $\sigma_a^2$. The name,"random walk," comes from the fact that at time $t-1$, the movement to $t$ is determined by the random quantity $a_t$. It is sometimes convenient to write the model in Equation 5.20 as

```
$X_t = \sum_{k=1}^t a_k, \quad (5.21)$
```

for $t=1, 2, \dots$. From Equation 5.21, it can be seen that $E(X_t)=0$, and the variance of $X_t$ is given by

```
$Var(X_t) = t\sigma_a^2, \quad (5.22)$
```

Thus, the random walk model in Equation 5.20 is nonstationary since $Var(X_t)$ is not constant. It can also be shown that if $1 \le t_1 \le t_2$, then

```
$Cov(X_{t_1}, X_{t_2}) = t_1\sigma_a^2, \quad (5.23)$
```

and

```
$\rho_X(t_1, t_2) = \sqrt{\frac{t_1}{t_2}}, \quad (5.24)$
```

(see Problem 5.12). Consequently, the autocorrelation between $X_{t_1}$ and $X_{t_2}$ depends on time, and the random walk process does not satisfy the stationarity conditions for either variance or autocorrelations. The impact of