2. Since the log-lynx data have a period of about 10 years, we focus our grid search for u in a neighborhood of 2π cos(0.10) = 0.8. Using est.garma.wge and letting u range from 0.4 to 0.12 in increments of 0.01, letting λ range from 0 to 0.5 in increments of 0.01, and letting p range from 0 to 3, and setting q = 0, we obtain the model

(1 − 0.51B)(1 − 2 × 0.796 + B²)^{0.4}(X_t − 2.9036) = a_t,

where σ_a² = 0.045 See Appendix 11A for further details about est.garma.wge.

# 11.6 Forecasting Based on the k-Factor GARMA Model

In this section we consider the problem of forecasting using the k-factor GARMA model. While the use of the difference equation provides easy-to-use forecasts in the case of the ARMA and ARUMA models using Equations 6.24 and 6.36, respectively, this method is not suitable for GARMA processes because there is no finite-order difference equation form for ∏_{j=1}^k (1 − 2u_j B + B²)^{λ_j}.

Brockwell and Davis (1991) use the π-weights version of the classical Box-Jenkins forecasts (see Section 6.4) to forecast the FARMA process φ(B)(1 − B)^d (X_t − μ) = θ(B)a_t, and Woodward et al. (1998) use this method for forecasting based on a k-factor GARMA model. The π-weights of the k-factor GARMA model can be calculated using the identity