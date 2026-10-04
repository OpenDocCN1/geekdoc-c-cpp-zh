# 266 Applied Time Series Analysis with R

lastn = logical variable. If lastn = FALSE (default) then the forecasts are for x(H+1), x(H+2), ..., x(n.ahead) where n is the length of the realization. If lastn = TRUE, then the program forecasts the last n.ahead values in the realization.

plot = logical variable. If plot = TRUE (default) then the forecasts will be plotted along the realization. If plot = FALSE then no plots are output. (default = TRUE)

limits = logical variable. If limits = TRUE then the 95% forecast limits will be plotted along the forecasts.

NOTE: As was the case with the fore.arma.wge function, you can use either a "known" or a fitted model. The following examples uses the "true" ARIMA(1,1,0) model in Equation 6.42 in Example 6.4.

Example:
data(fig6.6nf)
example = fore.arma.wge(fig6.6nf,phi=.8,d=1,n.ahead = 20)
This code produces the plot in Figure 6.6 along with the following output:

+   - example$f is a vector containing the forecasts
- example$l is a vector containing the lower limits
- example$ul is a vector containing the upper limits
- example$resid is a vector containing the residuals
- example$wnv is the white noise variance estimate
- example$se is a vector containing the SE for each forecast
- example$psi is a vector containing the psi weights

c.sigplusnoise.wge(x, linear, freq, max, p, n.ahead, lastn, plot,limits)

This function forecasts n.ahead steps ahead a signal + noise model of the form

```
X_t = b_0 + b_1t + Z_t,
or
X_t = A_0 + A_1 cos(2πf_0t + A_2) + Z_t
```

Note that signals are restricted to linear or (single) sinusoidal signals. As with other forecasts in this chapter we assume that the signal and the (autoregressive) noise model are known when assessing the forecast errors. The forecasts and forecast limits can optionally be