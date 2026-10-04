For example, if $t_0 = n$, then using Equation 6.17, it follows that

```
$\hat{X}_n^{(T)}(1) = ar{X} - \pi_1(X(n)-ar{X}) - \pi_2(X(n-1)-ar{X}) - \cdots - \pi_n(X(1)-ar{X})$$\n$\hat{X}_n^{(T)}(2) = ar{X} - \pi_1(\hat{X}_{t_0}^{(T)}(1)-ar{X}) - \pi_2(X(n)-ar{X}) - \cdots - \pi_{n+1}(X(1)-ar{X}),$
```

NOTES: the $\pi$-weight version of the forecast function is appropriately used when the $\pi$-weights damp quickly quickly so that $\pi$'s are essentially zero for $j>\ell$, which should generally hold for stationary and invertible ARMA processes when $t_0$ is sufficiently large. This form of the forecast function is useful for forecasting based on long memory models (see Section 11.6).

# 6.5 Forecasting Based on the Difference Equation

If $X$, is a stationary, invertible ARMA$(p,q)$ process, then Equation 6.9 is an expression for the best predictor of $X_{t_0+\ell}$ given $X_{t_0,t_0+\ell-1}$ in terms of the general linear process or “infinite moving average” representation of the process. $\hat{X}_t(\ell)$, can also be written in terms of the difference equation satisfied by $\phi(B)X_t = 	heta(B)a_t$, and hence is more useful in practice. Suppose $X$ satisfies $\phi(B)B = X_t = 	heta(B)a_t$, and hence\u2013.

```
$X_{t_0+\ell} - \phi_1 X_{t_0+\ell-1} - \cdots - \phi_p X_{t_0+\ell-p} = a_{t_0+\ell} - \theta_1 a_{t_0+\ell-1} - \cdots - \theta_p a_{t_0+\ell-p}$.
```

Taking conditional expectations, we obtain

```
$E_{t_0}[X_{t_0+\ell} - \phi_1 X_{t_0+\ell-1} - \cdots - \phi_p X_{t_0+\ell-p}] = E_{t_0}[a_{t_0+\ell} - \theta_1 a_{t_0+\ell-1} - \cdots - \theta_p a_{t_0+\ell-p}].\n\n(6.18)
```

This can be written as

```
$\hat{X}_{t_0}(\ell) = \phi_1 \hat{X}_{t_0}(\ell-1) + \phi_2 \hat{X}_{t_0}(\ell-2) + \cdots + \phi_p \hat{X}_{t_0}(\ell-p)$$\n$+ E_{t_0}[a_{t_0+\ell} - \theta_1 E_{t_0}[a_{t_0+\ell-1}] - \cdots - \theta_p E_{t_0}[a_{t_0+\ell-p}]],\n\n(6.19)
```

where

```
$\hat{X}_{t_0}(k) = X_{t_0+k}, \quad k \le 0$,
```