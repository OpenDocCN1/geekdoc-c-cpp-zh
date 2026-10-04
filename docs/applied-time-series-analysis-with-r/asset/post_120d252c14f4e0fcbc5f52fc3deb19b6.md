
## 268 Applied Time Series Analysis with R

b0 = 0, calculated x10 = x + 10 between the two call statements,
let x10 be the realization on which to base the forecasts.
Note that you need to specify freq in the forecast call statement. In a real data situation in which you believe the realization may be a cosine signal +noise model, you will typically obtain a good estimate of freq using a spectral density estimate or fitting a high order AR model and checking the factor for the dominant frequency. Note also that while gen.sigplusnoise.wge can generate a realization with one linear and two cosine components, the function fore.sigplusnoise.wge provides forecasts only in the simple linear or single cosine cases.

## Utility Routines

+ psi.weights.wge(phi,theta,lag,max) calculates the ψ-weights for an ARMA (or ARIMA) model.
phi = the vector of AR coefficients (un-factored form) for a stationary model along with any (1 - B), seasonal, and λ(B) factors (multiplied together using mult.wge. (default = 0))
theta = MA coefficients of the ARMA model in un-factored form.
default = 0)
lagmax = maximum lag at which the psi weights will be calculated. The function calculates psi weights psi(1), psi(2),..., psi(lag,max).
Note that psi(0) = 1. (default = 0)

+ Examples:
psi.weights.wge(phi = c(1.2,-.6),theta = .5,lag.max = 2) returns the ψ-weights calculated in Example 6.2, that is, ψ1=0.7 and ψ2=0.25. Recall that ψ0=1
to get the first 5 psi weights for the ARIMA(1,1,0) model in Equation 6.42 use the following code:
prod = mult.wge(facl = .8,fac2 = 1)
psi.weights.wge(phi = prod$model.coef,lag.max = 5)
psi.weights.wge (described in Appendix 3B)

## EXERCISES
Applied Problems

+ A realization of length n = 10 from the ARMA(4, 2) model

```
(X_t - μ) + 1.1(X_{t-1} - μ) + 1.78(X_{t-2} - μ) + 0.88(X_{t-3} - μ) + 0.64(X_{t-4} - μ)
a = a_t - 0.2a_{t-1} + 0.9a_{t-2}
```

where μ = 40 is given in the following table.

| t | X_t | t | X_t |
|---|---|---|---|
| 1 | 40.0 | 6 | 48.7 |
| 2 | 30.5 | 7 | 39.2 |
| 3 | 49.8 | 8 | 31.7 |
| 4 | 38.3 | 9 | 46.1 |
| 5 | 29.3 | 10 | 42.4 |

+ a. By hand (calculator)
  i. Obtain forecasts \hat{X}_{10}(ℓ), ℓ = 1, 2, 3, 4 using Equation 6.24
  ii. Find 95% prediction intervals for the forecasts in (a)
  b. Repeat (i) and (ii) using a statistical forecasting package

+ 6.2 For the realization in Figure 6.6, X_{60} = X_{50} = 144.67 and X_{60-1} = X_{40} = 145.6 while showing that the general solution of the forecast function in Equation 6.44 constants C_1 = 3.72 and C_2 = -8.15. Find \hat{X}_t(ℓ), ℓ = 1, ..., 3 using this general solution. Also, find these forecasts using Equation 6.43.

+ 6.3 Using gen.arma.wge (after calling mult.wge) generate a realization of length n = 100 from the ARMA(3,1) model

```
$(1-0.8B)(1-B+0.9B^2)(X_t-50) = (1+0.5B)a_t$.
```

Do the following fore.arma.wge:

+ a. Forecast the next 20 steps beyond the end of the series showing 95% probability limits using the ARMA(3,1) model given above.
b. Plot the forecasts and describe their behavior.
c. Forecast the last 10 values of the series (using t_0 = 90 as the forecast-origin) and discuss the behavior of the forecasts and how well the forecasts perform.
d. Redo part (c) this time showing the 95% probability limits. How many of the actual last 10 values stay within these limits?

+ 6.4 Generate a realization of length n=100 from the ARUMA(1,5,0) model

```
$(1-B)(1-B^4)(1+0.5B)(X_t-50) = a_t$.
```

Do the following:

+ a. Forecast the next 10 steps beyond the end of the series.
b. Forecast the last 10 values of the series (using t_0 = 90 as the forecast-origin) and discuss the behavior of the forecasts and how well the forecasts perform.

## Forecasting

c. Redo part (b) this time showing the 95% probability limits. How many of the actual last 10 values stay within these limits?

6.5 The log airline data are given the tswge data set airlog. Figure 6.9 shows forecasts of the last 36 values of the log-airline data using the ARUMA(12,13,0) model (1–B) (1–B²)φ(B)(X_t-μ) = a_t, φ(B) is the stationary 12th-order operator given in Equation 6.54. Using the same model, and plot forecasts, such as those in Figure 6.9 for the last 12, 24, 36, and 48 values. Discuss the features of the associated forecasts.

6.6 Forecast 3 years (3 months) beyond the end of the airlog data (a) using the ARUMA(12,13,0) model used in Problem 6.5, and by using the ARUMA(13,12,0) model in Equation 6.55 obtained by Parzen. Compare and contrast the associated forecasts. What features of the two models accounts for the differing behaviors of the two eventual forecast functions?

6.7 Models A and B follow that the models are given in Problem 3.12 as models that have been proposed for the sunspot data from 1749 to 1924 found in sunspot.classic. Model C is the non-stationary model analogous to (b) obtained by moving the plex roots with the dominant 10–11 year cycle to the unit cycle.

A. $(1.42B + 0.73B^2)(X_t - 44.78) = a_t$

B. $(1.23B + 0.47B^2 + 0.14B - 0.16B^4 + 0.14B^5 - 0.07B^6 + 0.13B^7 - 0.21B^9)(X_t - 44.78) = a_t$

C. $(1.664B + B^2)(1 + 0.37B + 0.11B^2 - 0.033B^3 - 0.29B^4 - 0.31B^5 - 0.27B^6)(X_t - 44.78) = a_t$

+ i. For each of these forecasts and determine, on the basis of the forecasts, which model appears to be the better model for the sunspot data?

+ ii. What features in the two models account for the rather substantial differences in the forecasts?

+ iii. On the basis of this comparison, which model do you prefer? Which seems to be the poorest model?

+ One method for assessing the quality of a model is to examine how well the model fits the last several data values in the data set. Using the three models

+ i. Compute and plot the forecasts for the last 50 data values using year 1874 as the forecast origin. That is, plot the realization along with the forecasts of the last 50 values.

+ ii. Discuss the quality of the forecasts. That is, how close were the forecasts to the actual values, and how well did the forecasts stay in phase with the actual cycles?

+ iii. On the basis of this comparison, which model do you prefer? Which seems to be the poorest model?

6.8 a. Generate a realization of length n=50 from the signal-plus-noise model X_i = 5+0.3+Z_i, where Z_i = (1+0.2B+0.6B^2)a_i and σ_Z^2=0.5. Plot the realization, forecasts, and forecast limits for the next 20 time periods.

b. Generate a realization of length n=100 from the signal-plus-noise model X_i=50+5cos(2π f_0 t+2.5)+Z_i, where f_0=0.1 and Z_i=(1+0.7B)a_i and σ_Z^2=1. Plot the realization, forecasts, and forecast limits for the next 20 time periods.

## Theoretical Problems

6.9 Prove Theorem 6.3, show that if X_t is a stationary process with autocovariance γ_0 then the quantities a_1, …, a_n in the definition of \hat{X}_t(ℓ) in Equation 6.2 are the solutions to the system

![](img/41dcbfb9af56fa48895afde322197b0b_287_0.png)

6.10 Verify the following properties associated with the \hat{X}_t(ℓ):

+ a. the one-step forecast errors are the a_s, that is, e_t(1)=a_{t+1}.
b. the forecast errors have expectation zero, that is, E[e_t(ℓ)]=0, ℓ ≥ 1.
c. the variance of the forecast errors is given by Var[e_t(ℓ)]=σ_a^2σ_w^2.
d. covariance between forecast errors

Cov[e_t(ℓ), e_{t-j}(ℓ)]=0, j ≥ ℓ.

Thus, whenever j=0, 1, …, ℓ-1, the forecast errors may be correlated.
e. e_t(ℓ_1) and e_t(ℓ_2) are correlated. Specifically, find an expression for Cov[e_t(ℓ_1), e_t(ℓ_2)] where ℓ_2 > ℓ_1.
f. the "best MSE forecast" for ∑_{k=1}^m α_k X_{t+k} from origin t_0 is given by ∑_{k=1}^m α_k \hat{X}_t(k).

## 271

6.11 Show that forecasts, \hat{X}_t(ℓ), from the model $(1 - B)^2$ $(X_t - μ) = a_t$
all lie on a straight line that passes through X_{t_0-1} and X_{t_0}.

6.12 Let \hat{X}_{t_0}(ℓ) denote the best forecast of X_{t_0+ℓ} given data to time t_0.
Show if \hat{X}_{t_0+1} is observed, then the best forecast of X_{t_0+ℓ'} that
is, \hat{X}_{t_0+1'} (ℓ - 1) is given by the updating formula

```
$\hat{X}_{t_0+1}(\ell - 1) = \hat{X}_{t_0}(\ell) + \psi_{\ell-1}(X_{t_0+1} - \hat{X}_{t_0}(1))$
```

where ψ denotes the j/th ψ-weight from the ARMA model from
which the forecasts are obtained.

6.13 Let $(1 +7B)(X_t - μ) = a_t$ and let x_t, t=1..100 be a realization from
this model with x_{100}=57.5, x_{99}=44.2, and \bar{x}=49.4. Find the equa-
t of the eventual forecast function.
