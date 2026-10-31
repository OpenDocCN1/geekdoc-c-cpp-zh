depends on time, and the random walk process does not satisfy the stationarity conditions for either variance or autocorrelations. The impact of Equations 5.22 through 5.24 on realizations is that the variability increases with time while simultaneously the autocorrelation between X_t and X_{t+k}, for fixed k, increases as t increases. Figure 5.6a shows a realization of length n = 200 from a random walk model with σ_a^2 = 1. The random progression in time is apparent along with the tendency for the variability to increase as t increases.

![](bbox=[0.18, 0.3, 0.82, 0.6])

# FIGURE 5.6

Realizations from (a) random walk and (b) random walk with drift models.

# 5.4.2 Random Walk with Drift

An extension of the model in Equation 5.20 is the random walk with drift model given by

X_t = α + X_{t-1} + a_t, (5.25)

where α is a nonzero constant called the drift, and again X_0 = 0. Based on model in Equation 5.25, at time t − 1, the movement to time t is α plus the random a_t. It follows that E(X_t) = αt, and, thus, the process mean increases or decreases in time depending upon whether α is positive or negative, respectively. Figure 5.6b displays a realization of length n = 200 for a random walk with drift α = 0.1 and σ_a^2 = 1 using the same random sequence a_1, a_2, ..., a_200 that was used in Figure 5.6a. The upward drift is evident.