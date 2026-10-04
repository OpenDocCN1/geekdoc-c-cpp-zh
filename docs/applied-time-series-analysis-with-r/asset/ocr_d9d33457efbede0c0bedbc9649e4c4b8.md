# Vector-Valued (Multivariate) Time Series

To find the correlation matrices $ho(k)$, we use the bivariate version of Equation 10.4 to yield

```
$$\rho(k) = \begin{pmatrix} \gamma_{11}^{1/2} & 0 \ 0 & \gamma_{22}^{1/2} \end{pmatrix} \Gamma(k) \begin{pmatrix} \gamma_{11}^{-1/2} & 0 \ 0 & \gamma_{22}^{-1/2} \end{pmatrix} $$
```

from which it follows that

```
$$\rho(0) = \begin{pmatrix} 1 & -0.02 \ -0.02 & 1 \end{pmatrix}, \rho(1) = \begin{pmatrix} 0.89 & -0.45 \ 0.39 & 0.71 \end{pmatrix}, \rho(2) = \begin{pmatrix} 0.62 & -0.71 \ 0.65 & 0.32 \end{pmatrix}$$
$$$\rho(3) = \begin{pmatrix} 0.26 & -0.06 \ 0.72 & -0.06 \end{pmatrix} \dots$$
```

From these matrices, it can be seen that the contemporaneous cross-correlation between $X_1$ and $X_2$ ($ho_{12}(0) = -0.02$), there is substantial cross-correlation at lags 1, 2, and 3. Figure 10.4a and b show the autocorrelations for $X_1$ and $X_2$, respectively, where it can be seen that the autocorrelations reflect a sinusoidal wave with period around 14 for $X_1$ and $X_2$. The cross-correlations in Figure 10.4c show that while there is very contemporaneous correlation, the cross-correlations, $\gamma_{ij}(k)$, for $k=1$ through 5 are more substantial (and negative) for $k=-1$ to $-5$, the cross-correlations are positive.

This relationship between $X_1$ and $X_2$ is not easy to visualize from the realizations in Figure 10.3. In Figure 10.5a, we show the two very realizations in Figure 10.3 overlaid, and it is seen that there is very little contemporaneous correlation between $X_1$ and $X_2$ which is consistent with the fact that $ho_{12}(0) = -0.02$. From Figure 10.4c, we see that the maximum value for $ho_{12}(k)$ occurs at $k=-3$. Figure 10.5b shows overlays of $X_1$ and $X_{1-3}$, where it is seen that the resulting curves are positively correlated, that is, they reach their cyclic peaks and troughs together. Correspondingly, in Figure 10.5c, we show overlays of $X_{1}$ and $X_{1-3,2}$, which reveal a negative correlation that is consistent with the fact that $ho_{12}(3) = -0.76$.

# Definition 10.7

Let $X_t$ be a stationary multivariate process that satisfies

```
$$\mathbf{X}_t - \Phi_1 \mathbf{X}_{t-1} - \dots - \Phi_p \mathbf{X}_{t-p} = \alpha + \mathbf{a}_t - \Theta_1 \mathbf{a}_{t-1} - \dots - \Theta_q \mathbf{a}_{t-q} $$
```

where $\Phi_s$ and $\Theta_s$ are real-valued $m 	imes m$ matrices, and $\mathbf{a}_t$ is multivariate white noise. Then, $X_t$ is a VARMA$(p,q)$ process.