
The syntax for GLIMMIX combines many of the features of PROC GENMOD and PROC MIXED (which does linear mixed models). The option METHOD=QUAD is essential for getting maximum likelihood estimates rather than pseudo likelihood estimates. QUAD refers to Gaussian quadrature, which is the method used to integrate the likelihood function over the distribution of the random intercept. The D=B option on the MODEL statement specifies a binomial distribution for the dependent variable, with a default logit link function. Note that, unlike LOGISTIC, SURVEYLOGISTIC, or GENMOD, PROC GLIMMIX does not require the DESCENDING option or the EVENT='1' option. With D=B, GLIMMIX models the probability of a 1 rather than a 0. The SOLUTION option (which can be abbreviated as just S) requests that coefficient estimates be reported, in addition to the usual hypothesis tests.

The RANDOM statement (which is much like the RANDOM statement in PROC MIXED), declares that the intercept will be treated as a random variable. The SUBJECT option says that this random variable will be different for each value of the SUBJID variable, but will be the same for observations with the same value of SUBJID. The COVTEST statement provides a test of the null hypothesis that the variance of α is 0. Output 8.11 gives the results.

Note that I’ve included SUBJID in the CLASS statement. Unlike GENMOD, GLIMMIX does not require that the subject variable be in the CLASS statement, but it’s usually a good idea to do so. If the data are sorted by the subject variable, you’ll get the same results whether that variable is or is not in the CLASS statement. But if the data are not sorted by the subject variable, leaving it out of the CLASS statement will yield completely erroneous results.

## Output 8.11 PROC GLIMMIX Results for a Random Intercepts Model

| Covariance Parameter Estimates |
| Cov Parm | Subject | Estimate | Standard Error |
| Intercept | subjid | 2.1242 | 0.5774 |

| Solutions for Fixed Effects |
| Effect | time | Estimate | Standard Error | DF | t Value | Pr > |t| |
| Intercept |  | 2.3588 | 1.1838 | 314 | 1.99 | 0.0472 |
| control |  | -1.3239 | 0.2969 | 627 | -4.46 | <.0001 |
| problems |  | 0.3545 | 0.07049 | 627 | 5.03 | <.0001 |
| sevent |  | 0.4016 | 0.1086 | 627 | 3.70 | 0.0002 |
| cohes |  | -0.2476 | 0.06249 | 627 | -3.96 | <.0001 |
| time | 1 | 0.5258 | 0.2518 | 627 | 2.09 | 0.0371 |
| time | 2 | 0.3513 | 0.2394 | 627 | 1.47 | 0.1428 |
| time | 3 | 0 | . | . | . | . |

| Tests of Covariance Parameters Based on the Likelihood |
| Label | DF | -2 Log Like | ChiSq | Pr > ChiSq | Note |
| Parameter list | 1 | 966.85 | 41.54 | <.0001 | MI |

MI: P-value based on a mixture of chi-squares.

The first thing we see in the output is an estimate of the variance of the random intercept: 2.1242. If this were 0, we’d be back to an ordinary logistic regression model. At the bottom of the output, we get a likelihood ratio chi-square test of the null hypothesis that this variance is 0. Clearly, that hypothesis can be rejected. Incidentally, there are serious technical difficulties that arise in the calculation of the p-value for a likelihood ratio test that a variance is equal to 0. But GLIMMIX solves those problems by calculating p-values “based on a mixture of chi-squares.”

In the “Solutions for Fixed Effects” table, we find the coefficients, standard errors, t-statistics and p-values. Let’s compare these results in with those in Output 8.10 for the GEE exchangeable odds ratio model, which is the GEE model that’s most similar to the random intercepts model. The t-statistics in Output 8.11 are all pretty close to the z-statistics in Output 8.10 (both are just ratios of the coefficients to their standard errors). But the

coefficients for the random intercepts model are all larger in magnitude than the coefficients for the GEE model. That’s to be expected because mixed model coefficients correct for heterogeneity shrinkage but GEE coefficients do not. The greater the variance of α, the bigger the difference you will find between mixed model and GEE coefficients.

So if you really want subject-specific estimates of the coefficients, mixed models are the way to go. But mixed models can be much more computationally intensive than GEE because of the need for numerical integration. And not infrequently, they break down completely for reasons that are not always apparent. If your main goal is to get accurate p-values, GEE may do perfectly well.

Mixed models can be elaborated in several different ways, one of which is to allow the coefficients themselves to vary randomly across persons. This is sometimes called a random slopes model. Let’s try it for the PTSD data. Suppose we think that SEVENT (the number of stressful events) has different effects for different people. To allow for this, we can modify the model by putting an i subscript on the coefficient vector.

log( p_it / (1 - p_it) ) = α_i + β_i x_it . (8.3)

This equation would allow all the coefficients to vary across persons, but we want to focus on the special case where just one of them is allowed to vary. We’ll assume that the SEVENT coefficient is normally distributed, with a mean and variance that we shall estimate. We’ll also assume that the random coefficient is independent of everything else on the right-hand side of the equation. Here’s the GLIMMIX code for implementing that model:

```
PROC GLIMMIX DATA=ptsd METHOD=QUAD;
    CLASS subjid time;
    MODEL ptsd = control problems sevent cohes time / D=B S;
    RANDOM INTERCEPT sevent/ SUBJECT=subjid;
    COVTEST 0 .;
    COVTEST . 0;
RUN;
```

To make a coefficient random, we merely put the variable name on the RANDOM statement. This can only be done for variables that vary within subject. We could not, for example, put COHES on the RANDOM statement because it was only measured once and does not change

over time. Also, it’s nearly always a bad idea to allow coefficients to be random without also specifying a random intercept.

Notice the two COVTEST statements. The first one tests the null hypothesis that the variance of the random intercept is 0, while allowing the random slope to be non-zero. The second tests the null hypothesis that the random slope is 0, while allowing the random intercept to be non-zero.

Results are shown in Output 8.12. In the first table, we see the estimated variances of the random intercept and the random slope. At first glance, the slope variance does not appear to be significantly different from 0 because it is not more than twice its standard error. Nevertheless, the more accurate likelihood ratio test reported in the bottom table yields a p-value of .015. So we do have evidence of variability in the effect of SEVENT across persons in the sample.

## Output 8.12 PROC GLIMMIX Results for a Random Slope Model

| Covariance Parameter Estimates |
| Cov Parm | Subject | Estimate | Standard Error |
| Intercept | subjid | 2.1546 | 0.6649 |
| sevent | subjid | 0.7009 | 0.4773 |

| Solutions for Fixed Effects |
| Effect | time | Estimate | Standard Error | DF | t Value | Pr > |t| |
| Intercept |  | 2.8295 | 1.2997 | 314 | 2.18 | 0.0302 |
| control |  | -1.4913 | 0.3313 | 387 | -4.50 | <.0001 |
| problems |  | 0.3774 | 0.07738 | 387 | 4.88 | <.0001 |
| sevent |  | 0.3054 | 0.1521 | 240 | 2.01 | 0.0458 |
| cohes |  | -0.2620 | 0.06785 | 387 | -3.86 | 0.0001 |
| time | 1 | 0.6014 | 0.2720 | 387 | 2.21 | 0.0276 |
| time | 2 | 0.4236 | 0.2581 | 387 | 1.64 | 0.1016 |
| time | 3 | 0 | . | . | . | . |

| Label | DF | -2 Log Like | ChiSq | Pr > ChiSq | Note |
|---|---|---:|---:|---:|---:|---|
| Parameter list | 1 | 948.35 | 27.76 | <.0001 | MI |
| Parameter list | 1 | 925.31 | 4.71 | 0.0150 | MI |

**MI:** P-value based on a mixture of chi-squares.

The coefficients reported in the “Solutions for Fixed Effects” table are very similar to those in Output 8.11, which did not have the random slope. However, the coefficient for SEVENT (.3054) now has a different interpretation. Instead of being the unique coefficient of SEVENT, it is merely the mean of the coefficients across persons. With a standard deviation of .84 (the square root of the random-effects variance of .7009), there is a lot of variability in this effect. Under the assumption that the coefficient is normally distributed, we conclude that 68 percent of the people have coefficients that range between -.53 and 1.15 (adding and subtracting one standard deviation). That’s a big range.

It’s possible to have more than one random slope, but when I tried to introduce random slopes for each of the other variables, the algorithm failed to converge. The default is to assume that the all random effects are uncorrelated. But you can allow for correlations by specifying TYPE=UNR as an option on the RANDOM statement. When I did this for the model in Output 8.12, I got a correlation of -.29 between the random intercept and the random slope. But that correlation was not significantly different from 0.

By default, the standard errors reported by GLIMMIX are model-based rather than robust. This means that they are based on the exchangeability assumption, an assumption that is not easily relaxed in the mixed model framework. It’s easy to switch to robust standard errors, however, by putting the option EMPIRICAL on the PROC statement. That’s generally a good idea unless the sample size is small. (For smaller samples, the empirical standard errors can be somewhat improved by specifying EMPIRICAL=MBN.) For this example, switching to robust standard errors made very little difference.

## 8.6 Fixed-Effects with Conditional Logistic Regression

Although GEE and mixed models are wonderful tools, they don’t correct for bias resulting from omitted explanatory variables at the cluster level. To be more specific, when you have multiple observations per person—as in the PTSD example—it is possible to statistically
