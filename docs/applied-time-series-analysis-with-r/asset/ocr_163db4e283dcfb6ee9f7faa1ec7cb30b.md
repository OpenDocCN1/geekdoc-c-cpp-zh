# 268 Applied Time Series Analysis with R

b0 = 0, calculated x10 = x + 10 between the two call statements,
let x10 be the realization on which to base the forecasts.
Note that you need to specify freq in the forecast call statement. In a real data situation in which you believe the realization may be a cosine signal +noise model, you will typically obtain a good estimate of freq using a spectral density estimate or fitting a high order AR model and checking the factor for the dominant frequency. Note also that while gen.sigplusnoise.wge can generate a realization with one linear and two cosine components, the function fore.sigplusnoise.wge provides forecasts only in the simple linear or single cosine cases.

# Utility Routines

+   psi.weights.wge(phi,theta,lag,max) calculates the ψ-weights for an ARMA (or ARIMA) model.
phi = the vector of AR coefficients (un-factored form) for a stationary model along with any (1 - B), seasonal, and λ(B) factors (multiplied together using mult.wge. (default = 0))
theta = MA coefficients of the ARMA model in un-factored form.
default = 0)
lagmax = maximum lag at which the psi weights will be calculated. The function calculates psi weights psi(1), psi(2),..., psi(lag,max).
Note that psi(0) = 1. (default = 0)

+   Examples:
psi.weights.wge(phi = c(1.2,-.6),theta = .5,lag.max = 2) returns the ψ-weights calculated in Example 6.2, that is, ψ1=0.7 and ψ2=0.25. Recall that ψ0=1
to get the first 5 psi weights for the ARIMA(1,1,0) model in Equation 6.42 use the following code:
prod = mult.wge(facl = .8,fac2 = 1)
psi.weights.wge(phi = prod$model.coef,lag.max = 5)
psi.weights.wge (described in Appendix 3B)

# EXERCISES
Applied Problems

+   A realization of length n = 10 from the ARMA(4, 2) model

```
(X_t - μ) + 1.1(X_{t-1} - μ) + 1.78(X_{t-2} - μ) + 0.88(X_{t-3} - μ) + 0.64(X_{t-4} - μ)
a = a_t - 0.2a_{t-1} + 0.9a_{t-2}
```