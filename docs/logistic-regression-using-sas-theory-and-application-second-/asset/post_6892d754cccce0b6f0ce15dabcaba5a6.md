
| Analysis of Maximum Likelihood Estimates |
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | -0.7870 | 0.1748 | 20.2718 | <.0001 |
| nih | 1 | 0.0729 | 0.0158 | 21.2380 | <.0001 |

| Odds Ratio Estimates |
| Effect | Point Estimate | 95% Wald Confidence Limits |
| nih | 1.076 | 1.043 | 1.110 |

What can we do about this? Well, we can get a saturated model by deleting NIH and putting in dummy variables for 39 of the 40 universities. That wouldn’t be very informative, however—we might just as well look at the percentages receiving postdoctoral training across the 40 universities. Because there’s only one independent variable, we don’t have the option of including interactions, but we can allow for nonlinearities by including powers of NIH in the model. I tried a squared term but that didn’t help at all. The addition of a cubed term got the p-value up to .032, but further powers didn’t bring any improvement. (I tried up to the 7th power.) In short, any polynomial model with enough terms to fit would be so complicated that it would have little appeal over the saturated model.

However, it’s quite possible that the lack of fit is due not to departures from linearity in the effect NIH funding but to a lack of independence in the observations. There are many characteristics of biochemistry departments besides NIH funding that may have some impact on whether their graduates seek and get postdoctoral training. Possibilities include the prestige of the department, whether the department is in an agricultural school or a medical school, and the age of the department. Omitting these variables from the model could induce a residual correlation among the observations: People from the same department tend to have the same outcome because they share a common environment. This lack of independence will produce what is called extra-binomial variation—the variance of the dependent variable will be greater than what is expected under the assumption of a binomial distribution. Besides producing a large deviance, extra-binomial variation can result in underestimates of the standard errors and overestimates of the chi-square statistics.

One approach to this problem is to adjust the chi-squares and test statistics, leaving the coefficient estimates unchanged. The adjustment is quite simple: Take the ratio of the goodness-of-fit chi-square to its degrees of freedom, and then divide all the individual chi-squares by that ratio. Equivalently, take the square root of the ratio and multiply all the standard errors by that number. This adjustment, which can be based either on the Pearson chi-square or the deviance, is easily implemented in LOGISTIC by changing the SCALE option. SCALE=D makes the adjustment with the deviance chi-square and SCALE=P uses the Pearson chi-square.

Output 4.15 shows results produced by the SCALE=D option. The coefficient (and odds ratio) are identical to what we saw in Output 4.14. However, we are informed that “the covariance matrix has been multiplied by the heterogeneity factor…1.68853”, which is the deviance divided by the degrees of freedom. As a consequence, all the chi-squares and all the model fit statistics in Output 4.15 are divided by this number. Thus, the Wald chi-square for NIH declines from 21.2 to 12.56, which is considerably smaller but still highly significant. The standard errors are multiplied by the square root of 1.68853. Because the deviance and the Pearson chi-square are pretty close for this data, switching to the SCALE=P option wouldn’t make much difference.

## Output 4.15 Doctorate Model with Overdispersion Adjustment

| Deviance and Pearson Goodness-of-Fit Statistics |
| Criterion | Value | DF | Value/DF | Pr > ChiSq |
| Deviance | 64.1642 | 38 | 1.6885 | 0.0050 |
| Pearson | 61.0206 | 38 | 1.6058 | 0.0103 |

| Model Fit Statistics |
| Criterion | Intercept Only | Intercept and Covariates | With Constant |
| AIC | 377.901 | 366.798 | 100.830 |
| SC | 382.030 | 375.056 | 109.088 |
| -2 Log L | 375.901 | 362.798 | 96.830 |

| Testing Global Null Hypothesis: BETA=0 |
| Test | Chi-Square | DF | Pr > ChiSq |
| Likelihood Ratio | 13.1032 | 1 | 0.0003 |
| Score | 12.9347 | 1 | 0.0003 |
| Wald | 12.5778 | 1 | 0.0004 |

| Analysis of Maximum Likelihood Estimates |
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | -0.7870 | 0.2271 | 12.0056 | 0.0005 |
| nih | 1 | 0.0729 | 0.0206 | 12.5778 | 0.0004 |

| Odds Ratio Estimates |
| Effect | Point Estimate | 95% Wald Confidence Limits |
| nih | 1.076 | 1.033 | 1.120 |

PROC LOGISTIC offers an alternative overdispersion correction proposed by Williams (1982) that modifies the coefficients as well as the standard errors and chi-squares. Based on the method of quasi-likelihood, these coefficients should be more statistically efficient than the conventional estimates; that is, they should have smaller true standard errors. The SAS code for implementing this correction is

```
PROC LOGISTIC DATA=nihdoc;
    MODEL pdoc/docs=nih / SCALE=WILLIAMS;
RUN;
```

Results are shown in Output 4.16. Williams’ method uses iterative reweighting of the observations, and this is reflected in much of the reported output. In the preliminary output, we see the weight function used at the final iteration, along with the sum of the weights. This sum can be thought of as the effective sample size after correction for overdispersion.

Although both Pearson and deviance chi-squares are reported, there is a warning that they are not to be used to assess the fit of the model. Both the coefficient and the chi-square for NIH are a little larger than they were under the simpler SCALE=D correction in Output 4.15. Note that when the group size variable (DOCS in this example) has the same value for all groups, Williams’ method does not alter the conventional coefficient estimates, and the standard error correction is the same as the simpler adjustment using Pearson’s chi-square.

## Output 4.16 Doctorate Model with Williams’ Adjustment for Overdispersion

| Model Information |
| Data Set | WORK.NIHDOC |
| Response Variable (Events) | pdoc |
| Response Variable (Trials) | docs |
| Weight Variable | 1 / ( 1 + 0.042183 * (docs - 1) ) |

| Model Information |
|---|---|
| Model | binary logit |
| Optimization Technique | Fisher's scoring |

| Number of Observations Read | 40 |
| Number of Observations Used | 40 |
| Sum of Frequencies Read | 459 |
| Sum of Frequencies Used | 459 |
| Sum of Weights Read | 276.8967 |
| Sum of Weights Used | 276.8967 |

| Response Profile |
| Ordered Value | Binary Outcome | Total Frequency | Total Weight |
| 1 | Event | 216 | 133.24419 |
| 2 | Nonevent | 243 | 143.65250 |

| Deviance and Pearson Goodness-of-Fit Statistics |
| Criterion | Value | DF | Value/DF | Pr > ChiSq |
| Deviance | 39.8872 | 38 | 1.0497 | 0.3862 |
| Pearson | 37.9995 | 38 | 1.0000 | 0.4695 |

Number of events/trials observations: 40

Note: Since the Williams method was used to accommodate overdispersion, the Pearson chi-squared statistic and the deviance can no longer be used to assess the goodness of fit of the model.

| Model Fit Statistics |
| Criterion | Intercept Only | Intercept and Covariates | With Constant |
| AIC | 385.469 | 370.396 | 114.478 |
| SC | 389.598 | 378.654 | 122.736 |
| -2 Log L | 383.469 | 366.396 | 110.478 |

| Testing Global Null Hypothesis: BETA=0 |
| Test | Chi-Square | DF | Pr > ChiSq |
| Likelihood Ratio | 17.0734 | 1 | <.0001 |
| Score | 16.7876 | 1 | <.0001 |
| Wald | 16.1391 | 1 | <.0001 |

| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|---:|---:|
| Intercept | 1 | -0.7521 | 0.2084 | 13.0309 | 0.0003 |
| nih | 1 | 0.0829 | 0.0206 | 16.1391 | <.0001 |

| Effect | Point Estimate | 95% Wald Confidence Limits |
|---|---:|---:|
| nih | 1.086 | 1.043, 1.131 |

What makes the doctorate example different from the earlier examples in this chapter is that the individuals are grouped into naturally occurring clusters, in this case, university departments. It’s reasonable to suppose that individuals in the same department are *not* independent—not only can they influence each other, but they are also exposed to many common factors that may produce the same outcome. In most contingency table analyses, on the other hand, individuals are grouped together merely because they have the same values on some discrete variable. In such cases, there is usually no reason to think that the observations within groups are anything other than independent.

When independence is presumed, the correct strategy for dealing with overdispersion is to elaborate the model until you find a version that does fit the data, not to casually invoke the overdispersion options. If, after diligent investigation, you cannot come up with a reasonably parsimonious model with an acceptable fit to the data, then there may be some value in correcting the standard errors and test statistics for any remaining overdispersion. But be aware that the correction for overdispersion always produces chi-square statistics that are lower than they would be without the correction.

Note also that overdispersion does *not* arise from heterogeneity *within* groups. The problem stems from differences *between* groups, differences that are not fully described by the measured variables. Another way to deal with overdispersion is to postulate a random effect for departments that accounts for the overdispersion. This can be done with PROC GLIMMIX or PROC NLMIXED. In Chapter 8, we’ll see how to use these procedures to analyze individual-level data when there is clustering and a lack of independence within clusters. See Allison (1987) for still other ways to approach the overdispersion problem for these data.

It’s also worth noting that the “badness of fit” for the NIH data comes primarily from a small number of observations. The graph in Output 4.17 shows the change in the deviance
