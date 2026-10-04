forecasts while the forecasts based on the 2-factor GARMA model perform better in the long term.

NOTE: The model in Equation 11.33 is not a 2-factor GARMA model as we have defined in this chapter since it also contains the nonstationary factor $(1 - B^2)$. That is, by an extension of our previous notation, this could be called a 2-factor GARIMA or GARUMA model. However, $Y_t = (1-B)^2(X_t - ar{X})$ does satisfy a 2-factor GARMA model and our previous conditions for stationarity and estimation then are applicable.

# Appendix 11A: R Commands

# 11A.1 Basic Computation and Plot Routines for Chapter 11

+   a. `true.farma.aut.wge(d,phi,theta,lag.max,vara,trunc)` calculates the true autocorrelations and autocariances associated with a fixed GARMA model of the form in Equation 11.5.

d is the fractional difference parameter Equation 11.6
phi is a vector of AR parameters (using signs as in this text)
theta is a vector of MA parameters (using signs as in text)
lag.max is the maximum lag at which the autocorrelations and autocovariances will be calculated (default=25)
vara is the white noise variance (default=1)

trunc is the truncation point in the infinite series expansion of the FARMA autocovariance (default=1000). See proof of Theorem 2.4 in Hosking (1981).

plot is a logical variable: TRUE (default) = plot autocorrelations,
FALSE = no plot

The function outputs

+   acf (the true autocorrelations from lags 0 to lag.max)
acv (the true autocovariances from lags 0 to lag.max)

NOTES:

+   1. You may want to use the utility function mult.wge if you know the factors of the AR or MA model instead of the coefficients.
2. max(p,q+1) $\le 25