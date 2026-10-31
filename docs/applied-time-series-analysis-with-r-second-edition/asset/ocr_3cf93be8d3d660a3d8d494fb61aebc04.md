![](bbox=[0.1, 0.07, 0.9, 0.65])

# FIGURE 8A.5

(a) True autocorrelations. (b) Sample autocorrelations. (c) True partial autocorrelations. (d) Sample partial autocorrelations. Plots (a) and (c) are based on the ARMA(4,3) model in Equation 8A.11.

# 8A.4 Generalized Partial Autocorrelations

One major concern with the Box–Jenkins approach in the case of an ARMA(p,q) with both p > 0 and q > 0 is that there is uncertainty concerning model selection even when examining the true autocorrelations and partial autocorrelations. The failure of the true autocorrelation and partial autocorrelation functions to uniquely identify p and q in a mixed ARMA(p,q) model as discussed above led Woodward and Gray (1981) to define the generalized partial autocorrelation in order to better handle the mixed process. Let X_t be a stationary process with autocorrelations ρ_j, j = 0, ±1, ±2, …, and consider the following k × k system of equations: