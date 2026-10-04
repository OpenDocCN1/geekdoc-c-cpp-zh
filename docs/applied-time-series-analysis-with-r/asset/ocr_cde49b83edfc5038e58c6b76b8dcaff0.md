# 444 Applied Time Series Analysis with R

mean-squared error $E[(X_t - \sum_{i}^t a_i Y_i)^2]$ is a minimum. A similar result follows when the univariate random variables are replaced by their vector counterparts. That is, if $Y_{t-j}, \dots, Y_t$ are jointly multivariate normal, then the conditional expectation $E[X_t|Y_t]$ is the linear combination $\sum_{i}^t a_i Y_i$ such that $E[(X_t - \sum_{i}^t a_i Y_i)(X_t - \sum_{i}^t a_i Y_i)]$ is a minimum. For prediction, we can find

```
$\Gamma_{t-1}^{-1} = E[X_t|Y_1, \dots, Y_{t-1}],$
```

which has the associated mean-squared error

```
$\Gamma_{t-1}^{-1} = E\left[(X_t - \hat{X}_{t-1})(X_t - \hat{X}_{t-1})\right]$$
```

From Equation 10.48, it follows that

```
$\hat{X}_{t-1}^{-1} = E[X_t|Y_1, \dots, Y_{t-1}]\n= E[FX_{t-1} + V_t|Y_1, \dots, Y_{t-1}]\n= F\hat{X}_{t-1}^{-1},$
```

since $E[V_t|Y_1, \dots, Y_{t-1}] = 0$, giving the relationship in Equation 10.50. Now,

```
$\Gamma_{t-1}^{-1} = E\left[(X_t - \hat{X}_{t-1})(X_t - \hat{X}_{t-1})\right]$\n= E\left[(FX_{t-1} + V_t - F\hat{X}_{t-1}^{-1})(FX_{t-1} + V_t - F\hat{X}_{t-1}^{-1})\right]\n= E\left[F(X_{t-1} - \hat{X}_{t-1}^{-1}) + V_t)(F(X_{t-1} - \hat{X}_{t-1}^{-1}) + V_t)\right]\n= E\left[F(X_{t-1} - \hat{X}_{t-1}^{-1})(X_{t-1} - \hat{X}_{t-1}^{-1})F'\right] + E[V_t V_t']\n=F\Gamma_{X_{t-1}^{-1}^{-1}}F' + F\Gamma_v,$
```

giving Equation 10.51. Note also that

```
$\hat{Y}_{t-1}^{-1} = E[Y_t|Y_1, \dots, Y_{t-1}]\n= E[GX_t + W_t|Y_1, \dots, Y_{t-1}]\n=G\hat{X}_{t-1}^{-1},$
```

since $E[W_t|Y_1, \dots, Y_{t-1}] = 0$.