![](bbox=[0.408, 0.091, 0.79, 0.42])

# FIGURE 3.16

(a) Realization, (b) autocorrelations, and (c) spectral densities for the AR(3) model $(1 - 0.95B)(1 - 1.6B + 0.9B^2)X_t = a_t$.

# EXAMPLE 3.9: AN AR(3) MODEL WITH A NEGATIVE REAL ROOT AND COMPLEX CONJUGATE ROOTS

In Figure 3.17, we show a realization, where $\sigma_a^2 = 1$, true autocorrelations, and the true spectral density for the AR(3) model

$X_t - 0.65X_{t-1} - 0.62X_{t-2} + 0.855X_{t-3} = a_t,$ \qquad (3.75)

which can be written in factored form as $(1 + 0.95B)(1 - 1.6B + 0.9B^2)X_t = a_t$. The factored form of the model in Equation 3.75 has the same second-order factor that was in model (3.73) with the difference being that the characteristic equation associated with Equation 3.75 has a negative real root $r_1 = 1/(-0.95) = -1.05$. Again, from the discussion of AR(1) and AR(2) models, we know that an AR(1) model based on the first-order factor $1 + 0.95B$ has: (a) realizations that display a rapidly oscillating behavior as seen in Figure 3.5b, (b) autocorrelations that are oscillating damped exponentials as in Figure 3.4b, and (c) a peak in the spectral density at