# Output 8.26 PROC GLIMMIX Estimates for Hybrid PTSD Model

| Covariance Parameter Estimates |
| Cov Parm | Subject | Estimate | Standard Error |
| Intercept | subjid | 2.1220 | 0.6115 |

| Solutions for Fixed Effects |
| Effect | time | Estimate | Standard Error | DF | t Value | Pr > |t| |
| Intercept |  | 0.4516 | 1.7457 | 312 | 0.26 | 0.7961 |
| dcontrol |  | -1.1815 | 0.4131 | 626 | -2.86 | 0.0044 |
| dproblem |  | 0.2009 | 0.09911 | 626 | 2.03 | 0.0431 |
| dsevent |  | 0.1946 | 0.1538 | 626 | 1.27 | 0.2062 |
| mcontrol |  | -1.1438 | 0.4210 | 626 | -2.72 | 0.0068 |
| mproblem |  | 0.4913 | 0.09908 | 626 | 4.96 | <.0001 |
| msevent |  | 0.8033 | 0.1966 | 626 | 4.09 | <.0001 |
| cohe s |  | -0.2345 | 0.06373 | 626 | -3.68 | 0.0003 |
| time | 1 | 0.8433 | 0.2873 | 626 | 2.94 | 0.0035 |
| time | 2 | 0.4433 | 0.2324 | 626 | 1.91 | 0.0569 |
| time | 3 | 0 | . | . | . | . |

While the deviation coefficients can be interpreted in the same way as the conditional logit coefficients, the coefficients for the mean variables are usually difficult to interpret causally. Under the assumptions of the conventional random intercept model of Section 8.5, the coefficients for the mean variables and the corresponding deviation variables should be identical. Hence, the degree to which they differ can be the basis of a specification test for the conventional model. We can test the null hypothesis that the coefficients are the same by including a CONTRAST statement in the hybrid model program:

```
CONTRAST 'spec test' dcontrol 1 mcontrol -1,
    dproblem 1 mproblem -1, dsevent 1 msevent -1;
```

This produced an F-statistic of 4.25 with 3 and 626 degrees of freedom, yielding a p-value of .0055. Apparently, at least one pair of coefficients is different, suggesting that the conventional mixed model could lead to biased estimates of the coefficients.