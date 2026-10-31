+   example$ll is a vector containing the lower limits  
+   example$ul is a vector containing the upper limits  
+   example$resid is a vector containing the residuals  
+   example$wnv is the white noise variance estimate  
+   example$se is a vector containing the standard error (SE) for each forecast  
+   example$psi is a vector containing the psi weights

2. Estimating the model parameters and using them as the model from which to forecast

```
data(fig6.2nf)
exii = est.arima.wge(fig6.2nf,p = 2,q = 1)
example    =    fore.aruma.wge(fig6.2nf,phi    =    exii$phi,    theta    =
exii$theta,n.ahead = 20)
```

b.

```
fore.aruma.wge(x,phi,theta,d,s,lambda,n.ahead,lastn,plot,limits
```

This function forecasts n.ahead steps ahead using the Box–Jenkins forecasting approach for nonstationary ARUMA models that may have stationary ARMA components, factors such as (1 − B)^d, seasonal, and/or other nonstationary factors. The forecasts and forecast limits can optionally be plotted.

+   x = realization  
+   phi is a vector of AR coefficients (default = 0)  
+   theta is a vector of MA coefficients (default = 0)  
+   d is the order of the difference operator, (1 − B)^d, in the model (default = 0)  
+   s is the seasonal order (default = 0)  
+   lambda is a vector containing the coefficients of the nonstationary not included in the difference or seasonal operators. (default = 0)  
+   n.ahead = the number of steps ahead you want to forecast (default = 2)  
+   lastn = logical variable. If lastn = FALSE (default) then the forecasts are for x(n + 1), x(n + 2), ..., x(n + n.ahead) where n is the length of the realization. If lastn = TRUE, then the program forecasts the last n.ahead values in the realization.  
+   plot = logical variable. If plot = TRUE (default) then the forecasts will be plotted along with the realization. If plot = FALSE then no