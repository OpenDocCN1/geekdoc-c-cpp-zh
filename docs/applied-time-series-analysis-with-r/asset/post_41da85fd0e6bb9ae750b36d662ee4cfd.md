
# Model Building 387

```
$Y_i = (1-\phi_1 B)X_i$
$= (1-\phi_1 B)(a+bt+Z_i)$
$= a(1-\phi_1)+b(1-\phi_1 B)t+(1-\phi_1 B)Z_t$
$= c+bt_i+a_i, \quad (9.13)$
```

where Equation 9.13 is a regression equation with the same slope coefficient, $b$, as in Equation 9.11 with a new independent variable $t_{\phi_1}=(1-\phi_1 B)t=t-(t-1)$ and uncorrelated residuals. In, however, $\phi_1, a,$ and $b$ will not be known and must be estimated from the data. Cochrane and Orcutt (1949) suggested fitting a regression line to the data using least-squares estimates and fitting an AR(1) model to the data $\hat{Z}_i=X_i-\hat{a}-\hat{b}$, the estimated coefficient, $\hat{Y}_i=X_i-\phi_1 X_{i,t}=2,...,n$. Thus, the resulting series, $\hat{Y}_i$, is of length $n-1$ and satisfies

```
$\hat{Y}_i=(1-\phi_1 B)\hat{X}_i$
$=a(1-\phi_1)+b(1-\phi_1 B)t+(1-\phi_1 B)Z_t+g_t, \quad (9.14)$
```

where $t_{\hat{\phi}_1}}=t-\hat{t}(t-1)$. Noting that $Z=(1-\phi_1 B)^{-1}a_i$, we see that $g_t=(1-\phi_1 B)(1-\phi_1 B)^{-1}a_i$, which is not white noise but must be almost. The Cochrane–Orcutt (CO) procedure is used to test the null hypothesis $H_0: b=0$ in Equation 9.14 where the independent variable is $t_{\hat{\phi}_1}$ using standard least-squares methods. Then, the CO test involves the test statistic

```
$t_{CO}=\frac{\hat{b}_{CO}}{SE(\hat{b}_{CO})}, \quad (9.15)$
```

$\hat{b}_{CO}$ is the usual least-squares estimate of the slope $b$ in Equation 9.14 and $\hat{SE}(t_{CO})$ is its usual standard error. Then, $H_0: b=0$ is tested assuming the statistic $t_{CO}$ in Equation 9.15 has a Student’s $t$ distribution. Beach and MacKinnon (1978) developed a ML approach that also involves calculation of a test statistic that has a $t$ distribution under the null. While the CO and ML approaches assume that the residuals are AR(1), extensions to residuals that are AR($\rho$) or ARMA($\rho,q$). Another test developed by Bloomfield and Nychka (1992) (BN) involves a frequency-domain expression for the standard error of $\hat{b}$.

Although this, ML, and BN seem reasonable, it has been shown that they tend to have significance levels higher than their nominal levels

# 388 Applied Time Series Analysis with R

(see Park and Mitchell, 1980; Woodward and Gray, 1993; Woodward et al., 1997. While these tests have the desired asymptotic properties, Woodward et al. (1997) demonstrate that this asymptotic behavior is often not approached by realizations of moderate length (e.g., $n=100$) in the presence of moderate correlation structure in the data. For example, Woodward et al. (1997) show when $Z_i$ is an AR(1) with $\phi_1=0.9$ or $b=0$, realizations of length $n=1000$ or more may be required in order for the CO, ML, or BN tests to have observed significance levels close to the nominal levels. The simulations performed by Woodward et al. (1997) show that if the model is $(1-0.9B)X_t=\epsilon_t$, a stationary model with no deterministic trend), then the CO method, detects a significant trend at the nominal 5% level of significance (incorrectly) in 20% of realizations of length $n=100$ while Beach and MacKinnon’s (1978) ML method detects a trend in 17% of these realizations. Realizations of length $n=1000$, the CO and ML procedures detect significant trends in about 8% of the realizations, which are still highly.

## 9.3.2 A Bootstrapping Approach

Woodward et al. (1997) suggested a bootstrap method to estimate the accuracy of the test statistics obtained by the CO and MLE procedures. In the following, we will consider the application of the bootstrap to $t_{CO}$ in Equation 9.15. Here, the $t_{CO}$ statistic is calculated as described previously on the original (observed) data. Set to simulate realizations of $H_0$ an AR model fit to the observed data. This procedure assumes $H_0$ that any trending behavior in the series is due to the correlation structure alone. Then, K realizations are generated from the AR model fit to the original data. Woodward et al. (1997) used a parametric bootstrap procedure that assumes normal errors and generates $a_t$ in the simulated procedures as random normals. If normality of the errors is questioned, a non-parametric bootstrap could be used in which the original series, $\hat{a}_t, t=1,...,K$, from the original AR(p) fit to the data are resampled with replacement for use in the terms in the simulated procedures. For a two-sided test, $H_0: b=0$ is rejected at significance level $\alpha$ if $t_{CO} > t_{\alpha/2}$ or $t_{CO} < -t_{\alpha/2}$, where $t_{\beta}^{(b)}$ is the $\beta$th empirical quantile of $\{t_{CO}^{(b)}\}_{b=1}^K$ with standard adjustments for one-sided tests.

## 9.3.3 Other Methods for Trend Testing

Other researchers have developed tests for slope in the presence of correlated residuals for the observed significance level is closer to the nominal levels. Jenkins and Watts (1997) and Vogelsang (1998) propose tests that are appropriate whether or not the model for $Z_i$ has unit roots, while Sun and Pantula (1999) describe several alternative methods. Brillinger

# Model Building

proposed a test for detecting a monotonic trend, that is, for the case in which s is a monotonic function, and Woodward and Gray (1993) demonstrated that this test has inflated significance levels (similar to CO and ML) for moderate realization lengths. Sanders (2009) investigated bootstrap tests for monotonic and other nonparametric trends.

Needless to say, the problem of detecting a trend in the presence of related data is a very challenging one. It is worth making special note of the fact that if a significant trend is detected and a nonzero slope coefficient is included in the model, then the implicit decision is that the trend behavior is predicted to continue. Such a model should be used with caution especially if more than simply short-term forecasts are needed. See Woodward (2013).

## 9.4 Checking Realization Characteristics

Even though a model is selected by a particular model identification procedure or has residuals that seem appropriate and the model makes sense physically, it may in fact not be an appropriate model for forecasting, spectral estimation, etc. One useful diagnostic concerning the appropriateness of a model fit to a set of time series data is to determine whether generated from the model have characteristics consistent with those of the observed data. For example, do realizations from the model have spectral densities, sample autocorrelations, and so forth, similar to those of the original data set?

> EXAMPLE 9.3: CHECKING REALIZATION CHARACTERISTICS FOR MODELS FIT TO THE SUNSET DATA

We consider the annual number sunsets shown in Figure 1.23a that, for convenience, plotted in the horizontal axis is the sequence number (1–26). The 10–11 year cycle previously mentioned along with a tendency for there more variability in the heights of the cycles than in the troughs is evident in Figure 9.7a. The sample autocorrelations in Figure 9.7b have a damped sinusoidal pattern with a period of 10–11 years. The smoothed spectral density estimate based on a Parzen window with M = 32 is shown in Figure 9.7c, as we expected, we see a peak at f = 0.1 associated with the 10–11 year cycle. We also see a peak at f = 0 associated with the wandering and piecewise trending behavior of the cycle crest.

A subset of these data (called Series C) was considered by Box et al. (2008), and one of the models they fit to the data set was AR(2). This model was suggested by the fact that the partial autocorrelations are quite small the first two partial autocorrelations, which are about 0.8 and –0.7. This same pattern of partial autocorrelations can be found

# Applied Time Series Analysis with R

![](img/41dcbfb9af56fa48895afde322197b0b_406_0.png)

![](img/41dcbfb9af56fa48895afde322197b0b_406_1.png)

FIGURE 9.7
(a) Sunspot data, (b) sample autocorrelations, and (c) Parzen spectral density estimator using $M = 32$.

using the updated series in Figure 9.7a. Thus, we fit an AR(2) model to the sunspot data in Figure 9.7a with ML estimates and obtain the model

> $$1 - 1.385B + 0.69B^2(X_t - 52.2) = a_t,$

with $\sigma_a^2 = 293$. Applying AIC with $P = 10$ and $Q = 3$, we select the AR(9) model

> $$1 - 1.158B + 0.392B^2 + 0.185B^3 - 0.155B^4 + 0.10B^5 - 0.021B^6 - 0.029B^7$
+0.066B^8 - 0.024B^9(X_t - 52.2) = a_t,$

> $$\sigma_\theta^2 = 238.$

When comparing models in Equations 9.16 and 9.17, we first note that Equation 9.16 is a much more parsimonious model and should be considered to preferable if there are no substantive advantages for using the higher order model. In Figures 9.8 and 9.9, we show four realizations from models in Equations 9.16 and 9.17, respectively. Clearly, neither model does a good job of generating realizations that have more variability in the peaks of the cycles than the troughs, and the realizations
