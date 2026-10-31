![](bbox=[0.38, 0.1, 0.56, 0.27])

![](bbox=[0.15, 0.32, 0.45, 0.55])

![](bbox=[0.55, 0.32, 0.85, 0.55])

# FIGURE 3.28

(a) Realization, (b) autocorrelations, and (c) spectral densities for the seasonal model (1 − 0.8B⁴)X_t = a_t.

# TABLE 3.8

Factor Table for Seasonal Model (1 − 0.8B⁴)X_t = a_t

| AR Factor | Roots (r_j) | | r_j^{-1} | | f_0j |
|---|---|---|---|---|
| 1 - 0.95B | 1.06 | 0.95 | 0.00 |
| 1 + 0.95B | -1.06 | 0.95 | 0.50 |
| 1 + 0.89B² | ±1.06i | 0.95 | 0.25 |

**Using R:** A realization from the seasonal model in Equation 3.125, true autocorrelations, and spectral densities can be obtained using the tswge function plotts.true.wge discussed previously. In this case you would specify the model as an AR(4) with coefficients 0, 0, 0, and 0.8. Using these same AR(4) coefficients you can obtain a factor table for this seasonal model using factor.wge.

One feature of the model in Equation 3.125 that makes it less than ideal for practical situations is that there is very likely autocorrelation between adjacent or