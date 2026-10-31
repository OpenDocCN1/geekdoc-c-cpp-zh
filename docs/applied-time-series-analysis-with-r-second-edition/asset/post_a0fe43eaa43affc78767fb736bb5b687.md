
k = 8
1 - 1.988B + 0.989B²    1.005 ± 0.03i    0.995    0.005
1 - 1.19B + 0.63B²      0.95 ± 0.83i     0.79     0.11
1 - 0.56B               1.78             0.56     0
1 + 0.48B              -2.10            0.48     0.5
1 + 0.15B              1 + 0.15B + 0.22B²  -0.33 ± 2.09i  0.47  0.28
k = 10
1 - 1.986B + 0.987B²    1.006 ± 0.03i    0.994    0.005
1 - 1.37B + 0.72B²      0.94 ± 0.70i     0.85     0.10
1 + 0.82B              -1.23            0.82     0.5
1 + 0.80B + 0.62B²     -0.64 ± 1.09i    0.79     0.33
1 - 0.62B + 0.60B²      0.52 ± 1.19i     0.77     0.18
1 - 0.77B               1.30             0.77     0

![](img/a0e0259119deb8c7b41dfd4f664e541d_415_0.png)

## FIGURE 8.7

(a) Daily wages data in Figure 2.9a. (b) Sample autocorrelations for the realization in (a). (c) Data in (a) differenced. (d) Sample autocorrelation for differenced data in (c).

The wandering nature of the data and the slowing damping sample autocorrelations strongly suggest at least one positive unit root. Also, AR fits with p = 8, 10, and 12 (factor tables not shown here) show that the factor with roots closest to the unit circle are 1 − 0.997B for p = 8,

∇X_{t-j} = (1 - B)X_{t-j} = X_{t-j} - X_{t-j-1},   β₀ = μ(1 - φ₁ - ⋯ - φ_p),   τ = -(1 - φ₁ - ⋯ - φ_p),

and β_j = -(φ_{i+1} + ⋯ + φ_p), for j = 1, ..., p - 1. The form in Equation 8.23 is called the *error correction form*. (See Problem 8.10.) Note that there are p - 1 terms involving the ∇ X_{t-j} in Equation 8.23. These are sometimes called the *augmenting* terms. Note that if 1 - φ₁ z - ⋯ - φ_p z^p = 0 has a unit root, then 1 - φ₁ - ⋯ - φ_p = 0, and also τ = 0. As a consequence, tests for unit roots have been developed that test the hypothesis H₀ : τ = 0 versus H_a : τ < 0 in Equation 8.23. The augmented Dickey–Fuller (tau) test (see Dickey and Fuller, 1979) is based on considering Equation 8.23 to be a regression equation with dependent variable ∇X_t and independent variables X_{t-1}, ∇X_{t-1}, ..., ∇X_{t-p+1}. Using standard OLS regression (including an intercept term), the test statistic t_{DF} = \hat{τ} / se(\hat{τ}) is calculated, and H₀ : τ = 0 is rejected if t_{DF} < C for a critical value C. Dickey and Fuller (1979) show that under the null hypothesis H₀ : τ = 0, the sampling distribution of the test statistic, t_{DF}, does not follow the usual t-distribution and that its limiting distribution is skewed to the left. The α-level critical values, t*_{DF}(α), based on the limiting distribution are -2.57, -2.86, and -3.43 for α = 0.1, 0.05, and 0.01, respectively (Dickey, 1976). It should be noted that in practice, the value of p is chosen sufficiently large, so that the residuals, \hat{a}_t appear to be uncorrelated.

Testing for a factor (1 - B)^d, that is, d unit roots, requires application of the procedure d times. For example, if the null hypothesis of a unit root is not rejected, then a second unit root test could be performed by letting Y_t = (1 - B)X_t, considering the model

∇Y_t = α₀ + τ Y_{t-1} + β₁ ∇Y_{t-1} + ⋯ + β_{p-1} ∇Y_{t-p+1} + a_t,

and testing H₀ : τ = 0 in this new model.

## EXAMPLE 8.7

- 1. *Testing the data in Figure 8.6 for unit roots:* We apply the augmented Dickey–Fuller (tau) test to the realization from Equation 8.21 shown in Figure 8.6a. Note that this model has two unit roots and a second-order stationary component. We use

It should be noted that the adfTest function gives three versions of the augmented Dickey-Fuller test. In addition to the test including a constant term α₀ in the model in Equation 8.23 that was used above, a test assuming β₀ = 0, can be obtained using type = “nc”. The third form of the test is based on a model of the form in Equation 8.23 but with β₀ replaced by β₀ + β₁t, allowing for the possibility that some of the trending behavior in the data is caused by an underlying trend line. This test is obtained with adfTest using type = “ct”.

A final comment should be made about unit root tests. While these tests give the investigator a “yes-or-no” answer regarding a unit root, there are areas of concern regarding their use. Note that the decision to retain a unit root is based on failure to reject a null hypothesis, and depending on the power of the test, the conclusion that the model has a unit root may not be one that can be made with much confidence. Unit root tests can be useful tools to assist in the decision, but the final decision concerning the inclusion of nonstationary factors rests with the investigator. The point is that finite realizations from the nonstationary model (1 − B)Xₜ = aₜ and, for example, the stationary (but nearly nonstationary) model (1 − 0.97B)Xₜ = aₜ will be very similar, and tests such as the augmented Dickey–Fuller test will often conclude the existence of a unit root when applied to realizations from the aforementioned nearly nonstationary model. The final decision concerning whether to include a factor 1 − B should be based on such considerations as whether there is any reason to believe that there is an attraction to the mean, and a decay in the autocorrelations at lag lengths of interest (in which case a stationary model is appropriate). A unit root model is often used to model the behavior of stock market prices, where such an attraction to the mean does not seem to exist.

## 8.3.5.3 Including a Seasonal Factor (1 − B^s) in the Model

In Section 5.3, we discussed the multiplicative seasonal model. Here, we consider the special case

(1 − B^s)φ(B)(X_t − μ) = θ(B)a_t,  (8.24)

In these models, the s roots of 1 − z^s = 0 all lie on the unit circle, and the seasonal factor, 1 − B^s, models a tendency in the data for the patterns observed at times t = 1, 2, ..., s to be similar to the patterns for observations t = s + 1, s + 2, ..., 2s, etc. For example, quarterly sales data may exhibit a seasonal behavior if

the general pattern of sales in each quarter (e.g., relatively lower sales in first quarter, higher sales in fourth quarter, etc.) tends to be repeated from year to year. As mentioned in Section 5.3, it is typical to use a seasonal model with \(s = 4\) for quarterly data exhibiting such behavior or \(s = 12\) for monthly data with this type of pattern. In Example 5.9, we discussed the “airline model”

$$(1-B)(1-B^s)\phi(B)(X_t-\mu)=\theta(B)a_t, \tag{8.25}$$

as a model that allows for seasonal and trending behavior. However, a seasonal component may or may not be appropriate for data collected monthly, quarterly, etc. In the following examples, we discuss techniques that help you determine whether a seasonal component is appropriate.

## EXAMPLE 8.8: SIMULATED SEASONAL DATA

Figure 8.8 shows a realization and sample autocorrelations from the seasonal model

$$(1-B^{12})(1-1.25B+0.9B^2)(X_t-50)=a_t, \tag{8.26}$$

with white noise variance \(\sigma_a^2=1\). The realization in Figure 8.8a can be found in data set `fig8.8a` in tswge. Inspection of the realization shows that a 12-unit seasonal pattern seems to be replicated, and the sample autocorrelations show spikes at multiples of 12. To further examine the need for the nonstationary seasonal component, \(1-B^{12}\), in the fitted model, we use the overfitting procedure used previously. In order to decide whether to include a seasonal factor, \(1-B^{12}\), we overfit using AR(\(p\)) models with \(p=16\), 18, and 20. Table 8.4 shows the factor table for \(p=16\), which is similar to those for the other two overfit orders considered. This factor table should be compared to the factors of \(1-B^{12}\) shown in Table 5.5.

![](img/a0e0259119deb8c7b41dfd4f664e541d_421_0.png)

## FIGURE 8.8

(a) Seasonal data from model in **Equation 8.26**. (b) Sample autocorrelations of the data in (a). (c) Plot of (a) transformed by $1 - B^{12}$. (d) Sample autocorrelations of transformed data in (c).

## Table 8.4

Factor Table for AR(16) Model Fit to the Realization in **Figure 8.8a**

| AR Factors | Roots ($r_j$) | $|r_j^{-1}|$ | $f_{0j}$ |
|---|---|---:|---:|
| $1 + 1.73B + 0.998B^2$ | $-0.87 \pm 0.50i$ | 0.999 | 0.417 |
| $1 + 1.01B + 0.997B^2$ | $-0.50 \pm 0.87i$ | 0.998 | 0.334 |
| $1 + 0.998B^2$ | $-1.002$ | 0.998 | 0.5 |
| $1 - 0.01B + 0.995B^2$ | $0.01 \pm 1.00i$ | 0.997 | 0.249 |
| $1 - B + 0.993B^2$ | $0.50 \pm 0.87i$ | 0.997 | 0.167 |
| $1 - 1.71B + 0.984B^2$ | $0.87 \pm 0.51i$ | 0.992 | 0.084 |
| $1 - 0.988B$ | $1.012$ | 0.988 | 0 |
| $1 - 1.27B + 0.855B^2$ | $0.74 \pm 0.79i$ | 0.925 | 0.130 |
| $1 + 0.164B$ | $-6.109$ | 0.164 | 0.5 |
| $1 - 0.152B$ | $6.583$ | 0.152 | 0 |

By examining the factors associated with the first seven rows of the factor table in **Table 8.4**, it can be seen that these factors are very
