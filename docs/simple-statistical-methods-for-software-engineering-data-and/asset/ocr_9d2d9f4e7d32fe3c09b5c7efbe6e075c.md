# Standard Deviation

If we take the square root of the variance of bug fix time, we will obtain 11.190 days. This is the standard deviation, SD, of bug repair time, the most commonly used measure of dispersion. This is larger than the average absolute deviation.

> The standard deviation is always larger than the average absolute deviation.

The exact formula for standard deviation, SD, has a small correction for sample size. Instead of using n as the number of data points, the exact calculation uses n − 1, the degrees of freedom; that is,

```
SD = sqrt( sum_{i=1}^{n} (x - x̄)^2 / (n - 1) )  (3.3)
```

The corrected value of standard deviation for bug repair time is 11.284.

Process dispersion can be defined in terms of standard deviation, sigma. It is a tradition dating back to the 1920s to take process variation as ±3 sigma. The normal distribution beyond ±3 sigma is disregarded. Mathematically speaking, the normal distribution runs from minus infinity to plus infinity. We trim the tails and take the span from −3 sigma to +3 sigma as the process dispersion. The trimming rules are associated with confidence level. The ±3 sigma trimming rule is associated with a confidence level of 97.3%.

# BOX 3.3 THUMB RULES

With experience, people develop thumb rules about using dispersion measures. Although the rules depend on the individual person, here is an educative example. The following table shows three ways of applying dispersion.

| SNo | Purpose | Range Considered | Confidence Level |
|---|---|---|---|
| 1 | Business decisions | Interquartile | 50% |
| 2 | Process decisions | 3–97 percentile | 94% |
| 3 | Risk avoidance | Max–min | 100% |

Business decisions are customarily taken to accommodate IQR of variation. To accommodate more would need an unrealistic budget. Process decisions are made with expectations of reasonably stringent discipline. Risk avoidance involves understanding and accommodating extreme values. You can form your own rules of thumb to manage dispersion.