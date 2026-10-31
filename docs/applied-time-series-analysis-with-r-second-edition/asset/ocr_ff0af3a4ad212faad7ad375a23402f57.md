autocorrelations have a damped exponential behavior given by ρ_k = 0.3(0.95^k), so that even at small lags, the correlation is not substantial. In the realization in Figure 3.23a, there is some indication of a wandering behavior but with much less attraction between adjacent or near adjacent values. The spectral density in Figure 3.23c is plotted on the same scale as Figure 3.6a to emphasize that although the spectral density for this ARMA(1,1) model has a maximum at f = 0, there is much less power concentrated around the frequency f = 0. In fact, the realization, autocorrelations, and spectral density in Figure 3.23 are approaching the corresponding behaviors of white noise, demonstrating the fact that the MA term in Equation 3.90 has nearly canceled the effect of the AR operator. Clearly, as θ₁ → 0.95, the ARMA(1,1) model (1 − 0.95B)X_t = (1 − θ₁)a_t approaches white noise.

![](bbox=[0.35, 0.48, 0.65, 0.68])

![](bbox=[0.15, 0.68, 0.48, 0.88])

![](bbox=[0.5, 0.68, 0.8, 0.88])

# FIGURE 3.23

(a) Realization, (b) autocorrelations, and (c) spectral densities for the ARMA(1,1) model (1 − 0.95B)X_t = (1 − 0.8B)a_t.