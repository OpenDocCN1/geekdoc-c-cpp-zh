
## Vector-Valued (Multivariate) Time Series

## EXAMPLE 10.12: PREDICTING, FILTERING, AND SMOOTHING DATA IN FIGURE 10.11

In this example, we illustrate the concepts of predicting, filtering, and smoothing using the data in Figure 10.11. In Example 10.9, it was seen that the series $X_t$ is an AR(1) model where the observations $Y_t$ follow an AR(1)-plus-noise model. We will use $\hat{X}_t^i$ from Equations 10.50 to find the predictions, $\hat{X}_t^i$, and filters $\Gamma_t^i$ (along with the corresponding mean-errors for the underlying signal, $Y_t$, and using the model parameters $F = \phi_i = 0.9$, $\sigma_t^2 = 1$, $G = 1$, and $\Gamma_w = \sigma_w = 0.75$). The predictions and filters are computed for $t=1, \dots, n_i$; we use the smoothing Equations 10.55 through 10.57 to calculate the smoothers, $\hat{\Gamma}_t^i$, with the corresponding mean-squared errors.

In Table 10.1, we show the underlying (observable) values of $Y_t$ for $t=1, \dots, 5$. (Recall that the full realization in Figure 10.11 has $n=75$ observations). The recursion is initialized with $X_0$, which is considered to be unknown from the AR(1) model $X_t - 0.9X_{t-1} = \epsilon_t$, where $\sigma_t^2 = 1$. $E(X_t)=0$, we assign $\hat{X}_0^i = x_0 = 0$. Also, we initialize $\Gamma_0^i = 1$. In this simple example, Equations 10.50 through 10.54 be $\hat{X}_t^i = 0.9\hat{X}_{t-1}^i + \Gamma_{t-1}^i$, $\Gamma_t^i = 0.81\hat{X}_{t-1}^i + 1, \hat{X}_t^i = \hat{X}_t^i + K_t(y_t - \hat{X}_t^i), \Gamma_t^i = (1-K_t)\Gamma_{t-1}^i$, and $K_t = \Gamma_t^i / (\Gamma_t^i + 0.75)$, respectively. So, it follows that:

```
\hat{X}_1^i = 0.9\hat{X}_0^i = 0
\Gamma_1^i = 0.81(1) + 1 = 1.81
K_1 = \frac{\Gamma_1^i}{\Gamma_1^i + \sigma_w^2} = \frac{1.81}{1.81 + 0.75} = 0.707
\hat{X}_1^i = \hat{X}_1^i + K_1(y_1 - \hat{X}_1^i) = 0 + 0.707(-0.74 - 0) = -0.523
\Gamma_1^i = (1 - K_1)\Gamma_0^i = (1 - 0.707)1.81 = 0.530
```

## TABLE 10.1
Predictors, Filters, and Smoothers for Data in Figure 10.11

| $t$ | $X_t$ | $Y_t$ | $\hat{X}_{t-1}^i$ | $\Gamma_{t-1}^i$ | $\hat{X}_t^i$ | $\Gamma_t^i$ | $\hat{\Gamma}_t^i$ | $\Gamma_t^i$ |
|---|---|---|---|---|---|---|---|---|
| 0 | | | | | 0.00 | 1.00 | -0.26 | 0.65 |
| 1 | -0.25 | -0.74 | 0.00 | 1.81 | -0.52 | 0.53 | -0.51 | 0.41 |
| 2 | -0.08 | 0.05 | -0.47 | 1.43 | -0.13 | 0.49 | -0.44 | 0.39 |
| 3 | -0.65 | -0.78 | -0.12 | 1.40 | -0.55 | 0.49 | -1.10 | 0.39 |
| 4 | -1.77 | -2.94 | -0.49 | 1.40 | -2.09 | 0.49 | -2.25 | 0.39 |
| 5 | -2.72 | -2.28 | -1.88 | 1.40 | -2.14 | 0.49 | -2.40 | 0.39 |

$\hat{X}_t^2 = 0.9\hat{X}_{t-1}^2 = -0.471$
$\Gamma_t^2 = 0.81\Gamma_{t-1}^2 + 1 = 1.429$
$K_2 = \frac{\Gamma_t^2}{\Gamma_{t-1}^2 + 0.75} = \frac{1.429}{1.429 + 0.75} = 0.656$
$\hat{X}_t^2 = \hat{X}_{t-1}^2 + K_2(y_2 - \hat{X}_{t-1}^2) = -0.471 + 0.656(0.045 + 0.471) = -0.132$

and so forth.

In Table 10.1, we show the predictors $(\hat{X}_t)$, filters $(\tilde{X}_t)$, and smoothers $(\hat{X}_t^s)$ along with associated mean-squared errors $(\Gamma_t^2)$ for the data in Figure 10.11 for $t=1, \dots, 5$. There is, as would be expected, that the mean-squared errors for prediction are greater than for filters (which are based on the initial data value $Y_0$), and these are greater than for the smoothers (which are based on all $n=75$ data values in the realization). From $\hat{X}_t$ (light line) shown in Figure 10.11 along the predicted, filtered, and smoothed estimates, respectively. There can be seen that the filtered values (dark line in (b)) are somewhat close to the true values (light line) than the predictors and filters. In Figure 10.12c, smoother than the predictors and filters. The observed mean-squared errors, $MSE = (1/75)\sum_{s=1}^{75}(\hat{X}_s - x_s)^2$, are 1.25 for predictors $(s=t-1)$, 0.51 for filters $(t)$, and 0.43 for smoothers $(s=75)$. Thus, the smoothers tend to be marginally closer to the true values than both filters while smoothers offer a substantial improvement over the predictors.

Using R: The results in Table 10.1 were obtained using the `kalmanfilter` function in the `forecast` package. This function is based on a call to `kalman`, a univariate simplification designed to perform analyses such as the predicting, filtering, and smoothing setting considered in Example 10.12. For description of the statements to create the data in Table 10.2, see Appendix 10.B.

## 10.6.5 Kalman Filtering and Missing Data

Suppose, we observe $(y_1, y_2, \dots, y_n)$, for $1 \le t_1 < t_2 < \dots \le t_r \le n$ are integers, there are $n-r$ missing observations. Such a situation (which is all common in practice) would cause serious problems with attempts to analyze this type of data using ARMA$(p,q)$ model based on techniques discussed in previous chapters of this book. One of the advantages of the state-space model is that it provides the ability to analyze such data. Specifically, state-space modeling provides at least two methods for dealing with this situation: (a) estimation of model (using ML) and (b) estimation of missing values.

![FIGURE 10.12](img/41dcbf9af56fa8895afde2197b0b_453_0.png)
![FIGURE 10.12](img/41dcbf9af56fa8895afde2197b0b_453_1.png)
![FIGURE 10.12](img/41dcbf9af56fa8895afde2197b0b_453_2.png)
FIGURE 10.12 overlaid with (a) predictors $\hat{X}_t^{i-1}$, (b) filters $\hat{X}_t^i$, and (c) smoothers $\hat{X}_t^s$.

## TABLE 10.2
Predictors, Filters, and Smoothers for Data in Figure 10.11

| $t$ | $X_t$ | $Y_t$ | $\hat{X}_{t-1}^i$ | $\hat{X}_t^i$ | $\Gamma_{t-1}^i$ | $\hat{X}_t^s$ | $\Gamma_t^s$ |
|---|---|---|---|---|---|---|---|
| 0 | | | | 0.00 | 1.00 | -0.35 | 0.67 |
| 1 | -0.25 | -0.74 | 0.00 | -0.52 | 1.81 | -0.69 | 0.46 |
| 2 | -0.08 | 0.05 | -0.47 | 1.43 | 1.43 | -0.98 | 0.82 |
| 3 | -0.65 | -0.78 | -0.12 | 2.16 | 1.40 | -1.28 | 0.44 |
| 4 | -1.77 | -2.94 | -0.49 | 1.45 | 1.40 | -2.35 | 0.43 |
| 5 | -2.72 | -2.28 | -1.88 | 1.94 | 1.40 | -2.57 | 0.81 |

In order to construct the state and observation equations for this missing data, we first define

$y_t^* = \begin{cases} y_t & \text{if } t \in \{t_1, t_2, \dots, t_r\} \\ 0 & \text{otherwise}. \end{cases}$

Then, the state-space model is

$X_t = F X_{t-1} + V_t$, state equation (unchanged),
$Y_t = G_t^* X_t + W_t^*$, new observation equation,

where

$G_t^* = \begin{cases} G_t, & \text{if } t \in \{t_1, t_2, \dots, t_r\} \\ 0, & \text{otherwise}\end{cases}$
$W_t^* = \begin{cases} W_t, & \text{if } t \in \{t_1, t_2, \dots, t_r\} \\ N_t, & \text{otherwise},\end{cases}$

and $(N_t)$ are iid $N(0,1)$ and uncorrelated with $V_t$ and $W_t$.

## EXAMPLE 10.13: EXAMPLE 10.12 REVISITED WITH TWO MISSING VALUES

Suppose the observations, $y_t$, for $t=2$ and $t=5$ are missing. That is, we define

$y_t^* = \begin{cases} y_t & \text{if } t \in \{1, 3, 4, 6 \text{ through } 75\} \\ 0, & \text{otherwise},\end{cases}$

since $E(Y_t) = 0$. The revised state-space equations are

$X_t = \phi_t X_{t-1} + V_t$
$Y_t^* = G_t^* X_t + W_t^*$

where

$Y_t^* = \begin{cases} y_t & \text{if } t \neq 2, 5 \\ 0, & \text{if } t = 2, 5 \end{cases}$
$G_t^* = \begin{cases} 1, & \text{if } t \neq 2, 5 \\ 0, & \text{if } t = 2, 5 \end{cases}$
$W_t^* = \begin{cases} W_t & \text{if } t \neq 2, 5 \\ W_t + N_t, & \text{if } t = 2, 5 \end{cases}$

We let $N_t \sim N(0, 1)$ denote noise that is uncorrelated with both $V_t$ and $W_t$. Consequently,

$\sigma_{W_t^*}^2 = \begin{cases} 0.75, & \text{if } t \neq 2, 5 \\ 1.75, & \text{if } t = 2, 5.\end{cases}$

## Vector-Valued (Multivariate) Time Series

The missing values are estimated using Kalman iteration to calculate $\hat{X}_t, \hat{X}_{t^{-1}}^{\Gamma_t}$, and $\Gamma_{t^{+1}}, t=1,\dots,75$, and then for $t=75,74,\dots,1$, the smoothing iterations are used to calculate the values for $\hat{X}_t^S$ and $\hat{\Gamma}_t^S$, which are the desired estimates. In Table 10.2, we show the revised version of Table 10.1 where $y_i$ and $y_j$ are missing. As expected, it can be seen that the cases with available data $Y_\cdot$.

**Using R:** The results in Table 10.2 were obtained using the `kalman.miss` function in the `forecast` package. This function is based on a call to `kalman`, a univariate simplification designed to perform analyses such as the predicting, filtering, and smoothing setting considered in Example 10.12.
