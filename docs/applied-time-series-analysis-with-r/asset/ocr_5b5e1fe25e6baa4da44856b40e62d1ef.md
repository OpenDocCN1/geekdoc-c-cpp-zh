# Model Identification 329

procedures for fitting ARUMA(p,d,q) models. Recall that an ARUMA(p,d,q) model is specified by

```
$\phi(B)\lambda(X_t - \mu) = \theta(B)a_t,$$
```

where
$\phi(B)$ and $\theta(B)$ are $p$ and $q$th order operators, respectively.
All the roots of $\phi(z) = 0$ and $\theta(z) = 0$ are outside the unit circle.
All roots of $\lambda(z) = 1 - \lambda_1z - \dotsdots - \lambda_qz^q = 0$ lie on the unit circle.

To begin this discussion, we recall the Finley–Quinn theorem satisfy (Theorem 5.1) that if $p > d$, the extended autocorrelations, $\rho_t$, satisfy a lower order difference equation than $p$. It was also seen in Example 3.12 that the stationary components are often “hidden” by nonstationary components, and in Example 7c, we noted that roots near the unit circle can cause parameter estimation problems.

As a consequence of the comments in the previous paragraph, it follows that model identification in the presence of nonstationarity or near nonstationarity must be done carefully. We make the following general comments in this regard:

General comments:

+   1. ML (and Burg/TT) estimates are better than YW (or extended YW) in the nonstationary or near stationary case. (See the estimation results in Tables 7.6 and 7.7)
2. Model ID techniques (such as the Box–Jenkins procedure) that are based on YW-type estimation can be misleading in the presence of nonstationary or near-nonstationary models. AIC using ML (or Burg) estimates for strictly AR models will not be as susceptible to nonstationarity or near nonstationarity.
3. The decision whether to fix a stationary model or a stationary model that has roots to the unit circle will often depend on the application, that is, the physical problem being considered.
4. YW and Burg estimates of the parameters of an AR model will always produce stationary models.
5. Indications of nonstationarity or near nonstationarity include
   a. Slowly damping autocorrelations.
   b. Realizations exhibiting wandering or strong cyclic behavior.

Because of items (1) and (2), we will use ML (and sometimes YW in the AR case) in our examples. We will further discuss these ideas in the following material.