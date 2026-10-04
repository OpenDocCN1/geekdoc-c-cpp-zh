# Forecasting

and recalling that $\psi_j 	o 0$ as $j 	o \infty$ for a stationary model. We will return
to the topic of calculating residuals in Section 7.4.
Finally, using Equation 6.27, forecasts are calculated as

```
$\tilde{X}_{25}(1) = 1.2\tilde{X}_{25}(0) - 0.6\tilde{X}_{25}(-1) - 0.5\tilde{a}_{25} + 0.4\bar{X}$
$= 1.2\tilde{X}_{25} - 0.6\tilde{X}_{24} - 0.5\tilde{a}_{25} + 0.4\bar{X}$
$= 1.2(52.05) - 0.6(50.66) - 0.5(1.36) + 0.4(50.04)$
$= 51.40$,
$\tilde{X}_{25}(2) = 1.2\tilde{X}_{25}(1) - 0.6\tilde{X}_{25}(0) + 0.4\bar{X}$
$= 1.2(51.40) - 0.6(52.05) - 0.4(50.04)$
$= 50.46$,
:
```

The forecasts $\hat{X}_{25}(\ell)$, $\ell = 1, \dots, 4$ are given in Table 6.2 and $\hat{X}_{25}(\ell)$, $\ell = 1, \dots, 20$ are shown in Figure 6.2.

**Using R:** Forecasts for a given stationary ARMA models can be found using the twge function `fore.arma.wge` and specifying the series, the ARMA model parameters, the number of steps ahead to forecast, and other plotting options. See Appendix 6B.

# TABLE 6.2
Forecasts from $l_0 = 25$ for the Realization in Table 6.1

| $\ell$ | $\hat{X}_{25}(\ell)$ |
|---|---|
| 1 | 51.40 |
| 2 | 50.46 |
| 3 | 49.73 |
| 4 | 49.42 |

![](bbox=[0.187, 0.711, 0.812, 0.883])

**FIGURE 6.2**
Forecasts using the ARMA(2,1) model $(1 - 1.2B + 0.6B^2)(X - 50) = (1 - 0.5B)a_t$.