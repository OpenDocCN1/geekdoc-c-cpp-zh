# Lifetime Data Analysis

601

# Table 25.26

Time to Failure Exponentially Distributed with Right-Censoring Type 2

| i | $\delta$ | TTF ($h$) | $\delta$ | TTF ($h$) | $\delta$ | TTF ($h$) | $\delta$ | TTF ($h$) |
|---|---|---|---|---|---|---|---||}{
| 1 | 1 | 31.32 | 0 | 1 | 2564.12 | 0 | 1 | 346.96 | 0 | 1 | 3432.90 |
| 2 | 1 | 91.00 | 0 | 907.43 | 0 | 1 | 353.41 | 1 | 1481.06 | 0 | 3666.17 |
| 3 | 1 | 131.81 | 0 | | 1 | 368.63 | 0 | 1 | 1739.20 | |
| 4 | 1 | 139.65 | 1 | 1002.30 | 0 | | 1 | 1770.10 | 0 |
| 5 | 1 | 159.92 | 0 | 1 | 2700.43 | 0 | 1 | 1957.75 | 1 | 5159.89 |
| 6 | 1 | 160.95 | 1 | 1095.70 | 0 | 1 | 671.81 | 1 | 1966.66 | 0 |
| 7 | 0 | | 1199.17 | 1 | 2829.03 | 0 | | | |
| 8 | 1 | 246.19 | 1 | 2947.40 | 0 | 1 | 2106.44 | 1 | 7455.63 |
| 9 | 1 | 247.87 | 0 | 2985.47 | 0 | | 1 | 2245.22 | 1 | 12377.70 |
| 10 | 1 | 302.91 | 1 | 3260.55 | 0 | | | | |
| j | | | 2 | 3 | 4 | 5 | 6 |

![](bbox=[0.147, 0.439, 0.852, 0.532])

$\lambda = (1.11 \times 10^{-4} h^{-1}, 1.85 \times 10^{-4} h^{-1})$

and

![](bbox=[0.118, 0.566, 0.882, 0.663])

$MTTF = \frac{5406.07}{898.57}$

If $T$ is the time to repair, the method introduced above provides the confidence intervals for the mean time to repair (MTTR) and for the repair rate ($\mu$).

# Confidence Interval for Availability - TTF and TTR Exponentially Distributed

This section presents a parametric method for estimating the confidence interval for availability when assuming the time to failure (TTF) and time to repair (TTR) are exponentially distributed [207].

The steady-state availability is defined (as Equation 16.2.18) as

![](bbox=[0.388, 0.874, 0.612, 0.915])