# Lifetime Data Analysis

**Example 25.2.3.** Fifty servers ($n = 50$) were placed in an accelerated reliability test. The test protocol specifies that an inspection should be carried out every $400h$. The test finished when every server failed. Table 25.3 shows the time intervals (Column $t_i$)

Table 25.3

| $t_i$ | $n_{i-1}$ | $n_i$ | $R(t_i)$ | $\hat{F}(t_i)$ | $\hat{f}(t_i)$ | $\hat{\lambda}(t_i)$ |
|---|---|---|---|---|---|--|
| 0 | Used | 50 | 1.0000 | 0.0000 | 0.0009 | 0.0009 |
| 400 | 17 | 33 | 0.6660 | 0.3400 | 0.0004 | 0.0005 |
| 800 | 7 | 26 | 0.5200 | 0.4800 | 0.0003 | 0.0005 |
| 1200 | 5 | 21 | 0.4200 | 0.5800 | 0.0002 | 0.0005 |
| 1600 | 4 | 17 | 0.3400 | 0.6600 | 0.0002 | 0.0004 |
| 2000 | 3 | 14 | 0.2800 | 0.7200 | 0.0003 | 0.0011 |
| 2400 | 6 | 8 | 0.1600 | 0.8400 | 0.0001 | 0.0003 |
| 2800 | 1 | 7 | 0.1400 | 0.8600 | 0.0001 | 0.0007 |
| 3200 | 2 | 5 | 0.1000 | 0.9000 | 0.0001 | 0.0010 |
| 3600 | 2 | 3 | 0.0600 | 0.9400 | 0.0001 | 0.0008 |
| 4000 | 1 | 2 | 0.0400 | 0.9600 | 0.0000 | 0.0000 |
| 4400 | 0 | 2 | 0.0400 | 0.9600 | 0.0001 | 0.0013 |
| 4800 | 1 | 1 | 0.0200 | 0.9800 | 0.0000 | 0.0000 |
| 5200 | 0 | 1 | 0.0200 | 0.9800 | 0.0000 | 0.0000 |
| 5600 | 0 | 1 | 0.0200 | 0.9800 | 0.0000 | 0.0000 |
| 6000 | 0 | 1 | 0.0200 | 0.9800 | 0.0000 | 0.0000 |
| 6400 | 0 | 1 | 0.0200 | 0.9800 | 0.0000 | 0.0000 |
| 6800 | 0 | 1 | 0.0200 | 0.9800 | 0.0000 | 0.0000 |
| 7200 | 0 | 1 | 0.0200 | 0.9800 | 0.0000 | 0.0000 |
| 7600 | 0 | 1 | 0.0200 | 0.9800 | 0.0001 | 0.0025 |
| 8000 | 1 | 0 | 0.0000 | 1.0000 | 0.0000 | Not used |

# Grouped Complete Lifetime Data

The reliability at $t_i = 2000$ is estimated as $\hat{R}(2000) = 0.28$. Then, the cumulative time distribution of the $TTFs$ at $t_i = 2000$ is $\hat{F}(2000) = 0.72$. The $MTTF = 1368h$. Adopting bootstrap, a confidence interval for the $MTTF$ was estimated. The sample used to perform the resampling was a multiset of $TTFs$ with the midpoint, $	ilde{t}_i$, where each interval $i$ is repeated $n_{i-1}-n_i, n_i-n_{i-1}$ is the number of failures in each interval. The original sample from which the resamples are obtained is shown in Table 25.4. Applying nonparametric bootstrap, one thousand