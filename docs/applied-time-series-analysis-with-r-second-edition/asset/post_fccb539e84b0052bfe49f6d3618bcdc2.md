
(tswge) generated from the AR(3) model

$X_t - 2.195X_{t-1} + 1.994X_{t-2} - 0.796X_{t-3} = a_t,$ (8.10)

which can be written as $(1 - 0.995B)(1 - 1.2B + 0.8B^2) X_t = a_t$. In Table 7.7, we show the factor table for the ML, Burg, and YW estimates of the parameters. The ML and Burg estimates are quite similar to each other and reasonably close to the true values while the YW estimates are poor. aic.wge and aic5.wge with $P = 8$ and $Q = 3$ correctly select $p = 3$ and $q = 0$. Again, the message is to avoid using YW estimates.

## B: Real Data Sets

We use aic.wge (and aic5.wge) to find ARMA(p,q) models for selected real data sets (for which we do not know the correct model, and more accurately, for which an ARMA(p,q) is only an approximating model.

- 1. In Chapter 7 we used an AR(9) model to estimate the parameters of the sunspot data in file ss08. Using aic.wge and letting $P = 12$ and $Q = 4$, the function selects an AR(9) as the best model using AIC, AICC, and BIC. The residuals and sample autocorrelations appear to be consistent with white noise. Further examination of model appropriateness will be discussed in Chapter 9.
- 2. The log (base10) lynx data in tswge file l1lynx was modeled by Tong (1977) as an AR(11) and by Campbell and Walker as a harmonic signal-plus-noise model. We used aic5.wge to select ARMA(p,q) models for the log-lynx data letting $P = 12$ and $Q = 4$. AIC selected an AR(12), ARMA(11,1), and AR(11) as the top three choices in that order while AICC picked AR(12), AR(11), and ARMA(11,1) as the top three. These models are consistent with the AR(11) model used by Tong (1977). Interestingly, BIC selected an ARMA(2,3), ARMA(3,3), and AR(2) as the top three models. In Example 7.11b we discussed the ARMA(2,3) model fit to the log-lynx data and its relationship to the ARMA(2,2) approximation of harmonic signal-plus-noise models discussed in Example 4.1.

## 8.3 Model Identification for Nonstationary ARUMA($p,d,q$) Models

In the previous section, we consider a variety of methods for identifying the orders of ARMA($p,q$) processes. However, it will often be necessary to fit a nonstationary model to a given set of data. In this section, we discuss procedures for fitting ARUMA($p,d,q$) models. Recall that an ARUMA($p,d,q$) model is specified by

$$\phi(B)\lambda(B)(X_t-\mu)=\theta(B)a_t, \qquad (8.11)$$

where

$\phi(B)$ and $\theta(B)$ are pth and qth order operators, respectively.

All the roots of $\phi(z)=0$ and $\theta(z)=0$ are outside the unit circle.

All roots of $\lambda(z)=1-\lambda_1z-\cdots-\lambda_dz^d=0$ lie on the unit circle.

To begin this discussion, we recall the Findley–Quinn theorem (Theorem 5.1) that says that if $p>0$, the extended autocorrelations, $\rho_k^*$, satisfy a lower order difference equation than $p+d$. The order of this difference equation is based on the roots on the unit circle of highest multiplicity. It was also seen in Example 3.12 that the stationary components are often “hidden” by near-nonstationary components, and, in Example 7.9c, we noted that roots near the unit circle can cause parameter estimation problems.

As a consequence of the comments in the previous paragraph, it follows that model identification in the presence of nonstationarities or near nonstationarities must be done carefully. We make the following general comments in this regard:

### General comments:

- 1. ML (and Burg/TT) estimates are better than YW (or extended YW) in the nonstationary or nearly nonstationary case. (See the estimation results shown in [Tables 7.6](#) and [7.7](#).)
- 2. Model ID techniques (such as the Box–Jenkins procedure) that are based on YW-type estimation can be misleading in the presence of nonstationary or near-nonstationary models. AIC using ML (or Burg) estimates for strictly AR models will not be as susceptible to nonstationarity or near nonstationarity.

$B$, but is not exactly equal to it. As mentioned in General Comment 4, the YW and Burg estimates will always produce a stationary AR model. Studies have also shown that ML estimates of $\phi_1$ in the AR(1) model $(1-\phi_1B)X_t=a_t$, where $\hat{\phi}_1\approx 1$ tend to have a negative bias (Kang, 1992). Thus, the fact that $|\hat{\phi}_1|<1$ is not sufficient evidence of a stationary AR(1) model, nor does the fact that all roots of $1-\hat{\phi}_1z-\cdots-\hat{\phi}_pz^p=0$ fall outside the unit circle imply that the underlying model is stationary.

### 8.3.2 Identifying Nonstationary Component(s) in a Model

General comment 5 has been demonstrated in Examples 3.14, 5.5, and 5.6 where we noticed that time series models with near unit roots have realizations whose characteristics are dominated by this nonstationary (or near-nonstationary) behavior. For example, in Example 5.5, we considered the model $(1-\alpha_1B)(1-1.2B+0.8B^2)X_t=a_t$, where $\alpha_1=0.8$, $0.95$, and $0.995$. We noticed that as $\alpha_1\to 1$ (i.e., as the associated root of the characteristic equation approached $+1$), the realizations were characterized by aimless wandering behavior with no attraction to a mean level and theoretical autocorrelations that tend to damp slowly. We note that sample autocorrelations will tend to have a similar behavior but will often damp more quickly than theoretical autocorrelations. In that example, we also noted that stationary features of the model may not be apparent because of the dominance of the near unit root. Similarly, in Example 5.6, we examined an AR(3) model $(1-0.8B)(1-1.34B+0.995B^2)X_t=a_t$ with a pair of complex roots close to the unit circle and noted that the realization and autocorrelations had a cyclic behavior and that the autocorrelations damped slowly. Additionally, the realization and autocorrelations showed very little evidence of the $1-0.8B$ factor. The behavior of the autocorrelations is consistent with the results of the Findley–Quinn theorem (Theorem 5.1).

It is common practice to make a decision concerning inclusion of a factor of $1-B$ based on examination of realizations and sample autocorrelations. Realizations with wandering or piecewise trending behavior along with slowly damping sample autocorrelations suggest a unit root of $+1$, that is, that a nonstationary factor of $1-B$ should be included in the model (e.g., see Box et al., 2008, p. 197). The classical Box–Jenkins procedure is then to stationarize the data by differencing. If the differenced data indicate continued evidence of a unit root of +1, then the Box–Jenkins procedure is to difference again, etc., until stationarity is achieved. We present an easy method for inspecting a model for unit roots or near unit roots anywhere on the unit circle. We refer to this method as overfitting, and it is based on the following result given by Tiao and Tsay (1983).

### Theorem 8.1 (Tiao–Tsay Theorem)

If $X_t$ is ARUMA$(p,d,q)$, that is, $\phi(B)\lambda(B)(X_t - \mu) = \theta(B)a_t$, then the model obtained using ordinary least squares (OLS) estimates of an AR$(d + j)$, $j > 0$ fit to the data can be factored as $\hat\phi_{d+j}(B) = \hat\phi_d(B)\hat\phi_j(B)$, where $\hat\phi_d(B)$ is a consistent estimator of $\lambda(B)$.

The implication of the Tiao–Tsay Theorem (Theorem 8.1) is that if a “high-order” AR model is fit to data from an ARUMA$(p,d,q)$ model, then the features of the model associated with the roots on the unit circle will be well estimated in the “overfit” model. Gray and Woodward (1986, 1987) demonstrated the application of Theorem 8.1 for identifying nonstationarities using Burg estimates instead of OLS estimates. The procedure recommended here is to successively overfit data with AR$(k)$ models. The factored forms of the resulting models are examined for near-nonstationary factors that tend to show in each of the overfit AR models. This procedure is illustrated in Example 8.4.

### EXAMPLE 8.4: IDENTIFYING NONSTATIONARITIES USING OVERFITTING

- 1. Figure 8.3a shows a realization of length $n = 200$ (previously shown in Figure 5.3c and available as data set `fig5.3c` in tswge) from the near-nonstationary AR(3) model

$(1 - 0.995B)(1 - 1.2B + 0.8B^2)X_t = (1 - 2.195B + 1.994B^2 - 0.796B^3)X_t = a_t,$ (8.12)
