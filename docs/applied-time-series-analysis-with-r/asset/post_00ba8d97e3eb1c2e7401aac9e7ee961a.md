
248

Applied Time Series Analysis with R

forecast from $t_0 = n - k$ where $0 < k < n$. Using this technique you can assess how well your forecasts are by forecasting the $k$ values in your realization (that have already been observed). These forecasts can be made using the model fit to the entire data set or you can fit a model to the first $n - k$ data values and use this model for forecasting. This technique for assessing forecasts is shown in Example 6.8 relating to the airline forecasts shown in Figure 6.10 and in Example 6.9. You can simply compare how close your forecasts are to the actual values (very close in Figure 6.10) or you plot forecast limits and count the number of actual values that fell within the forecast limits. If forecasts are performing appropriately, for example, about 95% of actual values should fall with the 95% forecast limits.

Caution: Given a model, there are two ways in which forecasts can be made of the last $k$ values in the data: (a) using $t_0 = n - k$ and making all forecasts from this origin, or (b) updating the forecast at each step and making one-step ahead forecasts. In the second case, $x_{n-k+2}$ is forecast using $t_0 = n - k$ as the forecast origin, etc. See Problem 6.12 for a simple update formula for obtaining these type (b) forecasts, that is, one-step ahead forecasts. In our experience we have always wanted to examine the forecast performance (a) forecasts, that is, to assess how well the model performs the last $k$ values from the fixed origin $t_0 = n - k$. However, it has also been our experience that obtaining forecasts of the last $k$ values of a time series, students and practitioners often unknowingly calculate the one-step ahead forecasts before they are calculating the fixed origin forecasts. When this occurs, the reaction is usually, "Wow, these are great forecasts," until it is realized that the forecasts are actually a set of one-step ahead forecasts, which should be quite accurate. Be careful!

**Using R:** The parameter last in the tswge fore.arima.wge can be used to specify whether forecasts are to be made in the future (last=FALSE) or whether you want to forecast the observed forecasts of the last $k$ values of your existing data set from a fixed origin (last=TRUE). To avoid the type of confusion described above, do not calculate the one-step ahead forecasts. For more details concerning the use of fore.arima.wge, see Appendix 6B.

## 6.2 Forecasts Using ARIMA(p,d,q) Models

Although the forecasting results obtained in Sections 6.1 through 6.7 are for ARMA(p,q) models, which are by definition stationary, the ARIMA(p,d,q)

# Forecasting

models of Section 5.2 are also an important class of models for forecasts. Suppose that $X_t$ follows an ARIMA$(p,d,q)$ model

$$\phi(B)\lambda(B)(X_t - \mu) = \theta(B)a_t, \quad (6.35)$$

where $\phi(z)$ is a $p$-th polynomial for which all the roots of $\phi(z)$ lie outside the unit circle. In addition, $\lambda(z)$ is a $d$-th polynomial $(d > 0)$ with all roots of $\lambda(z)=0$ on the unit circle. Let $\phi^{(u)}(B)=\phi(B)\lambda(B)$, so that $\phi^{(u)}(B)$ is a $(p+d)$-th order operator with coefficients, say $\phi_0^{(u)}, \dots, \phi_{p+d}^{(u)}$. Consider Equation 6.35 as a limit of stationary models

$$\phi(B)\lambda_m(B)(X_t^m) = \theta(B)a_t,$$

where the roots of $\lambda_m(z)$ are zero outside the unit circle but the roots of $\lambda(z)=0$ (on the unit circle as $m \to \infty$), From Equation 6.21, we obtain the 'limiting' forecast

$$\hat{X}_t(\ell) = \sum_{j=1}^{p+d} \phi_j^{(u)}\hat{X}_{t-j}(\ell-j) - \sum_{j=1}^{q} \theta_j\hat{a}_{t+\ell-j} \left(1 - \sum_{j=1}^{p+d} \phi_j^{(u)}\right) \mu.$$

As in the stationary case, in practice, we use this formula

$$\hat{X}_t(\ell) = \sum_{j=1}^{p+d} \phi_j^{(u)}\hat{X}_{t-j}(\ell-j) - \sum_{j=1}^{q} \theta_j\hat{a}_{t+\ell-j} \left(1 - \sum_{j=1}^{p+d} \phi_j^{(u)}\right) \hat{X}, \quad (6.36)$$

where the $\hat{a}_t$ are given

$$\hat{a}_t = 0, t \le p+d$$
$$= X_t - \sum_{j=1}^{p+d} \phi_j^{(u)}X_{t-j} + \sum_{j=1}^{q} \theta_j\hat{a}_{t-j} \left(1 - \sum_{j=1}^{p+d} \phi_j^{(u)}\right) \hat{X}, \quad (6.37)$$

$t = p+d+1, \dots, t_0$. It also follows that $\gamma_\ell = \hat{X}_t(\ell) - X_t$ satisfies the $(p+d)$-th order difference equation $\phi^{(u)}(B)\gamma_\ell=0$. However, since $X_t$, in Equation 6.35 follows a nonstationary model, the general linear process form

$$X_t - \mu = \sum_{j=0}^{\infty} \Psi_j a_{t-j},$$

249

$$(1-B)X_t = a_t. \quad (6.41)$$

# Forecasting

A realization of length $n=50$ from this model, which is plotted in Figure 6.5, can be found in tswge set fig.6.5nf. From Equation 6.36, forecasts, $\hat{X}_t(\ell)$, are given by

$$\hat{X}_t(\ell) = \hat{X}_t(\ell-1) + (1-\ell)\bar{X}$$
$$= \hat{X}_t(\ell-1).$$

Note that the characteristic equation $\lambda(z)=1-z=0$ has a root of $+1$, then $\bar{X}$ plays no role in the forecasts. The eventual forecast function satisfies the difference equation $g_\ell = g_{\ell-1}$ for $\ell > 0$, where $g_\ell = \hat{X}_t(\ell)-\bar{X}$. The root of the characteristic Equation $1-z=0$ is $r_1=0$, so that solutions of this difference equation are given by $g_\ell=C_1(1)^\ell$ where $C_1=g_0-X$. Thus,

$$\hat{X}_t(1) = \hat{X}_t(0) = X_t,$$
$$\hat{X}_t(2) = \hat{X}_t(1) = X_t,$$

and in general

$$\hat{X}_t(\ell) = X_{t-\ell}, \quad \ell=1,2,...$$

Thus, these forecasts display no tendency to return to $\bar{X}$ as in the stationary case, but due to the random walk nature of data from this model, the best forecast of the future is the last value observed. As evidenced by the fact $Var(\hat{X}_t(\ell))$ grows without bound as $\ell$ increases. Forecasts and 95% prediction limits for a realization of length $n=50$ from the model in Equation 6.41 with $\sigma^2_t=1$ are given in Figure 6.5. For this realization, $\bar{X}=100.4$ and $\hat{X}_{50}(\ell)=\hat{X}_{50}=98.6$ for $\ell \ge 1$.

![](img/41dcbfb9af56fa48895afde322197b0b_267_0.png)

**FIGURE 6.5**
Forecasts and 95% prediction limits from the ARIMA(0,1,0) $(1-B)(X_t-100)=a_t$.

# EXAMPLE 6.4: FORECASTS FROM AN ARIMA(1,1,0) MODEL

Consider the ARIMA(1,1,0) model

$$(1 - 0.8B)(1 - B)X_t = a_t. \quad (6.42)$$

A realization of length $n = 50$ from this model is shown in Figure 6.6 (and is available in tswge data set fig6nf). Upon multiplication of the factors in Equation 6.42, we obtain

$$(1 - 1.8B + 0.8B^2)X_t = a_t,$$

so that $\phi_1^{(u)}$ and $\phi_2^{(u)} = -0.8$. From Equation 6.36, forecasts from this model are given by

$$\hat{X}_t(\ell) = 1.8\hat{X}_t(\ell-1) - 0.8\hat{X}_t(\ell-2) + (1 - 1.8 + 0.8)\bar{X}$$
$$= 1.8\hat{X}_t(\ell-1) - 0.8\hat{X}_t(\ell-2).$$

Again, because of the $(1 - B)$ factor, $\bar{X}$ plays no role in the forecasts. It follows that

$$\hat{X}_t(1) = 1.8\hat{X}_t - 0.8\hat{X}_{t-1},$$
$$\hat{X}_t(2) = 1.8\hat{X}_t(1) - 0.8\hat{X}_{t-1},$$

and, in general, for $\ell > 0$,

$$\hat{X}_t(\ell) = 1.8\hat{X}_t(\ell-1) - 0.8\hat{X}_t(\ell-2). \quad (6.43)$$

These forecasts and 95% prediction limits for $\ell = 1, ..., 20$ are shown in Figure 6.6 along with the original realization.
Although Equation 6.43 furnishes a convenient method for computing forecasts, the general behavior of the forecasts can often be observed

![](img/41dcbfb9af56fa48895afde322197b0b_268_0.png)

FIGURE 6.6
Forecasts and 95% prediction limits from the ARIMA(1,1,0) model $(1 - 0.8B)(1 - B)X_t = a_t$.

# Forecasting 253

by examining the solution of the difference equation satisfied by the forecast function. Forecasts, $\hat{X}_t(\ell) - \bar{X}$, satisfy the difference equation $g_{\ell}-1.8g_{\ell-1}+0.8g_{\ell-2} = 0$ for $\ell > 0$. Since the roots of $1-1.8z+0.8z^2=0$ are $r_1=1/0.8$ and $r_2=1$, a general solution of the difference equation is

$$g_{\ell} = C_1(0.8)^{\ell}+C_2(1)^{\ell}$$
$$= C_1(0.8)^{\ell}+C_2. \quad (6.44)$$

For the realization shown in Figure 6.6, $X_{t0}=X_{t0}=144.7$, $X_{t-1}=X_{t0}=145.6$, $X_2=149.1$, and it can be seen (see Problem 6.2) that $C_1=3.72$ and $C_2=-8.15$. Thus, as $\ell$ increases, $g_{\ell}=\hat{X}_t(\ell)-X \to C_2=-8.2$. That is, forecasts, $\hat{X}_t(\ell)$, approach the horizontal line $y=C_2+\bar{X}=140.9$. The forecasts damp exponentially to a limit, but this limit is neither $\bar{X}$ $X_{t0}$.

# EXAMPLE 6.5: FORECASTS FROM AN ARIMA(0,2,0) MODEL

Consider the ARIMA(0,2,0) model

$$(1-B)^2X_t=a_t. \quad (6.45)$$

The characteristic equation associated with this model has two roots +1, and forecasts are given by

$$\hat{X}_t(\ell)=2\hat{X}_t(\ell-1)-\hat{X}_t(\ell-2)+(1-2+1)\bar{X}$$
$$=2\hat{X}_t(\ell-1)-\hat{X}_t(\ell-2). \quad (6.46)$$

A realization of length $n=50$ from the model in Equation 6.45 is shown in Figure 6.7 (and is available in tswge data set fig6.7nf), along with forecasts obtained from Equation 6.46. For this realization, $X_{t0}=-573.9$ and $X_{t0}=-572.7$, and forecasts are

![](img/41dcbfb9af56fa48895afde322197b0b_269_0.png)

**FIGURE 6.7**
Realization of length 50 from $(1-B)^2X_t=a_t$, forecasts, and 95% limits.
