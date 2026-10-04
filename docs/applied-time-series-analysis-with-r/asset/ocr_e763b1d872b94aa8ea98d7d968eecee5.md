# Vector-Valued (Multivariate) Time Series

and Equation 10.27 becomes

```
$$\hat{X}_{t01}(\ell) = 0.9\hat{X}_{t01}(\ell-1) + 0.6\hat{X}_{t02}(\ell-1) - 0.041.$$
$\hat{X}_{t02}(\ell) = -0.3\hat{X}_{t01}(\ell-1) + 0.7\hat{X}_{t02}(\ell-1) = 0.129.$$ (10.28)
```

Using the fact that $\hat{X}_{75,1}(0) = X_{75,1} = 4.51$ and $\hat{X}_{75,2}(0) = X_{75,2} = -0.59,$
it follows that

```
$$\hat{X}_{75,1}(1) = 0.9(4.51) + 0.6(-0.59) - 0.041 = 3.664,$$
$\hathat{X}_{75,2}(1) = -0.3(4.51) + 0.7(-0.59) + 0.129 = -1.637,$$
$\hathat{X}_{75,1}(2) = 0.9(3.664) + 0.6(-1.637) - 0.041 = 2.274,$$
$\hathat{X}_{75,2}(2) = -0.3(3.664) + 0.7(-1.637) + 0.129 = -2.116,$$$
```

etc. For example $\hat{X}_{75,1}(t)$ and $\hat{X}_{75,2}(t)$ are shown in Figure 10.6 where it can be seen that the forecasts follow the general pattern of the data and eventually decay as the stationary AR(p) case.

As in the univariate case, the forecast $\hat{X}_t(f)$ in Equation 10.24 can be expressed in terms of the multivariate general linear process form in Equation 10.17. Specifically, $\hat{X}_t(f)$ can be expressed as

```
$$\hat{X}_t(f) = \mu + \sum_{j=1}^{f} \Psi_j \mathbf{a}_{t-j},$$ (10.29)
```

![](bbox=[0.158, 0.555, 0.829, 0.853])

**FIGURE 10.6**nRealization shown in Figure 10.3 from the bVAR(1) model in Example 10.2 along with forecasts of the next 25 values. (a) Realization and forecasts from $X_{\eta}$. (b) Realization and forecasts from $X_2$.