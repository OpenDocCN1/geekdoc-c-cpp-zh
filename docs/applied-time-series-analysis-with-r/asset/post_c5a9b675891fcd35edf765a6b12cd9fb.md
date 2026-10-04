
# 150 Applied Time Series Analysis with R

(a)

![](img/41dcbfb9af56fa48895afde322197b0b_166_0.png)

(b)

![](img/41dcbfb9af56fa48895afde322197b0b_166_1.png)

(c)

![](img/41dcbfb9af56fa48895afde322197b0b_166_2.png)

(d)

![](img/41dcbfb9af56fa48895afde322197b0b_166_3.png)

FIGURE 3.27
Sunspot data from 1749–2008 and the first three additive components associated with the AR(9) fit in Example 3.15 whose factor table is designed in Table 3.5. (a) Realization. (b) Component 1: f=0.09. (c) Component 2: f=0. (d) Component 3: f=0.19.

due to the characteristic equation on the unit circle. One modification of ARMA(p,q) is designed to take into account seasonal behavior in data. For example, quarterly data (e.g., breaking the year into 4 month groups) will have seasonal characteristics implying that there is a natural correlation structure between, $X_i$ and $X_{i-4}$, is, between the current quarter and the quarter last year. In this case, it makes sense to include factors in the model as $\phi(B^4)=1-\phi_1B^4-\phi_2B^8-\dots-\phi_4B^{16}$, that take into account this four-quarter year relationship. For example, we might have that $\phi(B^4)=1-0.9B^4$ or $\phi(B^4)=1-B^4+0.8B^4$, is, the models $X_i=X_{i-4}+a_i$

## ARMA Time Series Models

and $X_t = X_{t-4} - 0.8X_{t-8} + a_t$, which specify that this quarter's performance is a linear combination of the same quarter in previous years plus noise. In general, we use $s$ to denote the 'season' (i.e., for monthly data, $s=12$ and for quarterly data $s=4$). A (purely) stationary seasonal model is given by

$\Phi(B^s)X_t = \Theta(B^s)a_t,$

where all the roots of

$1-\Phi_1z^s-\Phi_2z^{2s}-\dots-\Phi_{P_s}z^{P_ss}=,$

and

$1-\Theta_1z^s-\Theta_2z^{2s}-\dots-\Theta_{Q_s}z^{Q_ss}=,$

outside the unit circle.

**EXAMPLE 3.22: A PURELY SEASONAL STATIONARY MODEL**
In this example, we consider the model

$(1-0.8B^4)X_t = a_t,$

in more detail. Note that Equation 3.125 is an AR(4) model with the coefficients $\phi_2=\phi_3=0$ and $\phi_4=0$. However, it is also a seasonal model with $s=4$ and $P_s=1$, that is, as a seasonal model it is first order. In order to examine the nature of the model in Equation 3.125, we generate a realization of $n=20$, which we interpret as quarterly data for a 5-year period. The realization with the autocorrelations and AR-spectral density is shown in Figure 3.28. In Figure 3.28a, the vertical lines show the realization into years, and it can be seen that there is a strong correlation between a particular quarter and the next year. For example, quarters 1, 3, and 4 are relatively high in each year quarter 2 shows a dip. The autocorrelations vividly illustrate the sense in which the model describes seasonal (in this case quarterly) behavior. In Figure 3.28b, it is seen that the only nonzero autocorrelations are at lags that are multiples of four. For example, there is no correlation between adjacent months. The first-order seasonal nature of the model since illustrates that autocorrelations at lags that are multiples of four decay exponentially. The spectral density in Figure 3.28c shows peaks at frequencies. This behavior is also illustrated in the table in Table 3.8 it can also be seen that Equation 3.125 is a stationary model since all the roots of the characteristic equation are outside the unit circle.

## Applied Time Series Analysis with R

![](img/41dcbfb9af56fa48895afde322197b0b_168_0.png)

FIGURE 3.28

(a) Realization, (b) autocorrelations, and (c) spectral densities for the seasonal model (1 - 0.8B^4) $X_t = a_t$.

# TABLE 3.8
Factor Table for Seasonal Model $X_t = a_t$

| AR Factor | Roots ($r_j$) | $|r_j|$ | $f_{oj}$ |
|---|---|---|---|
| 1 - 0.95B | 1.06 | 0.95 | 0.00 |
| 1 + 0.95B | -1.06 | 0.95 | 0.50 |
| 1 + 0.89B^2 | ±1.06 | 0.95 | 0.25 |

**Using R:** A realization from the seasonal model in Equation 3.125, true auto-correlations, and spectral densities can be obtained using the `tswge` function `plotts.true.wge` discussed previously. In this case you would specify the model as an AR(4) with coefficients 0, 0, 0, and 0. Using these AR(4) coefficients you can obtain a factor table for this seasonal model using `factort.wge`.

One feature of the model in Equation 3.125 that makes it less than ideal for practical situations is that there is very likely autocorrelation between adjacent or nearly adjacent quarters in the quarterly behavior modeled by Equation 3.125. Consequently, the purely seasonal model in

## ARMA Time Series Models 153

Equation 3.124 requires modification to allow for this type of behavior. The multiplicative seasonal ARMA model

$\Phi(B^s)\phi(B)X_t = \Theta(B^s)\theta(B)a_t, \quad (3.126)$

where the roots of $\phi(z) = 1 - \phi_1 z - \dots - \phi_p z^p = 0$ and $\theta(z) = 1 - \theta_1 z - \dots - \theta_q z^q = 0$ all lie outside the unit circle, is widely used for this purpose. The model in Equation 3.126 is denoted by ARMA$(p,q) \times (P_s,Q_s)_s$.

# EXAMPLE 3.23: A MULTIPLATIVE SEASONAL STATIONARY ARMA(1,0) \times (1,0)_s MODEL

As an example of a multiplicative seasonal ARMA model, we consider the model

$(1-0.7B)(1-0.8B^4)X_t = a_t, \quad (3.127)$

which is a modification of the seasonal model in Equation 3.125. A realization of length $n = 20$ from this model along with the true autocorrelations and spectral density is shown in Figure 3.29. Figure 3.29a shows

![](img/41dcbfb9af56fa48895afde322197b0b_169_0.png)

**FIGURE 3.29**
a) Realization, (b) autocorrelations, and (c) spectral densities for the multiplicative seasonal model $(1-0.7B)(1-0.8B^4)X_t = a_t$.

## Applied Time Series Analysis with R

that the factor 1 – 0.7B induces within-year correlation, that is, all quarters in year one have lower values than the corresponding quarters in year two. This within-year correlation is also apparent in the autocorrelations of autocorrelations with relatively higher correlations at lags that are multiples of four. The factor 3.29b where there is a general damping behavior of autocorrelations in Figure 3.17 (not shown) is the same as shown in Table 3.8 for an additional factor, 1 – 0.7B, associated with a system frequency at f=0. As a result, the spectral density in Figure 3.29c has a similar behavior to that of Figure 3.28c except that the peak at f=0 is higher.

We return to the multipplicative seasonal models in Chapter 5 where we discuss nonstationary models. In fact, the most common use of the seasonal model is in which the seasonal components of the model have roots on the unit circle.

# EXAMPLE 3.24: METRIC TONS OF PORTLAND CEMENT USAGE

In Figure 3.30a (data set in `twage`) we show the quarterly usage of metric tons (in thousands) of Portland cement used according to the Australian Bureau of Statistics from the first quarter of 1973 through the fourth quarter of 1993. Figure 3.30b and c show the same autocorrelations and the Parzen window spectral density estimator. The quarterly

![](img/41dcbfb9af56fa48895afde322197b0b_170_0.png)

FIGURE 3.30
a) Realization, (b) sample autocorrelations, and (c) Parzen spectral density estimator for the Australian cement data.

behavior is visible in the data, for example, low production in the first quarter of each year and higher production in the other three quarters. Also, the seasonal behavior is noticeable in the sample autocorrelations and spectral density. Note the similarities between Figure 3.29b and c Figure 3.27b and c.

# 3.6 Generating Realizations from ARMA(p,q) Processes

The study of time series analysis using ARMA(p,q) models often involves the simulation of finite realizations, $[x_t, t=1,..,n]$ from known ARMA models to provide information concerning the characteristics of typical realizations, autocorrelation functions, and spectral densities. We have used this technique often in this chapter. These realizations are also useful in Monte Carlo studies, bootstrap resampling. For these reasons, we include a brief discussion concerning the generation of ARMA(p,q) time series realizations.

# 3.6.1 MA(q) Model

Generating realizations from the MA(q) process in Equation 3.1 is relatively simple. For known $\theta_k, k=1,..$ and $\sigma_a^2$, realization values are obtained from

$x_1 = \mu + a_1 - \theta_1 a_0 - \dots - \theta_q a_{1-q}$
$x_2 = \mu + a_2 - \theta_1 a_1 - \dots - \theta_q a_{2-q} \quad (3.128)$

where $a_i$ values are generated using a random number generator for generating uncorrelated deviates with mean zero and variance $\sigma_a^2$. From Equation 3.128, it is clear that the generation is initiated by obtaining the $q$ uncorrelated starting values $a_q,a_{q-1},..a_1$.

# 3.6.2 AR(2) Model

As an example of the complications that arise in computing appropriate starting values for simulating realizations from ARMA(p,q) models with $p>0$, we consider the AR(2) model with $\mu=0$ and $\sigma_\epsilon^2$. For the AR(2) model, the observations are generated from

$x_1 = \mu(1 - \phi_1 - \phi_2) + \phi_1 x_0 + \phi_2 x_{-1} + a_1$
$x_2 = \mu(1 - \phi_1 - \phi_2) + \phi_1 x_1 + \phi_2 x_0 + a_2 \quad (3.129)$
