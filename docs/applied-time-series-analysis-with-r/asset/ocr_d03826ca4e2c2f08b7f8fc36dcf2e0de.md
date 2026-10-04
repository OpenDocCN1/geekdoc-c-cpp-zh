# 436 Applied Time Series Analysis with R

$\hat{X}_t^2 = 0.9\hat{X}_{t-1}^2 = -0.471$
$\Gamma_t^2 = 0.81\Gamma_{t-1}^2 + 1 = 1.429$
$K_2 = \frac{\Gamma_t^2}{\Gamma_{t-1}^2 + 0.75} = \frac{1.429}{1.429 + 0.75} = 0.656$
$\hat{X}_t^2 = \hat{X}_{t-1}^2 + K_2(y_2 - \hat{X}_{t-1}^2) = -0.471 + 0.656(0.045 + 0.471) = -0.132$

and so forth.

In Table 10.1, we show the predictors $(\hat{X}_t)$, filters $(	ilde{X}_t)$, and smoothers $(\hat{X}_t^s)$ along with associated mean-squared errors $(\Gamma_t^2)$ for the data in Figure 10.11 for $t=1, \dots, 5$. There is we, as would be expected, that the mean-squared errors for prediction are greater than for filters (which are based on the initial data value $Y_0$), and these are in greater than for the smoothers (which are based on all $n=75$ data values in the realization). From $\hat{X}_t$ (light line) shown in Figure 10.11 along the predicted, filtered, and smoothed estimates, respectively. There can be seen that the filtered values (dark line in (b)) are somewhat close to the true values (light line) than the predictors and filters. In Figure 10.12c smoother than the predictors and filters. The observed mean-squared errors, $MSE = (1/75)\sum_{s=1}^{75}(\hat{X}_s - x_s)^2$, are 1.25 for predictors $(s=t-1)$, 0.51 for filters $(t)$, and 0.43 for smoothers $(s=75)$. Thus, the smoothers tend to be marginally closer to the true values than both filters while smoothers offer a substantial improvement over the predictors.

Using R: The results in Table 10.1 were obtained using the kalian.wge function in twge. This function is based on a call to Kalmansmo the astsa package has several functions for performing Kalman filtering. The korean.wge function is a univariate simplification designed to perform analyses such as the predicting, filtering, and smoothing setting considered in Example 10.12. For description of the statements made to create the data in Table 10.2, see Appendix 10B.

# 10.6.5 Kalman Filtering and Missing Data

Suppose, we observe $(y_1, y_2, \dots, y_n)$, for $1 \le t_1 < t_2 < \dots \le t$ and the $t'_s$ are integers. There, there is $n-r$ missing observations. Such a situation (which is all common in practice) would cause serious problems with attempts to analyze this type of data using ARMA$(p,q)$ model based on techniques discussed in previous chapters of this book. One of the advantages of the state-space model is that it provides the ability to analyze such data. Specifically, state-space modeling provides at least two methods for dealing with this situation: (a) estimation of model parameters (using ML) even with some missing data and (b) estimation of missing values.