# ARMA Time Series Models

139

![](bbox=[0.125, 0.121, 0.684, 0.487])

### FIGURE 3.24

(a) Realization, (b) autocorrelations, and (c) spectral densities for the ARMA(2,1) model $(1 - 1.6B + 0.9B^2)X_t = (1 - 0.8B)a_t$.

which can be factored as

> $(1 - 1.8B + 0.9B^2)(1 + 1.5B + 0.8B^2)X_t = (1 + 0.9B)(1 + 0.8B^2)a_t$. (3.95)

The factor table is shown in Table 3.7, and it should be noted that the AR factor is the one previously considered in the AR(4) model in Example 3.13. Figure 3.25 displays a realization of length $n = 200$ from the ARMA(4,3) model in Equations 3.94 and 3.95 with $\sigma_a^2 = 1$ along with the autocorrelations and spectral density. Comparing the spectral density

# TABLE 3.7

Factor Table for the ARMA(4,3) Model in Equations 3.94 and 3.95

| AR factors | Roots $(r_j)$ | $|r_j^{-1}|$ | $f_{uj}$ |
|---|---|---|-|
| $1 - 1.8B + 0.9B^2$ | $0.95 \pm 0.39i$ | 0.97 | 0.06 |
| $1 + 1.5B + 0.8B^2$ | $-0.89 \pm 0.63i$ | 0.92 | 0.04 |
| MA factors | | | |
| $1 + 0.9B$ | $-1.11$ | 0.9 | 0.50 |
| $1 + 0.8B^2$ | $\pm1.12i$ | 0.89 | 0.25 |