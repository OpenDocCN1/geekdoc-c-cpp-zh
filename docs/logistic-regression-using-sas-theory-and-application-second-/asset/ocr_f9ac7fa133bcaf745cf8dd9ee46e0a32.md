| Analysis of Maximum Likelihood Estimates |
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | -0.7870 | 0.1748 | 20.2718 | <.0001 |
| nih | 1 | 0.0729 | 0.0158 | 21.2380 | <.0001 |

| Odds Ratio Estimates |
| Effect | Point Estimate | 95% Wald Confidence Limits |
| nih | 1.076 | 1.043 | 1.110 |

What can we do about this? Well, we can get a saturated model by deleting NIH and putting in dummy variables for 39 of the 40 universities. That wouldn’t be very informative, however—we might just as well look at the percentages receiving postdoctoral training across the 40 universities. Because there’s only one independent variable, we don’t have the option of including interactions, but we can allow for nonlinearities by including powers of NIH in the model. I tried a squared term but that didn’t help at all. The addition of a cubed term got the p-value up to .032, but further powers didn’t bring any improvement. (I tried up to the 7th power.) In short, any polynomial model with enough terms to fit would be so complicated that it would have little appeal over the saturated model.

However, it’s quite possible that the lack of fit is due not to departures from linearity in the effect NIH funding but to a lack of independence in the observations. There are many characteristics of biochemistry departments besides NIH funding that may have some impact on whether their graduates seek and get postdoctoral training. Possibilities include the prestige of the department, whether the department is in an agricultural school or a medical school, and the age of the department. Omitting these variables from the model could induce a residual correlation among the observations: People from the same department tend to have the same outcome because they share a common environment. This lack of independence will produce what is called extra-binomial variation—the variance of the dependent variable will be greater than what is expected under the assumption of a binomial distribution. Besides producing a large deviance, extra-binomial variation can result in underestimates of the standard errors and overestimates of the chi-square statistics.

One approach to this problem is to adjust the chi-squares and test statistics, leaving the coefficient estimates unchanged. The adjustment is quite simple: Take the ratio of the goodness-of-fit chi-square to its degrees of freedom, and then divide all the individual chi-squares by that ratio. Equivalently, take the square root of the ratio and multiply all the