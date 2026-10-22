| Model Fit Statistics |  |  |
|---|---|---|
| Criterion | Intercept Only | Intercept and Covariates |
| AIC | 356.140 | 319.367 |
| SC | 362.686 | 339.005 |
| -2 Log L | 352.140 | 307.367 |

| Testing Global Null Hypothesis: BETA=0 |  |  |  |
|---|---|---|---|
| Test | Chi-Square | DF | Pr > ChiSq |
| Likelihood Ratio | 44.7727 | 4 | <.0001 |
| Score | 40.8753 | 4 | <.0001 |
| Wald | 38.5746 | 4 | <.0001 |

| Analysis of Maximum Likelihood Estimates |  |  |  |  |  |
|---|---|---|---|---|---|
| Parameter |  | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept 1 |  | 1 | -3.2691 | 0.5612 | 33.9325 | <.0001 |
| Intercept 2 |  | 1 | -1.4913 | 0.5085 | 8.6012 | 0.0034 |
| male |  | 1 | 1.0636 | 0.3255 | 10.6771 | 0.0011 |
| business |  | 1 | 0.7370 | 0.3515 | 4.3973 | 0.0360 |
| punish |  | 1 | 0.6874 | 0.2246 | 9.3644 | 0.0022 |
| explain |  | 1 | -1.0452 | 0.3392 | 9.4972 | 0.0021 |

| Odds Ratio Estimates |  |  |
|---|---|---|
| Effect | Point Estimate | 95% Wald Confidence Limits |
| male | 2.897 | 1.531 | 5.483 |
| business | 2.090 | 1.049 | 4.161 |
| punish | 1.989 | 1.280 | 3.089 |
| explain | 0.352 | 0.181 | 0.684 |

Turning to the more familiar portions of the output, we see from the global tests that there is strong evidence that at least one of the coefficients is not 0. This is further confirmed by the lower portion of the output which shows that all the coefficients have p-values below .05. In the next section, we’ll see how the parameter estimates and odds ratios can be interpreted in a fashion that is nearly identical to interpretation in a binary logit model.