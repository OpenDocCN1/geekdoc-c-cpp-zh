542 Performance, Reliability, and Availability of Computational Systems

# Table 25.4
Grouped TTFs - Replicated Interval's Midtimes

| | | | | |
| 200 | 200 | 600 | 1400 | 2200 |
| 200 | 200 | 600 | 1400 | 2200 |
| 200 | 200 | 600 | 1400 | 2600 |
| 200 | 200 | 600 | 1800 | 3000 |
| 200 | 200 | 1000 | 1800 | 3000 |
| 200 | 200 | 1000 | 1800 | 3400 |
| 200 | 200 | 1000 | 2200 | 3400 |
| 200 | 600 | 1000 | 2200 | 3800 |
| 200 | 600 | 1000 | 2200 | 4600 |
| 200 | 600 | 1400 | 2200 | 7800 |

resamples were generated, and the respective resamples' were computed and ordered. After, the quantiles 25% and 97.5% were selected to obtain a confidence interval of the MTTF, considering 95% degree of confidence. The obtained interval was MTTF $\in (100h, 1800h)$.

The reliability at $t = 2100h$ can be interpolated using $\hat{R}(t) = -3 	imes 10^{-4}t + 0.88$, which is the line equation for interpolating between points $(2000h, 0.28)$ and $(2400h, 0.16)$. Therefore, $\hat{R}(2000h) = 0.25$. Figure 25.6 shows the graphs $\hat{R}(t) 	imes t$, $\hat{F}(t) 	imes t$, $\hat{f}(t) 	imes t$, and $\hat{\lambda}(t) 	imes t$.

# 25.2.3 UNGROUPED MULTIPLY CENSORED DATA METHOD

This section presents a method for reliability analysis of ungrouped multiply data. Let $n$ be the number of devices, as servers, switches, which were observed. During the observation period, a device may either fail or censored at any moment. Figure 25.7 shows an observation timeline in which the failure or censored times are represented. It is worth stressing that the data set is ungrouped; here, the times between events (failure or censoring) vary.

The probability of a device failure occurs after $t_i$, given it not failed by $t_{i-1}$, is

```
$P(T > t_i|T > t_{i-1}) = \frac{P((T > t_i) \cap (T > t_{i-1}))}{P(T > t_{i-1})}\nP(T > t_i|T > t_{i-1}) = \frac{P(T > t_i)}{P(T > t_{i-1})}\nP(T > t_i|T > t_{i-1}) = \frac{R(t_i)}{R(t_{i-1})}$
```