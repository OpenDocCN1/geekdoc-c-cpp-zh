
# 536 Performance, Reliability, and Availability Evaluation of Computational Systems

An alternative is to adopt

```
$$\hat{F}(t_i) = \frac{i}{n+1}, \quad (25.2.5)
```

which leads to

```
$$\hat{R}(t_i) = \frac{n+1-i}{n+1}, \quad (25.2.6)
```

Hence,

```
$$\hat{f}(t_i) = \frac{1}{(n+1)(t_i-t_{i-1})}, \quad (25.2.7)
```

and

```
$$\hat{\lambda}(t_i) = \frac{1}{(n+1-i)(t_i-t_{i-1})}, \quad (25.2.8)
```

$\hat{F}(t_i), \hat{R}(t_i), \hat{f}(t_i),$ and $\hat{\lambda}(t_i)$ are provided in the responsive columns of Table 25.1. Another alternative is based on medians. The medians are usually numerically calculated. The following formula is often adopted as an approximation of the median [40, 42].

```
$$\hat{F}(t_i) = \frac{i-0.3}{n+0.4}, \quad (25.2.9)
```

```
$$\hat{R}(t_i) = \frac{n+0.7-i}{n+0.4}, \quad (25.2.10)
```

```
$$\hat{f}(t_i) = \frac{1}{(n+0.4)(t_i-t_{i-1})}, \quad (25.2.11)
```

and

```
$$\hat{\lambda}(t_i) = \frac{1}{(n+0.7-i)(t_i-t_{i-1})}, \quad (25.2.12)
```

The mean time to failure is estimated by

```
$$MTTF = \frac{\sum_{i=1}^{n} t_i}{n}, \quad (25.2.13)
```

Other statistics as standard deviation, variance, skewness, kurtosis, and quantile may also be calculated from the sample (see Chapter 3). The confidence interval of the mean time to failure may also be estimated using bootstrap (see Section 6.5).

**Example 25.2.1.** Consider a set of fifty servers ($n=50$) was set for an accelerate reliability test. The test finished when all presented presented a failure. Table 25.2, Column

# Lifetime Data Analysis

# Table 25.2
Ungrouped Complete Lifetime

| i | t_i | R(t_i) | F(t_i) | f(t_i) | \lambda(t_i) |
|---|---|---|---|---|---|
| 1 | 2.9 | 1.0000 | 0.0000 | 0.0068 | 0.0069 |
| 2 | 41.1 | 0.9861 | 0.0139 | 0.0005 | 0.0005 |
| 3 | 42.3 | 0.9663 | 0.0337 | 0.0162 | 0.0172 |
| 4 | 43.6 | 0.9464 | 0.0536 | 0.0159 | 0.0171 |
| 5 | 60.2 | 0.9266 | 0.0734 | 0.0012 | 0.0113 |
| 6 | 86.4 | 0.9065 | 0.0931 | 0.0068 | 0.0099 |
| 7 | 88.5 | 0.8869 | 0.1131 | 0.0095 | 0.0110 |
| 8 | 101.7 | 0.8671 | 0.1329 | 0.0015 | 0.0018 |
| 9 | 120.7 | 0.8472 | 0.1528 | 0.0010 | 0.0013 |
| 10 | 160.2 | 0.8274 | 0.1726 | 0.0005 | 0.0009 |
| 11 | 182.3 | 0.8075 | 0.1925 | 0.0006 | 0.0009 |
| 12 | 219.4 | 0.7877 | 0.2132 | 0.0004 | 0.0005 |
| 13 | 271.1 | 0.7679 | 0.2321 | 0.0004 | 0.0005 |
| 14 | 273.7 | 0.7480 | 0.2520 | 0.0073 | 0.0101 |
| 15 | 281.3 | 0.7282 | 0.2718 | 0.0026 | 0.0037 |
| 16 | 388.0 | 0.7083 | 0.2917 | 0.0002 | 0.0003 |
| 17 | 396.9 | 0.6883 | 0.3115 | 0.0002 | 0.0033 |
| 18 | 557.8 | 0.6683 | 0.3311 | 0.0008 | 0.0146 |
| 19 | 602.6 | 0.6468 | 0.3515 | 0.0008 | 0.0148 |
| 20 | 626.6 | 0.6290 | 0.3710 | 0.0003 | 0.0005 |
| 21 | 665.0 | 0.6091 | 0.3909 | 0.0005 | 0.0005 |
| 22 | 704.2 | 0.5893 | 0.4107 | 0.0005 | 0.0009 |
| 23 | 775.5 | 0.5694 | 0.4306 | 0.0004 | 0.0007 |
| 24 | 774.8 | 0.5496 | 0.4594 | 0.0012 | 0.0022 |
| 25 | 820.1 | 0.5298 | 0.4792 | 0.0001 | 0.0093 |
| 26 | 1072.1 | 0.5095 | 0.4991 | 0.0005 | 0.0010 |
| 27 | 1113.0 | 0.4901 | 0.5099 | 0.0005 | 0.0010 |
| 28 | 1149.3 | 0.4702 | 0.5298 | 0.0006 | 0.0014 |
| 29 | 1169.7 | 0.4504 | 0.5496 | 0.0001 | 0.0018 |
| 30 | 1378.5 | 0.4306 | 0.5694 | 0.0001 | 0.0018 |
| 31 | 1453.5 | 0.4107 | 0.5893 | 0.0003 | 0.0007 |
| 32 | 1507.7 | 0.3909 | 0.6099 | 0.0004 | 0.0010 |
| 33 | 1529.4 | 0.3710 | 0.6290 | 0.0009 | 0.0025 |
| 34 | 1688.1 | 0.3512 | 0.6488 | 0.0001 | 0.0004 |
| 35 | 1762.3 | 0.3313 | 0.6687 | 0.0003 | 0.0099 |
| 36 | 1940.3 | 0.3115 | 0.6883 | 0.0001 | 0.0099 |
| 37 | 2022.0 | 0.2917 | 0.7083 | 0.0002 | 0.0099 |
| 38 | 2174.3 | 0.2718 | 0.7282 | 0.0001 | 0.0099 |
| 39 | 2185.2 | 0.2520 | 0.7480 | 0.0016 | 0.0063 |
| 40 | 2260.5 | 0.2321 | 0.7679 | 0.0013 | 0.0016 |
| 41 | 2353.0 | 0.2123 | 0.7877 | 0.0002 | 0.0111 |
| 42 | 2388.0 | 0.1925 | 0.8076 | 0.0003 | 0.0033 |
| 43 | 2759.8 | 0.1726 | 0.8264 | 0.0001 | 0.0003 |
| 44 | 3029.0 | 0.1528 | 0.8472 | 0.0001 | 0.0096 |
| 45 | 3172.5 | 0.1329 | 0.8671 | 0.0001 | 0.0112 |
| 46 | 3251.1 | 0.1131 | 0.8869 | 0.0003 | 0.0227 |
| 47 | 3355.4 | 0.0933 | 0.9067 | 0.0002 | 0.0026 |
| 48 | 3803.7 | 0.0734 | 0.9266 | 0.0000 | 0.0008 |
| 49 | 4555.9 | 0.0536 | 0.9464 | 0.0000 | 0.0008 |
| 50 | 7847.7 | 0.0337 | 0.9663 | 0.0000 | 0.0004 |

# 538 Performance Reliability, and Availability Evaluation of Computational Systems t_i, presents the time to failure of servers in ascending order. Columns $\hat{R}(t_i)$, $\hat{F}(t_i)$, $\hat{f}(t_i)$, and $\hat{\lambda}(t_i)$ depict the reliability, the cumulative time distribution, and the failure rate at $t_i$, respectively. In this specific study Functions 25.2.10, 25.2.9, 25.2.11 and 25.2.12 were adopted. From this table, the reliability at $2022h$ is estimated as $\hat{R}(2022h) = 0.2917$. Likewise, $\hat{F}(t)$, $\hat{f}(t)$, and $\hat{\lambda}(t)$ are estimated. The estimated time to failure was MTTF = 134.85h. Adopting bootstrap, a confidence interval for the MTTF was estimated. The confidence interval obtained 95% of confidence is MTTF $(1016.57h, 1811.27h).

The reliability $\hat{R}(t)$ and the cumulative function $\hat{F}(t)$ are step functions that decreases and increases, respectively, each observed time. Consequently, some graph the reliability and cumulative function estimate as step functions. The density estimate $\hat{f}(t_i)$ is well represented by kernel density estimates or the empirical density function, closely related to histograms. Likewise, we plotted the hazard function estimate $\hat{\lambda}(t_i)$. Here, however, for each of these functions $\hat{R}(t_i)$, $\hat{F}(t_i)$, $\hat{f}(t_i)$, and $\hat{\lambda}(t_i)$, we each point and connect them with line segments. Figure 25.4 $\hat{R}(t_i)$, $\hat{F}(t_i)$, $\hat{f}(t_i)$, and $\hat{\lambda}(t_i)$.

![](img/2d145051bb14a0cdf0eb5048614ab_554_0.png)

**Figure 25.4** $\hat{R}(t_i)$, $\hat{F}(t_i)$, $\hat{f}(t_i)$ and $\hat{\lambda}(t_i)$ - Ungrouped Complete Data.

Assume one is interested in estimating the reliability at $t_j$, where $t_j$ is not a failure time recorded and $t_i < t_j < t_{i+1}$. Consider $t_i$ and $t_{i+1}$ are failure time during the observation. One of the simplest approaches is adopting a linear interpolation between

# Lifetime Data Analysis

# 539 the points $(t_i, \hat{R}(t_i))$ and $(t_{i+1}, \hat{R}(t_{i+1}))$, and estimating $R(t_j)$ by

```
\hat{R}(t_j) = a \times t_j + b, \quad (25.2.14)
```

such that

```
a = \frac{\hat{R}(t_{i+1}) - \hat{R}(t_i)}{t_{i+1} - t_i}, \quad (25.2.15)
```

```
b = \hat{R}(t_i) - a \times t_i, \quad (25.2.16)
```

Other interpolation or regression methods (see Section 6.7) may also be applied and provide more accurate estimates [316, 357].

**Example 25.2.2.** Consider the lifetime data set up in 25.2. Assume we need to estimate the reliability at $t_j = 2200h$. This value is recorded in the table. It is worth noting that $2187.52h < t_j < 2260.55h$. Here, an alternative is estimating the reliability using Function 25.2.14.

# 25.2.2 GROUPED COMPLETE DATA METHOD Assume the set of computers in a reliability test specifies that an inspection should be carried out every day to find failed computers. Therefore, the failure times are placed in intervals of twenty-four hours. A sort of failure data is grouped, as already mentioned at the beginning of the chapter. This introduces a method for lifetime analysis of grouped and complete data; that is, the time of failure of the computers is not lost, and the time to failure of every computer in the test is available.

Now the observation time was subdivided into intervals, where $t_1, t_2, ..., t_k$ are the times that represent the end of the respective time interval. Hence, $t_1 < t_2 < ... < t_k$. Let $n$ be the number of observed computers at the beginning of the test, and $n_i$ be the number of surviving computers at the end of interval $i$, $i \in \{1, 2, 3, ..., k\}$ (see Figure 25.5). Therefore, the reliability estimate at $t_i$ can be calculated through

```
\hat{R}(t_i) = \frac{n_i}{n}, \quad (25.2.17)
```
