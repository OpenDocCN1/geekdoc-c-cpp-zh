
Notice that I’ve coded HAPPY so that 1 is very happy and 3 is not too happy.

To fit the cumulative logit model, we run the following program, with results shown in Output 6.6:

```
PROC LOGISTIC DATA=happy;
    FREQ count;
    CLASS year / PARAM=GLM;
    MODEL happy = married year / AGGREGATE SCALE=NONE;
RUN;
```

## Output 6.6 Cumulative Logit Results for Happiness Data

| Score Test for the Proportional Odds Assumption |  |  |
|---|---|---|
| Chi-Square | DF | Pr > ChiSq |
| 26.5204 | 3 | <.0001 |

| Deviance and Pearson Goodness-of-Fit Statistics |  |  |  |  |
|---|---|---|---|---|
| Criterion | Value | DF | Value/DF | Pr > ChiSq |
| Deviance | 30.9709 | 7 | 4.4244 | <.0001 |
| Pearson | 31.4060 | 7 | 4.4866 | <.0001 |

| Testing Global Null Hypothesis: BETA=0 |  |  |  |
|---|---|---|---|
| Test | Chi-Square | DF | Pr > ChiSq |
| Likelihood Ratio | 356.3435 | 3 | <.0001 |
| Score | 348.4470 | 3 | <.0001 |
| Wald | 340.2626 | 3 | <.0001 |

| Type 3 Analysis of Effects |  |  |  |
|---|---|---|---|
| Effect | DF | Wald Chi-Square | Pr > ChiSq |
| married | 1 | 322.9185 | <.0001 |
| year | 2 | 3.7616 | 0.1525 |

| Analysis of Maximum Likelihood Estimates |
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept 1 | 1 | -1.3919 | 0.0513 | 735.2275 | <.0001 |
| Intercept 2 | 1 | 1.4160 | 0.0517 | 749.6434 | <.0001 |
| married | 1 | 0.9931 | 0.0553 | 322.9185 | <.0001 |
| year 1 | 1 | 0.0716 | 0.0636 | 1.2673 | 0.2603 |
| year 2 | 1 | 0.1195 | 0.0640 | 3.4827 | 0.0620 |
| year 3 | 0 | 0 | . | . | . |

| Odds Ratio Estimates |
| Effect | Point Estimate | 95% Wald Confidence Limits |
| married | 2.700 | 2.422 | 3.008 |
| year 1 vs 3 | 1.074 | 0.948 | 1.217 |
| year 2 vs 3 | 1.127 | 0.994 | 1.278 |

The first thing we see in Output 6.6 is that the score test for the proportional odds assumption indicates fairly decisive rejection of the model. This is corroborated by the overall goodness-of-fit tests (obtained with the AGGREGATE and SCALE=NONE options), both of which have p-values less than .0001. The score test has 3 degrees of freedom corresponding to the constraints imposed on the three coefficients in the model. Roughly speaking, the score test (chi-square=26.5) can be thought of as one component of the overall deviance (chi-square=31). So we can say that approximately 85% of the deviance stems from the constraints imposed by the cumulative logit model. The remaining 15% (and 4 degrees of freedom) comes from possible interactions between year and marital status that have been excluded from the model.

Should we reject the model? Keep in mind that the sample size is quite large (5,724 cases), so it may be hard to find any parsimonious model with a p-value above .05. But let’s postpone a decision until we examine more evidence. Turning to the lower part of the output, we see strong evidence that married people report greater happiness than the unmarried people, but little evidence for change over time. Neither of the individual year coefficients is statistically significant. The Type 3 test that both coefficients are 0 is also nonsignificant. So let’s try deleting the year variables and see what happens (Output 6.7).

## Output 6.7 Happiness Model with Year Deleted

| Score Test for the Proportional Odds Assumption |
| Chi-Square | DF | Pr > ChiSq |
| 0.3513 | 1 | 0.5534 |

| Deviance and Pearson Goodness-of-Fit Statistics |
| Criterion | Value | DF | Value/DF | Pr > ChiSq |
| Deviance | 0.3508 | 1 | 0.3508 | 0.5537 |
| Pearson | 0.3513 | 1 | 0.3513 | 0.5534 |

Number of unique profiles: 2

| Analysis of Maximum Likelihood Estimates |
| Parameter |  | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept 1 |  | 1 | -1.3497 | 0.0459 | 865.8068 | <.0001 |
| Intercept 2 |  | 1 | 1.4569 | 0.0468 | 968.1472 | <.0001 |
| married |  | 1 | 1.0017 | 0.0545 | 337.2287 | <.0001 |

| Odds Ratio Estimates |
| Effect | Point Estimate | 95% Wald Confidence Limits |
| married | 2.723 | 2.447 3.030 |

Now the model fits great. Of course, there’s only 1 degree of freedom in the score test because only one coefficient is constrained across the two implicit equations. The deviance and Pearson chi-squares also have only 1 degree of freedom because LOGISTIC has regrouped the data after the elimination of the year variables. Interpreting the marital status effect, we find that married people have odds of higher happiness that are nearly three times the odds for unmarried people.

It’s tempting to leave it at this, but the fact that the score statistic declined so dramatically with the deletion of the year variables suggests that something else is going on. To see what it might be, let’s fit separate models for the two ways of dichotomizing the happiness variable.

```
DATA a;
    SET happy;
    lesshap=happy GE 2;
    nottoo=happy EQ 3;
PROC LOGISTIC DATA=a;
    FREQ count;
    CLASS year / PARAM=GLM;
    MODEL lesshap=married year;
PROC LOGISTIC DATA=a;
    FREQ count;
    CLASS year / PARAM=GLM;
    MODEL nottoo=married year;
RUN;
```

Results are shown in Output 6.8. If the cumulative logit model is correct, the coefficients for the three variables should be the same in the two models. That’s nearly true for MARRIED. But the two YEAR variables have negative coefficients in the first model and positive coefficients in the second. Three of the four coefficients are significant at beyond the .01 level. This is surely the cause of the difficulty with the cumulative logit model. What seems to be happening is that 1994 is different from the other two years, but not in a way that could be described as a uniform increase or decrease in happiness. Rather, in that year there were relatively more cases in the middle category and fewer in the two extreme categories.

## Output 6.8 Results from Alternative Dichotomizations of General Happiness

1 vs. (2,3)

| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|---:|---:|
| **Analysis of Maximum Likelihood Estimates** |  |  |  |  |  |
| Intercept | 1 | -1.4615 | 0.0574 | 647.4056 | <.0001 |
| married | 1 | 0.9931 | 0.0624 | 253.2451 | <.0001 |
| year 1 | 1 | 0.2204 | 0.0699 | 9.9348 | 0.0016 |
| year 2 | 1 | 0.2271 | 0.0716 | 10.0650 | 0.0015 |
| year 3 | 0 | 0 | . | . | . |

## Output 6.9 Results from QLIM with Heterogeneous Disturbance

|  | Parameter Estimates |  |  |  |
| Parameter | DF | Estimate | Standard Error | t Value | Approx Pr > |t| |
| Intercept | 1 | 1.224813 | 0.055617 | 22.02 | <.0001 |
| married | 1 | -0.904331 | 0.056926 | -15.89 | <.0001 |
| _Limit2 | 1 | 2.549680 | 0.085444 | 29.84 | <.0001 |
| _H.yr94 | 1 | -0.335531 | 0.080389 | -4.17 | <.0001 |
| _H.yr84 | 1 | -0.081647 | 0.094153 | -0.87 | 0.3858 |

Results are consistent with what we have already seen. The sign of the MARRIED coefficient is the opposite of what we got with PROC LOGISTIC, because QLIM predicts the probability of being in a higher category, not a lower category, of the dependent variable. The two parameters preceded by _H are effects on the residual variance. We see that the variance in 1994 is significantly lower than in 1974, indicating that in 1994 people were more likely to be in the middle category and less likely to be in the extremes. The parameter labeled _LIMIT2 is the functional equivalent of the second intercept in the PROC LOGISTIC model.

## 6.6 Adjacent Categories Model

Another general model for ordered categorical data is the adjacent categories model. As before, we let p_ij be the probability that individual i falls into category j of the dependent variable, and we assume that the categories are ordered in the sequence j=1, ..., J. Now take any pair of categories that are adjacent, such as j and j+1. We can write a logit model for the contrast between these two categories as a function of explanatory variables:

log( p_{i,j+1} / p_{ij} ) = α_j + β_j x_i      j = 1,...,J-1,      (6.6)

where β_j x_i = β_{j1} x_{i1} + ... + β_{jk} x_{ik}. There are J-1 of these paired contrasts. It turns out that this is just another way of writing the multinomial logit model for unordered categories. In other words, equation (6.6) is equivalent to equation (5.1). To get the adjacent categories model for ordered data, we impose a constraint on this set of equations. Specifically, we assume that β_j = β for all j. In other words, instead of having a different set of coefficients
