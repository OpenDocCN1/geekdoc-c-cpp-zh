[16] "dshw" "easter" "ets"
[19] "findfrequency" "fitted.Arima" "forecast"
[22] "forecast.ar" "forecast.Arima" "forecast.bats"
[25] "forecast.ets" "forecast.fracdiff" "forecast.HoltWinters"
[28] "forecast.ln" "forecast.nnetar" "forecast.stl"
[31] "forecast.stlm" "forecast.StructTS" "forecast.tbats"
[34] "fourier" "fourierf" "gas"
[37] "geom_forecast" "GeomForecast" "getResponse"
[40] "ggAcf" "ggCcF" "ggmonthplot"
[43] "ggPacf" "ggseasonplot" "ggtaperedacf"
[46] "ggtaperedpacf" "ggtsdisplay" "gold"
[49] "holt" "hw" "InvBoxCox"
[52] "is.acf" "is.Arima" "is.bats"
[55] "is.constant" "is.ets" "is.forecast"
[58] "is.mforecast" "is.nnetar" "is.nnetamodels"
[61] "is.splineforecast" "is.stlm" "logLik.ets"
[64] "ma" "meanf" "monthdays"
[67] "msts" "na.interp" "naive"
[70] "ndiffs" "nnetar" "nsdiffs"
[73] "Pacf" "plot.ar" "plot.Arima"
[76] "plot.bats" "plot.ets" "plot.forecast"
[79] "plot.splineforecast" "plot.tbats" "rwf"
[82] "seasadj" "seasonaldummy" "seasonaldummyf"
[85] "seasonplot" "ses" "simulate.ar"
[88] "simulate.Arima" "simulate.ets" "simulate.fracdiff"
[91] "sindexf" "snaive" "splinef"
[94] "StatForecast" "stlf" "stl"
[97] "subset.ts" "taperedacf" "taperedpacf"
[100] "taylor" "tbats" "tbats.components"
[103] "thetacf" "tsclean" "tsdisplay"
[106] "tslm" "tsoutliers" "wineind"
[109] "woolyrng"

# Example 1: forecast-accuracy

```
> fit1 <- rwf(EuStockMarkets[1:200,1],h=100)
> fit2 <- meanf(EuStockMarkets[1:200,1],h=100)
> accuracy(fit1)
ME RMSE MAE MPE MAPE MASE ACF1
Training set 0.4393467 15.8461 8.959648 0.02128535 0.5533582
1 -0.007760885
```