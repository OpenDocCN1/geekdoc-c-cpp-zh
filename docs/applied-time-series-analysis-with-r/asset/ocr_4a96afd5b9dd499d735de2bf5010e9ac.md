# Vector-Valued (Multivariate) Time Series 445

For filtering, we define the innovations

```
$$\mathbf{I}_t = \mathbf{Y}_t - \hat{\mathbf{Y}}_{t-1}$$
$= \mathbf{Y}_t - \mathbf{G}_t\hat{\mathbf{X}}_{t-1}$$
$= \mathbf{G}_t\mathbf{X}_t + \mathbf{W}_t - \mathbf{G}_t\hat{\mathbf{X}}_{t-1}$$
$= \mathbf{G}_t(\mathbf{X}_t - \hat{\mathbf{X}}_{t-1}}) + \mathbf{W}_t,$$$
$$(10A.1)
```

$t = 1, ..., n.$ Note that $E(I_t) = 0$ and

```
$Var[\mathbf{I}_t] = Var[\mathbf{G}_t(\mathbf{X}_t - \hat{\mathbf{X}}_{t-1}}) + \mathbf{W}_t]$$
$= \mathbf{G}_t\Gamma_t^{-1}'\mathbf{G}_t' + \Gamma_{\mathbf{W}}$
```

Using the fact that $I_t$ are uncorrelated with past observations, that is, $E[I_t I_s] = 0$ for $s \leq t-1$, it follows from Equation 10A.1 that $\mathbf{X}_t - \hat{\mathbf{X}}_{t-1}$ is uncorrelated with past observations. Because of normality it follows that $\mathbf{X}_t - \hat{\mathbf{X}}_{t-1}$ is independent of past observations. Thus,

```
$Cov[\mathbf{X}_t, \mathbf{I}_t | \mathbf{Y}_1, ..., \mathbf{Y}_{t-1}] = Cov[\mathbf{X}_t - \hat{\mathbf{X}}_{t-1}}, \mathbf{I}_t | \mathbf{Y}_1, ..., \mathbf{Y}_{t-1}]$$
$$(since \hat{\mathbf{X}}_{t-1}} \text{ is a function of } \mathbf{Y}_1, ..., \mathbf{Y}_{t-1})$)$$
$=Cov[\mathbf{X}_t - \hat{\mathbf{X}}_{t-1}}, \mathbf{G}_t(\mathbf{X}_t - \hat{\mathbf{X}}_{t-1}}) + \mathbf{W}_t | \mathbf{Y}_1, ..., \mathbf{Y}_{t-1}]$$
$=Cov[\mathbf{X}_t - \hat{\mathbf{X}}_{t-1}}, \mathbf{G}_t(\mathbf{X}_t - \hat{\mathbf{X}}_{t-1}}) + \mathbf{W}_t]$$
$= \Gamma_t^{-1}'\mathbf{G}_t',,$
```

with the third equality following from the independence between $\mathbf{X}_t - \hat{\mathbf{X}}_{t-1}$ and past observations.

From the aforementioned development, the conditional distribution of

![](bbox=[0.465, 0.703, 0.532, 0.755])

is multivariate normal with mean

![](bbox=[0.465, 0.782, 0.532, 0.834])

and covariance matrix

![](bbox=[0.368, 0.876, 0.631, 0.928])