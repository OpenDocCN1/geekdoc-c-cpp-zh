∇X_{t-j} = (1 - B)X_{t-j} = X_{t-j} - X_{t-j-1},   β₀ = μ(1 - φ₁ - ⋯ - φ_p),   τ = -(1 - φ₁ - ⋯ - φ_p),

and β_j = -(φ_{i+1} + ⋯ + φ_p), for j = 1, ..., p - 1. The form in Equation 8.23 is called the *error correction form*. (See Problem 8.10.) Note that there are p - 1 terms involving the ∇ X_{t-j} in Equation 8.23. These are sometimes called the *augmenting* terms. Note that if 1 - φ₁ z - ⋯ - φ_p z^p = 0 has a unit root, then 1 - φ₁ - ⋯ - φ_p = 0, and also τ = 0. As a consequence, tests for unit roots have been developed that test the hypothesis H₀ : τ = 0 versus H_a : τ < 0 in Equation 8.23. The augmented Dickey–Fuller (tau) test (see Dickey and Fuller, 1979) is based on considering Equation 8.23 to be a regression equation with dependent variable ∇X_t and independent variables X_{t-1}, ∇X_{t-1}, ..., ∇X_{t-p+1}. Using standard OLS regression (including an intercept term), the test statistic t_{DF} = \hat{τ} / se(\hat{τ}) is calculated, and H₀ : τ = 0 is rejected if t_{DF} < C for a critical value C. Dickey and Fuller (1979) show that under the null hypothesis H₀ : τ = 0, the sampling distribution of the test statistic, t_{DF}, does not follow the usual t-distribution and that its limiting distribution is skewed to the left. The α-level critical values, t*_{DF}(α), based on the limiting distribution are -2.57, -2.86, and -3.43 for α = 0.1, 0.05, and 0.01, respectively (Dickey, 1976). It should be noted that in practice, the value of p is chosen sufficiently large, so that the residuals, \hat{a}_t appear to be uncorrelated.

Testing for a factor (1 - B)^d, that is, d unit roots, requires application of the procedure d times. For example, if the null hypothesis of a unit root is not rejected, then a second unit root test could be performed by letting Y_t = (1 - B)X_t, considering the model

∇Y_t = α₀ + τ Y_{t-1} + β₁ ∇Y_{t-1} + ⋯ + β_{p-1} ∇Y_{t-p+1} + a_t,

and testing H₀ : τ = 0 in this new model.

# EXAMPLE 8.7

+   1. *Testing the data in Figure 8.6 for unit roots:* We apply the augmented Dickey–Fuller (tau) test to the realization from Equation 8.21 shown in Figure 8.6a. Note that this model has two unit roots and a second-order stationary component. We use