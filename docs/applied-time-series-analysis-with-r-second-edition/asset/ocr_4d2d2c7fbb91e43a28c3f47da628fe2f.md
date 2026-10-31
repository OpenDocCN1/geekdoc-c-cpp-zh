considerable attention in the engineering and geophysical literature at least partially due to their need to either estimate parameters in real time, to obtain estimates for a large collection of time series, or for time series of several thousand points. In Section 7.2, we discuss techniques for obtaining preliminary estimates of the model parameters, and, then, in Section 7.3, we discuss ML estimation. Section 7.4 discusses the topic of estimating σ_a^2 and describes backcasting. Section 7.5 gives asymptotic properties, Section 7.6 provides some example applications and comparisons of estimation methods, and Section 7.7 discusses ARMA spectral estimation.

# 7.2 Preliminary Estimates

In this section, we discuss techniques for obtaining preliminary estimates of the parameters of AR(p), MA(q), and ARMA(p,q) models.

# 7.2.1 Preliminary Estimates for AR(p) Models

We consider the problem of estimating the parameters of the AR(p) model

X_t - μ - φ1(X_{t-1} - μ) - ... - φp(X_{t-p} - μ) = a_t,  (7.2)

where p is assumed to be known. We focus here on Yule–Walker (YW), least squares, and Burg estimates.

# 7.2.1.1 Yule–Walker Estimates

As the name suggests, the YW estimates are based on the YW equations in Equation 3.41. In particular, recall that the autocorrelation, ρ_k, of a stationary AR(p) process satisfies the difference equation

ρ_k = φ1 ρ_{k-1} + ... + φp ρ_{k-p},  (7.3)

for k > 0. Letting k = 1,2, ..., p in Equation 7.3 yields the YW equations:

(7.4)