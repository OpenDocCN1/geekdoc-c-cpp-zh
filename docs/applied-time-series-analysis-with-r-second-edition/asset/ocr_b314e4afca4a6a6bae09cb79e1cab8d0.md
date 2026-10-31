+   ii. What is the major difference between the two models concerning this periodic component?

+   iii. Based on these plots, which model appears to be the better model for the sunspot data? (Clearly neither model accounts for the fact that there is more variability in the peaks than the troughs. Ignoring this problem that both models have, which seems better and why?)

# 3.13 Generate realizations of length n = 100 from the following stationary AR(p) models

+   i. $(1 - 2.2B + 2.1B^2 - 0.8B^3)X_t = a_t$
+   ii. $(1 - 0.42B - 0.34B^2 + 0.91B^3)X_t = a_t$
+   iii. $(1 - 2.09B + 2.56B^2 - 1.96B^3 + 0.88B^4)X_t = a_t$

For each of these realizations

+   a. Plot the realization along with the additive AR components (see Section 3.4).
+   b. Discuss your results relating each additive component to one of the lines in the factor table.

**NOTE:** To best visualize the contribution of each component, use the same vertical scale on each of the plots associated with a given realization.

3.14 Use tswge function factor.comp.wge to fit an AR(8) model to the sunspot data in sunspot.classic. Create the factor table and the additive AR components obtained from factor.comp.wge and plot the data along with the first four components. Discuss the contributions of each component.

# Theoretical Problems

3.15 Show that the function $f(u) = |u| / (1 + u^2)$ has a maximum of 0.5, and thus for an MA(1) process, max$|\rho_1|$ = 0.5.

3.16 a. For an MA(2), show that $|\rho_2| \le 0.5$.
b. For an MA(q) process, show that $|\rho_q| < 0.5$.

3.17 Let $X_t$ be a stationary zero-mean time series and define $Y_t = X_t - 0.4X_{t-1}$ and $W_t = X_t - 2.5X_{t-1}$. Express the autocovariance and autocorrelation functions of $Y_t$ and $W_t$ in terms of the autocovariance function of $X_t$, and show that $Y_t$ and $W_t$ have the same autocorrelations but that their autocovariance functions differ.