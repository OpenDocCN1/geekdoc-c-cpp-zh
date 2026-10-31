
```r
[57] "meucci.moments"              "meucci.ranking"
[59] "minimax_objective"             "mult.portfolio.spec"
[61] "objective"                     "optimize.portfolio"
[63] "optimize.portfolio.parallel"   "optimize.portfolio.rebalancing"
[65] "optimize.portfolio.rebalancing_v1" "optimize.portfolio_v1"
[67] "optimize.portfolio_v2"         "portfolio.spec"
[69] "portfolio_risk_objective"      "pos_limit_fail"
[71] "position_limit_constraint"     "quadratic_utility_objective"
[73] "random_portfolios"             "random_portfolios_v1"
[75] "random_portfolios_v2"          "random_walk_portfolios"
[77] "randomize_portfolio"           "randomize_portfolio_v1"
[79] "randomize_portfolio_v2"        "regime.portfolios"
[81] "return_constraint"              "return_objective"
[83] "risk_budget_objective"          "rp_grid"
[85] "rp_sample"                      "rp_simplex"
[87] "rp_transform"                   "scatterFUN"
[89] "set.portfolio.moments"          "statistical.factor.model"
[91] "trailingFUN"                    "transaction_cost_constraint"
[93] "turnover"                       "turnover_constraint"
[95] "turnover_objective"             "update_constraint_v1tov2"
[97] "var.portfolio"                  "weight_constraint_objective"
[99] "weight_sum_constraint"
> ac.ranking
function (R, order, ...)
{
    if (length(order) != ncol(R))
        stop("The length of the order vector must equal the number of
assets")
    nassets <- ncol(R)
    if (hasArg(max.value)) {
        max.value <- match.call(expand.dots = TRUE)$max.value
    }
    else {
        max.value <- median(colMeans(R))
    }
    c_hat <- scale.range(centroid(nassets), max.value)
    out <- vector("numeric", nassets)
    out[rev(order)] <- c_hat
    return(out)
}
<environment: namespace:PortfolioAnalytics>
> data(edhec)
> edhec

| Date | Convertible Arbitrage | CTA Global | Distressed Securities |
|---|---|---|---|
|1997-01-31|0.0119|0.0393|0.0178|
|1997-02-28|0.0123|0.0298|0.0122|
|1997-03-31|0.0078|-0.0021|-0.0012|
|1997-04-30|0.0086|-0.0170|0.0030|
|1997-05-31|0.0156|-0.0015|0.0233|
|2009-06-30|0.0241|-0.0147|0.0198|
|2009-07-31|0.0611|-0.0012|0.0311|
|2009-08-31|0.0315|0.0054|0.0244|

| Date | Emerging Markets | Equity Market Neutral | Event Driven |
|---|---|---|---|
|1997-01-31|0.0791|0.0189|0.0213|
|1997-02-28|0.0525|0.0101|0.0084|
|1997-03-31|-0.0120|0.0016|-0.0023|
|1997-04-30|0.0119|0.0119|-0.0005|
|1997-05-31|0.0315|0.0189|0.0346|
|2009-06-30|0.0013|0.0036|0.0123|
|2009-07-31|0.0451|0.0042|0.0291|
|2009-08-31|0.0166|0.0070|0.0207|

| Date | Fixed Income Arbitrage | Global Macro | Long/Short Equity |
|---|---|---|---|
|1997-01-31|0.0191|0.0573|0.0281|
|1997-02-28|0.0122|0.0175|-0.0006|
|1997-03-31|0.0109|-0.0119|-0.0084|
|1997-04-30|0.0130|0.0172|0.0084|
|1997-05-31|0.0118|0.0108|0.0394|
|2009-06-30|0.0126|-0.0076|0.0009|
|2009-07-31|0.0322|0.0166|0.0277|
|2009-08-31|0.0202|0.0050|0.0157|

| Date | Merger Arbitrage | Relative Value Arbitrage | Short Selling | Funds of Funds |
|---|---|---|---|---|
|1997-01-31|0.0150|0.0180|-0.0166|0.0317|
|1997-02-28|0.0034|0.0118|0.0426|0.0106|
|1997-03-31|0.0060|0.0010|0.0778|-0.0077|
|1997-04-30|-0.0001|0.0122|-0.0129|0.0009|
|1997-05-31|0.0197|0.0173|-0.0737|0.0275|
|2009-06-30|0.0104|0.0101|-0.0094|0.0024|
|2009-07-31|0.0068|0.0260|-0.0596|0.0153|
|2009-08-31|0.0102|0.0162|-0.0165|0.0113|

------------------------------------------------------------------------
2009-06-30      0.0104      0.0101     -0.0094      0.0024
2009-07-31      0.0068      0.0260     -0.0596      0.0153
2009-08-31      0.0102      0.0162     -0.0165      0.0113
> R <- edhec[,1:4]
> ac <- ac.ranking(R, c(2,3,1,4))
[1] 0.01432457 -0.05000000 -0.01432457 0.05000000

> R # R = edhec[,1:4]; viz. Column Vectors 1 thru 4 of edhec:
#
#     1. Convertible Arbitrage
#     2. CTA Global
#     3. Distressed Securities
#     4. Emerging Markets
#
# but NOT Columns 5 thru 6:
#     5. Equity Market
#     6. Neutral Event Driven
# and, those 4 columns are:
#
              Convertible  CTA          Distressed
              Arbitrage     Global       Securities
1997-01-31       0.0119      0.0393        0.0178
1997-02-28       0.0123      0.0298        0.0122
1997-03-31       0.0078     -0.0021       -0.0012
1997-04-30       0.0086     -0.0170        0.0030
1997-05-31       0.0156     -0.0015        0.0233
------------------------------------------------------------------------
2009-06-30       0.0241     -0.0147        0.0198
2009-07-31       0.0611     -0.0012        0.0311
2009-08-31       0.0315      0.0054        0.0244

              Emerging
              Markets
1997-01-31       0.0791
1997-02-28       0.0525
1997-03-31      -0.0120
1997-04-30       0.0119
1997-05-31       0.0315
------------------------------------------------------------------------
2009-06-30       0.0013
2009-07-31       0.0451
2009-08-31       0.0166
>

> ac.ranking(R, c(2, 3, 1, 4))
> # Outputting:
[1] 0.01432457 -0.05000000 -0.01432457 0.05000000

## Remark:

order a vector of indexes of the relative ranking of expected asset returns in ascending order. Thus, the order = c(2, 3, 1, 4) means that the expected returns of R[,2] < R[,3] < R[,1] < R[,4].

## 6.4.4.4 Worked Example for Portfolio Optimization – Portfolio Optimization by AssetsM in CRAN

### Worked Example No. 8

In the R domain:

```
> library(urca)
Warning message:
package 'urca' was built under R version 3.2.3
> library(vars)
Loading required package: MASS
Loading required package: strucchange
Loading required package: zoo
Attaching package: 'zoo'
The following objects are masked from 'package:base':
as.Date, as.Date.numeric
Loading required package: sandwich
Loading required package: lmtest
Warning messages:
1: package 'vars' was built under R version 3.2.3
2: package 'MASS' was built under R version 3.2.4
3: package 'strucchange' was built under R version 3.2.3
4: package 'lmtest' was built under R version 3.2.3
> ## Loading data set and converting to zoo
> data(EuStockMarkets)
> Assets <- as.zoo(EuStockMarkets)
> ## Aggregating as month's-end series
> AssetsM <- aggregate(Assets, as.yearmon, tail, 1)
> head(AssetsM)
> # Outputting:
DAX SMI CAC FTSE
```

Jun 1991 1628.75 1678.1 1772.8 2443.6
Jul 1991 1619.29 1727.2 1754.7 2588.8
Aug 1991 1649.88 1736.6 1864.3 2645.7
Sep 1991 1605.47 1664.7 1880.6 2621.7
Nov 1991 1571.06 1622.6 1739.7 2420.2

### Applying unit root tests for subsample

```
> AssetsMsub <- window(AssetsM, start = start(AssetsM), end =
+ "Jun 1996")
```

### Levels

```
> ADF <- lapply(AssetsMsub, ur.df, type = "drift", selectlags =
+ "AIC")
> ERS <- lapply(AssetsMsub, ur.ers)
```

### Differences

```
> DADF <- lapply(diff(AssetsMsub), ur.df, selectlags = "AIC")
> DERS <- lapply(diff(AssetsMsub), ur.ers)
```

```
> VECM
> VEC <- ca.jo(AssetsMsub, ecdet = "none", spec = "transitory")
> summary(VEC)
```

# > # Outputting:

################
# Johansen-Procedure #
################

Test type: maximal eigenvalue statistic (lambda max), with linear trend
Eigenvalues (lambda):
[1] 0.431634123 0.245497723 0.091715832 0.001757365
Values of teststatistic and critical values of test:

test 10pct 5pct 1pct
r <=3 | 0.10 6.50 8.18 11.65
r <=2 | 5.68 12.91 14.90 19.19
r <=1 |16.62 18.90 21.07 25.75
r =0 |33.33 24.78 27.14 32.14

Eigenvectors, normalised to first column:
(These are the co-integration relations)
DAX.l1 SMI.l1 CAC.l1 FTSE.l1
DAX.l1 1.000000 1.0000000 1.000000 1.0000000
SMI.l1 -6.031316 -0.35450941 -1.797697 0.4074565
CAC.l1 4.545907 0.04603755 -2.607493 -0.7843438
FTSE.l1 7.547658 -0.29885304 2.049960 -0.4496086
Weights W:
(This is the loading matrix)

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
