![](bbox=[0.258, 0.125, 0.742, 0.315])

The $p$-value is the probability of obtaining a test statistic (e.g. $t$-statistic) at least as extreme as the one that was actually observed, assuming that the NULL hypothesis is true. It is often necessary to reject the NULL hypothesis when the $p$-value is less than 0.05 i.e. a 5% chance of rejecting the NULL hypothesis when it is true. When the NULL hypothesis is rejected, the result is said to be statistically significant. That is, if 95% of the $t$-distribution is closer to the mean than the $t$-statistic for the coefficient of the regression, this relates to a $p$-value of 5%. With such a value there is only a 5% chance that the results of the regression analysis would have occurred in a random distribution, or there is a 95% probability that the coefficient is having some effect on the regression model. It is important to note that the size of the $p$-value for a coefficient indicates nothing about the effect the coefficient is having on the regression model i.e. is possible to have a coefficient with a very low $p$-value which has only a minimal effect on the model.

# 4.12.2 Residual Plots

The error term in the linear regression model must possess the following properties:

+   1. The errors in the regression model must be random variables and have a mean of zero
2. The variance of the errors must be constant i.e. homoscedastic.$^{22}