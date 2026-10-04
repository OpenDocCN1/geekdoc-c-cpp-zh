284

Applied Time Series Analysis with R

# TABLE 7.1

$\hat{	heta}_{mi}, m=1, \dots; j=1, \dots, \min(m, 8)$ for a Realization of Length
400 from the MA(2) Model $X_t = a_t + 0.2a_{t-2}$ where $\sigma_t^2=1$

$\hat{	heta}_{mj}$

If the true autocorrelations are known, then the $p$ equations for $k=q+1, q+1, \dots, q+p$ can be solved by $\phi_1, \dots, \phi_p$. These are called the extended WYW equations. The extended WYW estimates of the AR parameters are obtained by replacing the true autocorrelations, $\rho_j$, and solving the resulting system of $p$ equations in $p$ unknowns. The sample autocorrelations, $\hat{ho}_j$, are used instead. The WYW estimates arise earlier from the special case in which $q=0$. However, unlike the case $q=0$, when $q>0$ the extended WYW estimates need not result in a stationary model. Choi (1986) gives an algorithm for solution of the extended WYW equations.

# 7.2.3 Tsay-Tiao Estimates of the AR Parameters

Tsay and Tiao (1984) obtained estimates of the AR parameters of an ARMA(p,q) model motivated by iterated AR(k) regressions, and recursively adding MA type terms to an AR(k) model. If $X_t$ follows an ARMA(p,q) model, then an AR(p,q) model

```
$X_t = \sum_{j=1}^p \phi_{jp}^{(0)} X_{t-j} + e_{pt}^{(0)}$
```

$t=p+1, \dots, n$ is initially fit to the data. The least squares estimates of the model parameters are denoted by $\phi_{jp}^{(p)}$. Based upon these estimates, the residuals

```
$\hat{e}_{pt}^{(p)} = X_t - \sum_{j=1}^p \phi_{jp}^{(p)} X_{t-j}$
```