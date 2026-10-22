| Analysis of Maximum Likelihood Estimates |
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | 1.5268 | 0.1352 | 127.4323 | <.0001 |
| stage | 1 | -1.1785 | 0.0753 | 244.9951 | <.0001 |
| white | 1 | -0.6918 | 0.0731 | 89.5732 | <.0001 |
| old | 1 | 0.0919 | 0.0867 | 1.1228 | 0.2893 |
| faed 1 | 1 | 0.2678 | 0.0776 | 11.9123 | 0.0006 |
| faed 2 | 1 | 0.6771 | 0.1336 | 25.7059 | <.0001 |
| faed 3 | 1 | 1.2031 | 0.1339 | 80.7279 | <.0001 |

| Odds Ratio Estimates |
| Effect | Point Estimate | 95% Wald Confidence Limits |
| stage | 0.308 | 0.266 | 0.357 |
| white | 0.501 | 0.434 | 0.578 |
| old | 1.096 | 0.925 | 1.299 |
| faed 1 vs 4 | 1.307 | 1.123 | 1.522 |
| faed 2 vs 4 | 1.968 | 1.515 | 2.557 |
| faed 3 vs 4 | 3.330 | 2.562 | 4.330 |

The highly significant deviance and Pearson chi-square statistics suggest that something about this model is not right. Like the other ordinal models, this one imposes some restrictions, namely that the effects of the explanatory variables are the same at each stage. We can test this by including interactions between STAGE and the other three variables:

```
MODEL advance(EVENT='1')=stage white old faed stage*white stage*old stage*faed;
```

This produces the Type 3 statistics shown in Output 6.13. Clearly there are interactions with all three variables, which means that each variable has different effects on advancement into high school and advancement to high school graduation.