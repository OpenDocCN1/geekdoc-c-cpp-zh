The comment in (a) relates to the fact mentioned at the beginning of this chapter, that our forecasting formulas are based on a known model. The estimation of $a_t$, proceeding by noting that for an ARMA(p,q) model,

```
$X_t = \sum_{j=1}^{p} \phi_j X_{t-j} + a_t - \sum_{j=1}^{q} \theta_j a_{t-j} + \left(1 - \sum_{j=1}^{p} \phi_j\right) \mu,$$
```

which can be rewritten as

```
$a_t = X_t - \sum_{j=1}^{p} \phi_j X_{t-j} + \sum_{j=1}^{q} \theta_j a_{t-j} - \left(1 - \sum_{j=1}^{p} \phi_j\right) \mu.$
```

So, for $t \le t_0, E_0[a_t] = (a_t)$ is estimated by

```
$$\hat{a}_t = \begin{cases} 0, t \le p \ X_t - \sum_{j=1}^{p} \phi_j X_{t-j} + \sum_{j=1}^{q} \theta_j a_{t-j} - \left(1 - \sum_{j=1}^{q} \phi_j\right) \hat{X}_t, t = \max(p+1,q+1), \dots, t_0. \end{cases}$
(6.23)
```

Moreover, from Equation 6.20, since $E_0[a_t] = 0$ for $t > t_0$, we define

```
$$\hat{a}_t = 0, t > t_0.$
```

This leads to the following.

# 6.5.2 Basic Difference Equation Form for Calculating Forecasts from an ARMA(p,q) Model

```
$$\hat{X}_{t_0}(\ell) = \sum_{j=1}^{p} \phi_j \hat{X}_{t_0}(\ell-j) - \sum_{j=1}^{q} \theta_j \hat{a}_{t_0+\ell-j} + \left(1 - \sum_{j=1}^{p} \phi_j\right) \hat{X}.$\n(6.24)
```

Notice that the $\hat{a}_i$'s enter the calculation of the forecasts only when there are moving average terms in the model. The use of Equation 6.24 for calculating forecasts is illustrated in the two examples. It should be noted that an improved method of calculating the $\hat{a}_i$'s, based on backcasting, is discussed in Section 74.