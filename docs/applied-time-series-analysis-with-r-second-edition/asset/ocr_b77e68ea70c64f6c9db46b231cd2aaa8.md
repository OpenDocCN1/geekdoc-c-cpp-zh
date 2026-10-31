order p to be 6, 8, and 10.

2. We next consider the near-nonstationary AR(3) model

(1 − 0.8B)(1 − 1.6B + 0.995B²)X_t = a_t,  (8.13)

where σ_a² = 1. Model in Equation 8.13 is nearly nonstationary because of two complex roots close to the unit circle (associated with the factor 1 − 1.6B + 0.995B²). In Figure 8.4a, we show a realization of length n = 200 from this model (data set fig8.4a in tswge). The sample autocorrelations in Figure 8.4b show a slowly damping sinusoidal behavior.

# Table 8.1

Factor Table for Overfit AR(k) Models Fit to the AR(3) Realization in Figure 8.3a

| AR Factors | Roots ($r_j$) | $|r_j^{-1}|$ | $f_{0j}$ |
|---|---|---|---|
| $k = 6$ |  |  |  |
| $1 - 0.98B$ | 1.02 | 0.98 | 0 |
| $1 - 1.17B + 0.77B^2$ | $0.76 + 0.85i$ | 0.88 | 0.13 |
| $1 + 0.58B + 0.21B^2$ | $-1.40 + 1.71i$ | 0.46 | 0.36 |
| $1 - 0.42B$ | 2.36 | 0.42 | 0 |
| $k = 8$ |  |  |  |
| $1 - 0.98B$ | 1.02 | 0.98 | 0 |
| $1 - 1.14B + 0.77B^2$ | $0.74 + 0.87i$ | 0.88 | 0.14 |
| $1 + 0.43 + 0.44B^2$ | $-0.49 + 1.43i$ | 0.66 | 0.30 |
| $1 - 1.05B + 0.35B^2$ | $1.48 + 0.80i$ | 0.60 | 0.08 |
| $1 + 0.56B$ | $-1.80$ | 0.56 | 0.5 |
| $k = 10$ |  |  |  |
| $1 - 0.98B$ | 1.02 | 0.98 | 0 |
| $1 - 0.95B + 0.71B^2$ | $0.66 + 0.99i$ | 0.85 | 0.16 |
| $1 - 1.26B + 0.70B^2$ | $0.89 + 0.79i$ | 0.84 | 0.12 |
| $1 + 0.43B + 0.66B^2$ | $-0.32 + 1.19i$ | 0.81 | 0.29 |
| $1 - 0.77$ | 1.31 | 0.77 | 0 |
| $1 + 1.34B + 0.55B^2$ | $-1.21 + 0.58i$ | 0.74 | 0.43 |

The strong cyclic behavior in the realization and the slowly damping sinusoidal sample autocorrelations are indications of nonstationarity or near-nonstationarity due to complex roots close to the unit circle. Table 8.2 shows