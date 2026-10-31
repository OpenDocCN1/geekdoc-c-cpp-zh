# 7.6 Estimation Examples Using Data

In this section, we will use realizations discussed in Chapters 3 and 5 from known models to illustrate some of the concepts of this chapter.

**Using R:** As mentioned earlier, to obtain YW, Burg, or ML estimates of AR(p) parameters you can use `est.ar.wge`. To obtain ML estimates of ARMA model parameters use the `tswge` function `est.arma.wge`. The output contains the parameter estimates, residuals (using backcasting), white noise variance estimate obtained from the backcast residuals, and the standard errors for the parameter estimates.

# EXAMPLE 7.8: ESTIMATING PARAMETERS IN MA(q) MODELS

We consider the realization of length n = 100 in Figure 3.1a from the MA(1) model X_t = (1 - 0.99B)a_t. In this case θ_1 = 0.99 and σ_a^2 = 1. The MA characteristic equation has its root (1/0.99) very close to the noninvertible region. Using the `itsmr` function ia to calculate innovations estimates, the estimate is θ̂_1 = 0.8 with σ̂_a^2 = 0.97 while the MLE is θ̂_1 = 0.8 with σ̂_a^2 = 0.94 We see that in each case, the parameter is underestimated. It should be noted that the MM estimate does not exist because ρ̂_1 = -0.54 See Example 7.1. As previously mentioned, we do not recommend the MM estimates for MA(q) models.

We revisit a few of the AR(p) examples considered in Chapters 3 and 5. As mentioned earlier, the methods (YW, Burg, and MLE) all behave similarly asymptotically, but for AR(p) models with roots close to the nonstationary region, the YW estimates do not perform as well.

# EXAMPLE 7.9: PARAMETER ESTIMATION FOR SELECTED AR MODELS

+   1. **AR(1):** Figure 3.5a shows a realization of length n = 100 from the AR(1) model (1 - 0.95B)X_t = a_t when σ_a^2 = 1. For these data, the YW, Burg, and ML estimates of φ_1 = 0.95 are 0.93, 0.94, and 0.95, respectively, and, in all cases,