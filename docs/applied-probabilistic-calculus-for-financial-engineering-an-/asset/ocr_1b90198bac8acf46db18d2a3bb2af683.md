```
DELL 0 0.011769151 0.015853209 0.034133394 0.009431736
0.011381346 0.006756110
C 0.010298180 0.010405993 0.009431736 0.010811254 0.008246582
0.004926015
JPM 0.007407937 0.011371177 0.011381346 0.008246582
0.012875001 0.006741935
BAC 0.003690800 0.00469313 0.006756110 0.004926015
0.006741935 0.007630011

> invViews <- matrix(ncol = 4, nrow = 1, dimnames = list(NULL,
+ c("JPM", "BAC", "MS")))
> invViews[,1:4] <- rep(1/4,4)
> views <- addBLViews(views, 0.15, 90, views)
> views
1 : 0.5*IBM-1*MS+0.5*DELL=0.06 + eps. Confidence: 100
2 : 0.25*MS+0.25*C+0.25*JPM+0.25*BAC=0.15
  + eps. Confidence: 90

> marketPosterior <- BLPosterior(as.matrix(monthlyReturns),
+ views, tau =1/2,
+ marketIndex = as.matrix(sp500Returns), riskFree =
+ as.matrix(US13WTB)
+ )
>
> BLPosterior # Output:
function (returns, views, tau = 1, marketIndex, riskFree = NULL,
    kappa = 0, covEstimator = "cov")
{
    covEstimator <- match.fun(covEstimator)
    alphaInfo <- CAPMList(returns, marketIndex, riskFree =
riskFree)
    post <- posteriorEst(views, tau = tau, mu = alphaInfo
[["alphas"]],
        sigma = unclass(covEstimator(returns)), kappa = kappa)
    post
}
<environment: namespace:BLCOP>
>
> marketPosterior <- BLPosterior(as.matrix(monthlyReturns),
+ views, tau =1/2,
+ marketIndex = as.matrix(sp500Returns), riskFree =
+ as.matrix(US13WTB) )
> marketPosterior
```