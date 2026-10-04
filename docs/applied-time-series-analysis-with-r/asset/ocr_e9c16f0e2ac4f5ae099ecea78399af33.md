# 9.3 Signal-Plus-Noise versus Purely Autocorrelation-Driven Models

Based on the preceding discussion, a question of importance is “how do we test for trend in time series data?” In Section 5.1, we considered the signal-plus-noise model.

$X_t = s_t + Z_t,$$

where
$s_t$ is a deterministic signal
$Z_t$ is a zero-mean stationary noise component that is usually modeled using ARMA($p,q$) model

For purposes here, we consider the case in which $s_t = a + bt$. That is, the signal-plus-noise (regression) model is given by

$X_t = a + bt + Z_t,$

Suppose we want to decide whether the observed data follow an ARMA($p,q$) model, which could be denoted

$X_t = \mu + Z_t,$

or a signal-plus-noise model of the form Equation 9.11. Noting that Equation 9.11 is the more general model and simplifies to Equation 9.12 if $b=0$, then the natural approach would be to fit a model of the form Equation 9.11 and test $H_0: b=0$. If this hypothesis is rejected, then the decision would be to include a deterministic component in the model. For simplicity in the following, we consider the case in which $Z_t$ satisfies an AR($p$) model. Since the residuals in the regression model in Equation 9.11 may be correlated, the test for $H_0: b=0$ using standard regression-based procedures assuming uncorrelated residuals may not be appropriate. Testing $H_0: b=0$ in Equation 9.11 when the residuals are correlated is a difficult problem, primarily due to the fact, as discussed in Section 5.1, that realizations from stationary AR($p$) models such as Equation 9.12 can produce results with trending behavior. Several authors have addressed this problem, and we discuss a few approaches here.

# 9.3.1 Cochrane–Orcutt and Other Methods

Consider the case in which $(1 - \phi_B)Z_t = a_r$. In this case, it follows from Equation 9.11 that