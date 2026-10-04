
# ARMA Time Series Models

Using R: For a given AR(p) model, you can obtain a factor table using the tswge factor.wge. This function will factor an m order polynomial into its first order and irreducible second order factors. Again, be-full with the signs. See Appendix 3B for more details.

## EXAMPLE 3.12: AN AR(4) MODEL

Consider the AR(4) process given by

```
$X_i - 1.15X_{i-1} + 0.19X_{i-2} + 0.64X_{i-3} - 0.61X_{i-4} = a_i.$
```

Although inspecting the coefficients in Equation 3.81 tells us nothing about the nature of the model, much can be learned by examining the factors. The characteristic polynomial can be factored

```
$\phi(z) = 1 - 1.15z + 0.19z^2 + 0.64z^3 - 0.61z^4$
$= (1-0.95z)(1-z+0.8z^2)$
```

Information concerning the factors of $\phi(z)$ is given in the factor table Table 3.3. Since $|r_1|<1$ for all roots, the model is causal and stationary. The factor table shows a complex pair of roots. The positive root is associated with damped exponential autocorrelations, wandering behavior in the realizations, and a peak in the spectral density at $f=0$. The negative root produces oscillating damped autocorrelations, oscillating behavior in realizations, and a peak in the spectral density at $f=0.5$. The complex conjugate roots are related to damped sinusoidal behavior in the autocorrelations with a system frequency (using Equation 3.63) of $f=0.16$, pseudo-periodic behavior in the data with periods of about 6 (i.e., 1/0.6), and a peak in the spectral density at $f=0.16$.

In Figure 3.18, we show a realization of length $n=200$ where $\sigma_\epsilon^2=1$, autocorrelations, and the spectral density for the AR(4) model in Equation 3.8. The realization in Figure 3.18a is stored in data set

### TABLE 3.3
Factor Table for the AR(4) Model in Example 3.12

| AR Factors | $|r_1|$ | $f_{sj}$ |
|---|---|---|
| $1 - 0.95B$ | 0.95 | 0 |
| $1 - 0.8B^2$ | $0.62 \pm 0.93i$ | 0.90 | 0.16 |
| $1 + 0.8B$ | $-1.25$ | 0.80 | 0.5 |

# 126 Applied Time Series Analysis with R

![](img/41dcbfb9af56fa48895afde322197b0b_142_0.png)

Figure 3.18

(a) Realization, (b) autocorrelations, and (c) spectral densities of the AR(4) model $X_{t}-1.15X_{t-1}+0.19X_{t-2}+0.64X_{t-3}=(1-0.95B)(1-B+0.8B^2)X_{t}=a_{t}$, in Example 3.12.

fig318a in tswge. The autocorrelations have a sinusoidal appearance (with period around 6) along a damped exponential path with very little evidence of the 0.5 frequency behavior associated with the factor (1+0.8B). The realization shows pseudo-cyclic behavior of period produced by the factor $(1-B+0.8B^2)$ along a wandering path produced by the 1. The realization shows very slight evidence of the high-frequency behavior associated with the factor $1+0.8B$. The spectral density peaks at $f=0, 0.16,$ and 0.5 as would be expected based on the factor.

NOTE: It is very important to realize that the behavior associated with roots closest to the unit circle tends to be dominant. In this example, the root 1.05 associated with the factor $(1-0.95B)$ is closest to the unit circle while the root -1.25 associated with $(1+0.8B)$ is the furthest removed from the unit circle. We have already noted that the behavior associated with the factor $1-0.95$ is clearly evident in the realization and the autocorrelations while that associated with $1+0.8B$ is not apparent. In the spectral density, we see peaks close to all three system frequencies, the peak at $f=0$ is much higher than the peak at $f=0.5$ and $f=0.16$. We will explore the domination of roots close to the unit circle further in Example 3.14 and in Chapter 5.

# ARMA Time Series Models

### EXAMPLE 3.13: AN AR(4) MODEL WITH ALL ROOTS COMPLEX
We consider the AR(4) model

```
$X_t - 0.3X_{t-1} - 0.9X_{t-2} - 0.1X_{t-3} + 0.8X_{t-4} = a_t,$
```

whose factor table is given in Table 3.4. In the factor table, it can be seen that the characteristic equation has pairs of conjugate roots, one associated with a system frequency of $f=0.06$ and the other with a frequency of $f=0.4$. It can also be seen that the roots with $f=0.06$ are closer to the unit circle. Thus, the realizations pseudo-periodic behavior with a more dominant period of about 17 (1/0.06) and a higher frequency component with period of about 2.5 (1/0.4). We also expect two peaks in the spectral density, at $f=0.06$ and $f=0.4$ as expected.

In Figure 3.19, we show a realization of length $n=200$, where $\sigma_a^2=1$, the autocorrelations, and the spectral density for the AR(4) model in this example has the anticipated pseudo-periodic behavior with a period of about 17 and a high-frequency component. There are peaks in the spectral density at $f=0.06$ and $f=0.4$ as expected. The autocorrelation is a damped sinusoidal with a period of about 17 with a slight indication of the higher frequency behavior. Again, we see that the spectral density and the factor table give a much clearer picture of the periodic behavior.

### EXAMPLE 3.14: DOMINANCE OF ROOTS NEAR
THE UNIT CIRCLE

In this example, we return to the AR(3) model in Example 3.8. We first consider the AR(3) models

```
$(1-0.95B)(1-1.6B-\lambda_2B^2)X_t = a_t,$
```

$\lambda_2=-0.7, -0.9$ (as in Example 3.8), and $-0.98$. We do not show the factor tables for these three roots, but it should be noted that $|r_1|=0.95$ for the real root. More completely, for $\lambda_2=-0.7, -0.9$ the complex roots have $|r_1|=0.84, 0.9$, and 0.99, respectively. Thus, the complex roots and real root are all close to the unit circle when $\lambda_2=-0.9$; however, when $\lambda_2=-0.7$, the real root is closer to the unit circle than the complex roots, and when $\lambda_2=-0.98$, the complex roots are closer. So, based on the discussion preceding Example 3.13, we expect the real root to dominate the cyclic behavior when $\lambda_2=-0.7$, and we expect the

### TABLE 3.4

| AR Factors | Roots ($r_j$) | $|r_1|$ | $f_{ij}$ |
|---|---|---|---|
| $1-1.8B+0.95B^2$ | $0.95 \pm 0.39i$ | 0.97 | 0.06 |
| $1+1.5B+0.85B^2$ | $-0.89 \pm 0.63i$ | 0.92 | 0.4 |

# Applied Time Series Analysis with R

![](img/41dcbfb9af56fa48895afde322197b0b_144_0.png)

FIGURE 3.19

+   (a) Realization, (b) autocorrelations, and (c) spectral densities for the AR(4) model $(1 – 1.8B + 0.95B^2)X_t = a_r$.

cyclic behavior with the complex roots overshoots the real root introduced wandering when $\lambda_2 = -0.98$. In Figures 3.20 through 3.22, we show autocorrelations, realizations (based on $\sigma_{\epsilon}^2=1$), and spectral densities for these three models. Figures 3.20b, 3.21b, and 3.22b are in which case the behavior imposed on the realization, autocorrelations, and spectral density by both the real and complex roots is clearly visible. However, in Figures 3.20a, 3.21a, and 3.22a, it is a damped exponential with very little indication of the cyclic behavior. The realizations have a wandering behavior with only a very mild pseudo-periodic behavior, and the peak at $f=0$ dominates the spectral density. Correspondingly, in Figures 3.20c, 3.21c, and 3.22c, we observe that when $\lambda_2 = -0.98$, the autocorrelations look like a damped sinusoidal with very little detectable damped exponential appearance, the realization has a distinct pseudo-periodic behavior with only a mild tendency to wander, while the peak at $f=0.1$ is the most dominant peak in the spectral density although the peak at $f=0$ is visible.

It is clear from Example 3.14 that the behavior of an AR process can be traced to its dominant factors, that is, closest to the unit circle.

# ARMA Time Series Models

![](img/41dcbfb9af56fa48895afde322197b0b_145_0.png)

![](img/41dcbfb9af56fa48895afde322197b0b_145_1.png)

**FIGURE 3.20**
Autocorrelations for the AR(3) models $(1 - 0.95B)(1 - 1.6B - \lambda_2B^2)X_t = a_r (a - c)$ $\lambda_2 = -0.7, -0.9, -0.98$.

![](img/41dcbfb9af56fa48895afde322197b0b_145_2.png)

![](img/41dcbfb9af56fa48895afde322197b0b_145_3.png)

**FIGURE 3.21**
Realizations from the AR(3) models $(1 - 0.95B)(1 - 1.6B - \lambda_2B^2)X_t = a_u (a - c)$ $\lambda_2 = -0.7, -0.9, -0.98$.
