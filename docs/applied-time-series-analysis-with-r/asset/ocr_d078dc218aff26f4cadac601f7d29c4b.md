# Forecasting

Example:

+   1. Using a known model
```
data(fig6.2nf)\example=fore.arma.wge(fig6.2nf,phi=c(1.2,-6),theta=.5,n.ahead=20)
```nThe function produces the plot in Figure 6.4 along with the following output:
example$f is a vector containing the forecasts
example$ll is a vector containing the lower limits
example$ul is a vector containing the upper limits
example$resid is a vector containing the residuals
example$wnv is the white noise variance estimate
example$se is a vector containing the standard error (SE) for each forecast
example$psi is a vector containing the psi weights

+   2. Estimating the model parameters and using them as the model from which to forecast
```
data(fig6.2nf)
exii=est.arma.wge(fig6.2nf,p=2,q=1)
example=fore.arma.wge(fig6.2nf,phi=exii$phi,theta=exii$theta,n.ahead=20)
```

b. aruma.wge(x,phi,theta,d,lambda,n.ahead,lastn,plot,limits) This function n.ahead steps ahead using the Box-Jenkins forecasting approach for nonstationary ARIMA models that have stationary ARMA components, factors such as(I-B)^d, seasonal, and/or nonstationary factors. The forecasts and forecast limits can be plotted.

x = realization
phi is a vector of AR coefficients (default =0)
theta is a vector of MA coefficients (default =0)
d is the order of the difference operator, (1 −B)^d, in the model (default =0)
s is the seasonal order (default =0)
lambda is a vector containing the coefficients of the nonstationary not included in the difference or seasonal operators. (default =0)
n.ahead = the number of steps ahead you want to forecast (default =2)