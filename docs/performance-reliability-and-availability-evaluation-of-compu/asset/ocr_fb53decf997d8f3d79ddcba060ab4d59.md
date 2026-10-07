# 620 Performance, Reliability, and Availability Evaluation of Computational Systems

and

```
$$\lambda_1 = \lambda_2 V_1^2 V_2^{-2}, \quad (26.1.11)$
```

```
$$\lambda_1 = \frac{1}{120h} \times 140V_2^2 \times 120V_2^{-2} = 1.944 \times 10^{-4}h^{-h}$.$
```

![](bbox=[0.858, 0.211, 0.878, 0.226])

# Regression

An alternative strategy is adopting curve fitting methods as those introduced in Section 6.7 to estimate parameters (failure rates, time to failure statistics, etc.) at several different high-stress levels, and then fitting the respective model, and extrapolating the found parameter values to the normal stress level. Hence, a strategy aims to find out trends that allow predictive analytic functions through the available data set to estimate failure parameters at normal operating conditions.

**Example 26.1.4.** Let us consider five samples of ten devices that were tested under distinct stress levels. The stress levels in the experiment accelerate the devices' failures by 10, 12, 14, 16, and 18. The whole experiment finished when every device of each sample failed. We assume the failure rate is constant for each stress level. The mean failure rate and the respective mean time to failure for each stress level are depicted in Table 26.2.

# Table 26.2

| s (stress level) | $\$\lambda$ (failure) | MTTF (h) |
|---|---||
| 10 | $$8.55 \times 10^{-3}$ | 116.98 |
| 12 | $$1.13 \times 10^{-2}$ | 88.31 |
| 14 | $$1.56 \times 10^{-2}$ | 64.15 |
| 16 | $$2.36 \times 10^{-2}$ | 42.42 |
| 18 | $$3.21 \times 10^{-2}$ | 31.13 |

Figure 26.3.a shows the set of points, each represented by $(s, \lambda(s))$, where $\$\lambda(s)$ is the mean failure rate, obtained from the sample evaluated considering the specific stress level, $s \in \{10, 12, 14, 16, 18\}$. Figure 26.3.b shows the set of points $\{(s, MTTF(s))\}$, where $MTTF(s)$ is the mean time to failure obtained from the sample evaluated at the stress level $s$.

Applying exponential regression (see Section 6.7.3) to the data set $\{(s, \lambda(s))\}$, we obtain

```
$$\lambda(s) = 1.4638 \times 10^{-3} e^{171.891 \times 10^{-3}} fph.$
```