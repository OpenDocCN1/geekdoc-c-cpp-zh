# Residuals (fit)

![](bbox=[0.18, 0.15, 0.85, 0.53])

Figure 6.13 Forecast-arima.

```
method=c("CSS-ML","ML","CSS"), n.cond,
optim.control=list(), kappa=1e6, model=NULL)
> fit <- Arima(MWusage,order=c(3,1,0))
> plot(forecast(fit,h=20))
> # Outputting: Figure 6.14 ARIMA-1
```

# Forecasts from ARIMA(3,1,0)

![](bbox=[0.18, 0.78, 0.85, 0.93])

Figure 6.14 ARIMA-1.