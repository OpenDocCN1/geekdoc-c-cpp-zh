# 6.8 Forecasts Using ARUMA(p,d,q) Models

Although the forecasting results obtained in Sections 6.1 through 6.7 are for ARMA(p,q) models, which are by definition stationary, the ARUMA(p,d,q) models of Section 5.2 are also an important class of models for which forecasts are of interest. Suppose that X_t follows an ARUMA(p,d,q) model

```
$$\phi(B)\lambda(B)(X_t - \mu) = \theta(B)a_t,\tag{6.35}$$
```

where φ(z) is a pth-order polynomial for which all the roots of φ(z) = 0 lie outside the unit circle. In addition, λ(z) is a dth-order polynomial (d > 0) with all roots of λ(z) = 0 on the unit circle. Let φ^{(u)}(B) = φ(B)λ(B), so that φ^{(u)}(B) is a (p + d)th-order operator with coefficients, say φ_1^{(u)}, φ_2^{(u)}, …, φ_{p+d}^{(u)}. Consider Equation 6.35 as a limit of stationary models

```
$$\phi(B)\lambda_m(B)(X_t^{(m)} - \mu) = \theta(B)a_t,$$
```

where the d roots of λ_m(z) = 0 are outside the unit circle but approach the roots of λ(z) = 0 (on the unit circle) as m → ∞. From Equation 6.21, we obtain the “limiting” forecast equation

```
$$\hat X_{t_0}(\ell)=\sum_{j=1}^{p+d}\phi_j^{(u)}\hat X_{t_0}(\ell - j)-\sum_{j=\ell}^{q}\theta_jE_{t_0}[a_{t_0+\ell-j}]+\left(1-\sum_{j=1}^{p+d}\phi_j^{(u)}\right)\mu.$$
```

As in the stationary case, in practice, we use the forecast formula

```
$$\hat X_{t_0}(\ell)=\sum_{j=1}^{p+d}\phi_j^{(u)}\hat X_{t_0}(\ell - j)-\sum_{j=\ell}^{q}\theta_j\hat a_{t_0+\ell-j}+\left(1-\sum_{j=1}^{p+d}\phi_j^{(u)}\right)\bar X,\tag{6.36}$$
```

where the \hat a_t s are given by