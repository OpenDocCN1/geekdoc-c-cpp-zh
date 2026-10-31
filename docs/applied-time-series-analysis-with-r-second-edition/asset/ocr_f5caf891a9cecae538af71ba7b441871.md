combinations of the Y'_j s, the mean-squared error E[(X_t - sum_{j=1}^s a_j Y_j)^2] is a minimum. A similar result follows when the univariate random variables are replaced by their vector counterparts. That is, if Y_1, ..., Y_s, X_t are jointly multivariate normal, then the conditional expectation E[X_t | Y_1, ..., Y_s] is the linear combination sum_{j=1}^s A_j Y_j such that E[(X_t - sum_{j=1}^s A_j Y_j)(X_t - sum_{j=1}^s A_j Y_j)'] is a minimum. For prediction, we want to find

$$\hat{X}_t^{t-1} = E[X_t | Y_1, ..., Y_{t-1}],$$

which has the associated mean-squared error

$$\Gamma_t^{t-1} = E[(\mathbf{X}_t - \hat{\mathbf{X}}_t^{t-1})(\mathbf{X}_t - \hat{\mathbf{X}}_t^{t-1})'].$$

From Equation 10.48, it follows that

$$\hat{\mathbf{X}}_t^{t-1} = E[\mathbf{X}_t | \mathbf{Y}_1, ..., \mathbf{Y}_{t-1}]$$ $$= E[\mathbf{F}\mathbf{X}_{t-1} + \mathbf{V}_t | \mathbf{Y}_1, ..., \mathbf{Y}_{t-1}]$$ $$= \mathbf{F}\hat{\mathbf{X}}_{t-1}^{t-1},$$

since E[V_t | Y_1, ..., Y_{t-1}] = 0, giving the relationship in Equation 10.50. Now,

$$\Gamma_t^{t-1} = E[(\mathbf{X}_t - \hat{\mathbf{X}}_t^{t-1})(\mathbf{X}_t - \hat{\mathbf{X}}_t^{t-1})']$$ $$= E[(\mathbf{F}\mathbf{X}_{t-1} + \mathbf{V}_t - \mathbf{F}\hat{\mathbf{X}}_{t-1}^{t-1})(\mathbf{F}\mathbf{X}_{t-1} + \mathbf{V}_t - \mathbf{F}\hat{\mathbf{X}}_{t-1}^{t-1})']$$ $$= E[(\mathbf{F}(\mathbf{X}_{t-1} - \hat{\mathbf{X}}_{t-1}^{t-1}) + \mathbf{V}_t)(\mathbf{F}(\mathbf{X}_{t-1} - \hat{\mathbf{X}}_{t-1}^{t-1}) + \mathbf{V}_t)']$$ $$= E[\mathbf{F}(\mathbf{X}_{t-1} - \hat{\mathbf{X}}_{t-1}^{t-1})(\mathbf{X}_{t-1} - \hat{\mathbf{X}}_{t-1}^{t-1})' \mathbf{F}'] + E[\mathbf{V}_t \mathbf{V}_t']$$ $$= \mathbf{F}\Gamma_{t-1}^{t-1}\mathbf{F}' + \Gamma_V,$$

giving Equation 10.51. Note also that