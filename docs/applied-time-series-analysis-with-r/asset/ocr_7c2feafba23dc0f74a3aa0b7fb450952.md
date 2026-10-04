# 382 Applied Time Series Analysis with R

![](bbox=[0.143, 0.131, 0.808, 0.303])

**FIGURE 9.4**
(a) Residuals from AR(4) fit to the global temperature data. (b) Sample autocorrelations of the residuals in (a).

wandering behavior of the realization makes the inclusion of a unit root (i.e., a factor of $1 - B$) plausible. Therefore, we consider the temperature data by differencing the data to calculate $Y_t = X_t - X_{t-1} = (1 - B)X_t$, and then modeling $Y_t$ as an AR(p) process. The differenced data are shown in Figure 9.5a

![](bbox=[0.143, 0.483, 0.808, 0.853])

**FIGURE 9.5**
(a) Differenced global temperature data in Figure 1.24a. (b) Sample autocorrelations for the data in (a). (c) Residuals from an AR(3) MLE fit to the differenced data in (a). (d) Sample autocorrelations for the residuals in (c).