![](bbox=[0.218, 0.089, 0.786, 0.446])

# **FIGURE 1.3**

Four realizations from stationary processes. (a) Realization 1. (b) Realization 2. (c) Realization 3. (d) Realization 4.

Realization 2 in [Figure 1.3b] shows an absence of pattern. That is, there appears to be no relationship between $X_t$ and $X_{t+1}$ or between $X_t$ and $X_{t+k}$ for any $k \ne 0$ for that matter. In fact, this is a realization from a white noise model, and, for this model, $\rho_k = 0$ whenever $k \ne 0$ as can be seen in [Figure 1.4b]. Notice that in all autocorrelation plots, $\rho_0 = 1$.

Realization 3 in [Figure 1.3c] is characterized by pseudo-periodic behavior with a cycle-length of about 14 time points. The corresponding autocorrelations in [Figure 1.4c] show a damped sinusoidal behavior. Note that, not surprisingly, there is a positive correlation between $X_t$ and $X_{t+14}$. Also, there is a negative correlation at lag 7, since within the sinusoidal cycle, if $x_t$ is above the average, then $x_{t+7}$ would be expected to be below average and vice versa. Also note that due to the fact that there is only a pseudo-cyclic behavior in the realization, with some cycles a little longer than others, by lag 28 (i.e., two cycles), the autocorrelations are quite small.