
# Performance Reliability, and Availability Evaluation of Computational Systems

![](img/2d1450514bb14a0cdf0eb5048614afab_566_0.png)

Figure 25.10 Kaplan-Meier Applied to Grouped Censored Data.

standard deviation are. The Equation 25.2.21 can be adopted to estimate the mean time to failure, that is

$$MTTF = \frac{\sum_{i=0}^{k-1}(n_i - n_{i+1})}{\sum_{i=0}^{k-1}r_i}$$

$\bar{t}_i = (t_i + t_{i+1})/2$. The confidence interval for the MTTF can be estimated using nonparametric bootstrap (Section 6.5) through the failure times observed, so for each time interval $i$ the overall sample contains $(n_i - n_{i+1})$ $TTF_i$, where $TTF_i = \bar{t}_i(n_i - n_{i+1})$, $i \in \{0, 1, \dots, k-1\}$.

Example 25.2. Twenty routers ($n=20$) were observed under stress load for 3528h.

## Lifetime Data Analysis

![](img/2d1450514bb14a0cdf0eb5048614afab_567_0.png)

Figure 25.11 Failure Times - Kaplan-Meier Applied to Grouped Data.

### Table 25.7 Kaplan-Meier - Grouped and Complete Data

| $i$ | $t_i (h)$ | $r_i$ | $n_{i+1}$ | $t_{i-1} (h)$ | $1-r_i/n_i$ | $\hat{R}(t)$ | $\hat{F}(t)$ | $\hat{f}(t)$ | $\lambda(t)$ |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 168 | 0 | 20 | 168 | 1 | 0.0000 | 0 | 0 | |
| 2 | 236 | 0 | 20 | 168 | 1 | 0 | 0 | 0 | |
| 3 | 504 | 0 | 20 | 168 | 1 | 0 | 0 | 0 | |
| 4 | 672 | 1 | 19 | 168 | 0.9500 | 0.95 | 0.0030 | 0.031 | |
| 5 | 840 | 1 | 18 | 168 | 0.9474 | 0.9 | 0.1 | 0.0033 | |
| 6 | 1008 | 0 | 18 | 168 | 1 | 0.9 | 0.1 | 0 | |
| 7 | 1176 | 2 | 16 | 168 | 0.8889 | 0.2 | 0.0060 | 0.00074 | |
| 8 | 1344 | 1 | 15 | 168 | 0.9375 | 0.75 | 0.25 | 0.0030 | 0.0040 |
| 9 | 1512 | 0 | 15 | 168 | 1 | 0.75 | 0.25 | 0 | |
| 10 | 1680 | 2 | 13 | 168 | 0.8667 | 0.65 | 0.35 | 0 | 0.0092 |
| 11 | 1848 | 0 | 13 | 168 | 1 | 0.65 | 0.35 | 0 | |
| 12 | 2016 | 0 | 13 | 168 | 1 | 0.65 | 0.35 | 0 | |
| 13 | 2184 | 2 | 11 | 168 | 0.8462 | 0.55 | 0.45 | 0.00108 |
| 14 | 2352 | 1 | 10 | 168 | 0.9091 | 0.5 | 0.5 | 0.0030 | 0.0060 |
| 15 | 2520 | 1 | 9 | 168 | 0.4 | 0.5 | 0.5 | 0.00066 |
| 16 | 2688 | 1 | 8 | 168 | 0.8889 | 0.4 | 0.6 | 0.0070 | 0.00074 |
| 17 | 2856 | 2 | 6 | 168 | 0.75 | 0.3 | 0.7 | 0.00110 | 0.00198 |
| 18 | 3024 | 1 | 5 | 168 | 0.8333 | 0.25 | 0.75 | 0.0030 | 0.00119 |
| 19 | 3192 | 3 | 2 | 168 | 0.4 | 0.1 | 0.9 | 0.00089 | 0.00893 |
| 20 | 3360 | 2 | 0 | 168 | 0 | 0 | 1 | | |

## Performance, Reliability, and Availability Evaluation of Computational Systems

**Figure 25.12** shows the graphs $\hat{R}(t) \times t, \hat{F}(t) \times t, \hat{f}(t) \times t$, and $\hat{\lambda}(t) \times t$. The reliability at $t=2016h$ is $\hat{R}(2016h)=0.65$. Interpolation may also be adopted to estimate $\hat{R}(t)$ and $\hat{F}(t)$ at $t_j$, for $t_{i-1} < t_j < t_i, i \in \{1, 2, \dots, n\}$.

![](img/2d1450514bb14a0cdf0eb5048614afab_568_0.png)

$\hat{R}(t) \times t, \hat{F}(t) \times t, \text{ and } \hat{\lambda}(t) \times t$.

**Figure 25.12** Kaplan-Meier Applied to Grouped Data.

The estimated time to failure is MTTF = 2276.4h. Confidence interval for the MTTF was estimated using nonparametric bootstrap. The sample used to perform the resampling is a multiset of TTFs at the midpoint $t_i$, of each interval $i$ is repeated $r_i$, which is the number of failures in the interval $i$. The original sample from which the resamples are the multiset {672, 840, 1176, 1176, 1340, 1680, 2184, 2184, 2352, 2520, 2628, 2856, 3192, 3192, 3360}. The estimated interval of the MTTF, considering 95% degree of confidence is MTTF $\in$(1844.4h, 2605.6h).

### Ungrouped and Complete Data

Consider a lifetime set of data. Also, assume that the times to failure are exact, which is ungrouped. The analysis of such a data set is a particular case of Kaplan-Meier method in which $r_i=1$ and $c_i=0$ for $t_i$ (see Figure 25.13). Every $t_i$ is a failure since there is no censoring. Therefore, Equation 25.2.31 becomes

$$n_{i+1} = n_i - r_i$$
$$\hat{R}(t) = \prod_{j=1}^{i} (1 - \frac{r_j}{n_j})$$

and the other functions remain basically the same but taking into account a new calculation of $n_{i+1}$. As the data set is complete, the MTTF, the variance, standard deviation, and other statistics may be calculated. Nonparametric bootstrap may be adopted to estimate confidence intervals.

![](img/2d1450514bb14a0cdf0eb5048614afab_569_0.png)

**Figure 25.13** Failure Times - Kaplan-Meier Applied to Ungrouped and Complete Data. Forty ($n=48$) servers were observed in a accelerated test until all servers failed. The time to failure of each server was recorded. Table 25.14 summarizes the reliability analysis. Column $t_i$ shows the number of surviving devices at the beginning of the $i+1$ interval. The reliability estimate $\hat{R}(t_i)$, the cumulative time to failure estimate $\hat{F}(t_i)$, the estimate of the time failure density $\hat{f}(t_i)$, and the estimate of the failure rate $\lambda(t_i)$ are presented in the respective columns. From Table 25.8, the reliability at $2027.2h$ is estimated as $\hat{R}(2027.2h)=0.29167$. Likewise, $\hat{F}(2027.2h)=0.70833$, $\hat{f}(2027.2h)=1.565 \times 10^{-3}$ and $\hat{\lambda}(2027.2h)=5.37 \times 10^{-3}$ are estimated. The expected mean time to failure was MTTF $=1789.4$. Adopting bootstrap, a confidence interval for the MTTF was estimated. The confidence interval considering 95% degree of confidence was MTTF $\in (1423.72, 2188.38)$. Interpolation may be adopted for statistics at $t_j$, $t_{i-1} < t_j < t_i, i \in \{1, 2, \dots, n\}$. Figure 25.14 depicts the reliability and cumulative distribution function of the time to failure.

### Table 2.8 Kaplan-Meier and Complete Data

| $i$ | $t_i (h)$ | $n_{i+1}$ | $1-r_i/n_i$ | $\hat{R}(t)$ | $\hat{f}(t)$ | $\lambda(t)$ |
|---|---|---|---|---|---|---|
| 0 | 0 | 48 | 1 | 1.0000 | 0 | 0 |
| 1 | 30.04 | 47 | 0.97917 | 0.97917 | 0.02083 | 0.00694 |
| 2 | 245.07 | 46 | 0.97682 | 0.95833 | 0.01469 | 0.00001 |
| 3 | 305.49 | 45 | 0.97826 | 0.93750 | 0.06250 | 0.00403 |
| 4 | 357.54 | 44 | 0.97718 | 0.91667 | 0.08333 | 0.00400 |
| 5 | 446.86 | 43 | 0.97727 | 0.89583 | 0.10417 | 0.00233 |
| 6 | 462.02 | 42 | 0.97854 | 0.87500 | 0.13131 | 0.01357 |
| 7 | 521.41 | 40 | 0.97914 | 0.85133 | 0.14852 | 0.00401 |
| 8 | 522.82 | 39 | 0.97561 | 0.83333 | 0.16667 | 0.01475 |
| 9 | 525.27 | 38 | 0.97500 | 0.81250 | 0.18503 | 0.01047 |
| 10 | 525.47 | 37 | 0.97416 | 0.79167 | 0.20843 | 0.01041 |
| 11 | 538.37 | 36 | 0.97668 | 0.77103 | 0.22917 | 0.02634 |
| 12 | 614.26 | 35 | 0.97290 | 0.75000 | 0.25028 | 0.00534 |
| 13 | 682.11 | 34 | 0.97229 | 0.72197 | 0.27083 | 0.00942 |
| 14 | 706.58 | 33 | 0.97193 | 0.70133 | 0.29167 | 0.01433 |
| 15 | 732.23 | 32 | 0.97069 | 0.68750 | 0.32150 | 0.01140 |
| 16 | 776.81 | 31 | 0.97622 | 0.66667 | 0.34333 | 0.02469 |
| 17 | 983.01 | 29 | 0.96875 | 0.64583 | 0.35417 | 0.01001 |
| 18 | 1122.80 | 28 | 0.96724 | 0.62750 | 0.37500 | 0.01494 |
| 19 | 1162.28 | 27 | 0.96619 | 0.60417 | 0.39583 | 0.00859 |
| 20 | 1230.12 | 26 | 0.96553 | 0.58333 | 0.41667 | 0.00602 |
| 21 | 1274.35 | 25 | 0.96529 | 0.56417 | 0.43750 | 0.01008 |
| 22 | 1352.68 | 24 | 0.96296 | 0.54583 | 0.45833 | 0.00049 |
| 23 | 1400.67 | 23 | 0.96259 | 0.52014 | 0.47917 | 0.00583 |
| 24 | 1479.84 | 22 | 0.96000 | 0.50000 | 0.50000 | 0.02623 |
| 25 | 1487.25 | 21 | 0.95833 | 0.47917 | 0.52068 | 0.00543 |
| 26 | 1570.43 | 20 | 0.95462 | 0.45831 | 0.54167 | 0.00952 |
| 27 | 1587.25 | 19 | 0.95123 | 0.43125 | 0.56250 | 0.00699 |
| 28 | 1683.28 | 18 | 0.95238 | 0.41667 | 0.58333 | 0.01997 |
| 29 | 1701.61 | 17 | 0.95009 | 0.39583 | 0.60417 | 0.01117 |
| 30 | 1822.66 | 16 | 0.94737 | 0.37500 | 0.62500 | 0.00172 |
| 31 | 1911.96 | 15 | 0.94449 | 0.35337 | 0.64583 | 0.02336 |
| 32 | 1958.93 | 14 | 0.94118 | 0.33333 | 0.66667 | 0.01133 |
| 33 | 2013.19 | 13 | 0.93853 | 0.31250 | 0.68750 | 0.01012 |
| 34 | 2027.31 | 12 | 0.93729 | 0.29167 | 0.70833 | 0.00537 |
| 35 | 2113.23 | 11 | 0.92508 | 0.27917 | 0.72442 | 0.00889 |
| 36 | 2164.79 | 10 | 0.92308 | 0.25000 | 0.75000 | 0.00162 |
| 37 | 2335.64 | 9 | 0.92197 | 0.22987 | 0.77013 | 0.00294 |
| 38 | 2487.26 | 8 | 0.92009 | 0.20833 | 0.79167 | 0.00400 |
| 39 | 2883.53 | 7 | 0.90000 | 0.18750 | 0.81250 | 0.00028 |
| 40 | 3057.11 | 6 | 0.93267 | 0.16667 | 0.83333 | 0.00997 |
| 41 | 3305.78 | 5 | 0.97718 | 0.14857 | 0.85142 | 0.00058 |
| 42 | 4389.78 | 4 | 0.88000 | 0.12850 | 0.87500 | 0.00198 |
| 43 | 4011.25 | 3 | 0.83333 | 0.10417 | 0.89583 | 0.00032 |
| 44 | 4138.45 | 2 | 0.80000 | 0.08333 | 0.91667 | 0.00196 |
| 45 | 4870.55 | 1 | 0.75000 | 0.06250 | 0.93750 | 0.00543 |
| 46 | 4939.94 | 0 | 0.66667 | 0.04167 | 0.95833 | 0.00721 |
| 47 | 5423.31 | 0 | 0.50000 | 0.02083 | 0.97917 | 0.00391 |
| 48 | 5479.37 | 0 | 0 | 1 | 0.00048 |
