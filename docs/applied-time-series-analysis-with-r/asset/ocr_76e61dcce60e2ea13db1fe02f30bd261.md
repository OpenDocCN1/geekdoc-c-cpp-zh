# Forecasting 235

Whenever $j = 0, \dots, \ell - 1$, the forecast errors may be correlated.

+   - $e_{t_0}(\ell_1)$ and $e_{t_0}(\ell_2)$ are correlated, that is, forecast errors from the same origin are correlated.

+   - The “best” mean squared error (MSE) forecast” for $\sum_{k=1}^m \alpha_k \hat{X}_{t_0+k}$ from origin $t_0$ is given by $\sum_{k=1}^m \alpha_k \hat{X}_t(k)$. As an example, if $X_t$ represents monthly sales, then (i) states that from forecast origin $t_0$, the “best” forecast for next quarter’s sales, that is, for $X_{t_0+1} + X_{t_0+2} + X_{t_0+3}$ is $X_{t_0}(1) + X_{t_0}(2) + X_{t_0}(3)$.

# 6.4 $\pi$-Weight Form of the Forecast Function

A stationary and invertible process can be written in the $\pi$-weight form

```
$$\sum_{j=0}^{\infty} \pi_j(X_{t-j} - \mu) = a_t,$$
```

which was previously given in Equation 3.83. Therefore, since $\pi_0 = 1$, Equation 6.15 can be written as

```
$X_t = \mu - \sum_{j=1}^{\infty} \pi_j(X_{t-j} - \mu) + a_t,$$
```

which leads to the forecasting formula

```
$$\hat{X}_{t_0}(\ell) = \mu - \sum_{j=1}^{\infty} \pi_j(\hat{X}_{t_0}(\ell-j) - \mu),$
```

where, as before, $\hat{X}_{t_0}(\ell) = X_{t_0+\ell}$, for $\ell \le 0$. The form in Equation 6.16 is similar to the $\psi$-weight form in Equation 6.9 in it involves an infinite summation and is based on the unrealistic assumption that $X_{t_0}, X_{t_0-1}, \dots, X_1, X_0, X_{-1} \dots$ are known. Then, the following truncated version of the forecast function is used in practice.

Truncated Version of the Forecast Equation

```
$$\hat{X}_{t_0}^{(T)}(\ell) = \bar{X} - \sum_{j=1}^{t_0-1+\ell} \pi_j(\hat{X}_{t_0}^{(T)}(\ell-j) - \bar{X}),,$$
```