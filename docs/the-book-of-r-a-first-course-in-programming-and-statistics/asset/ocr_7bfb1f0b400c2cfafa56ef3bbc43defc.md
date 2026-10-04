Residual standard error: 7.909 on 260 degrees of freedom
(29 observations deleted due to missingness)
Multiple R-squared: 0.3612, Adjusted R-squared: 0.3581
F-statistic: 116.5 on 1 and 206 DF, p-value: < 2.2e-16

# 20.3.2 Regression Coefficient Significance Tests

Let's begin by focusing on the way the estimated regression coefficients are reported. The first column of the coefficients table contains the point estimates of the intercept and slope (the intercept is labeled as such, and the slope is labeled after the name of the predictor variable in the data frame); the table also includes estimates of the standard errors of these statistics. It can be shown that simple linear regression coefficients, when estimated using least-squares, follow a t-distribution with $n-2$ degrees of freedom (when the number of observations, $n$, is used in the model fit). The standardized t value and a p-value are reported for each parameter. We represent the results of a two-tailed hypothesis test defined as

> $H_0 : \beta_j = 0$
$H_A : \beta_j \neq 0$

where $j = 0$ for the intercept and $j = 1$ for the slope, using the notation in Equation (20.1).
Focus on the row of results for the predictor. With a null value of zero, truth of $H_0$ implies that the predictor has no effect on the response. The claim here is interested in whether there is *any effect* of the covariate, not the direction of this effect, so $H_A$ is two-sided (via #). With any hypothesis test, the smaller the p-value, the stronger the evidence against $H_0$. With a small p-value ($< 2 \times 10^{-16}$) attached to this particular test statistic (which we can confirm using the formula in Chapter 18: $T = (3.116-0)/0.2888 = 10.79$), you'd conclude there is strong evidence *against* the claim that the predictor has no effect on the mean level of the response.

The same test is carried out for the intercept, but for the slope parameter $\beta_1$ is typically more interesting (since rejection of the null hypothesis for $\beta_1$ simply indicates that the regression line does not strike the vertex at zero), especially when the observed data don't include $x=0$, as is the case here.

From this, you can conclude the fitted model shows evidence that an increase in handspan is associated with an increase in height among the population being studied. For each additional centimeter of handspan, the average increase in height is approximately 3.12 cm.

You could produce confidence intervals for your estimates using Equation (17,2) on page 378 and knowledge of the sampling distributions of the regression parameters; however, again, R provides a convenient function for object of class "lm" to do this for you.