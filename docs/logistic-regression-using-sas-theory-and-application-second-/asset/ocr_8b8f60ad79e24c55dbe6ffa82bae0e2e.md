| Analysis Of GEE Parameter Estimates |
| Empirical Standard Error Estimates |
| Parameter |  | Estimate | Standard Error | 95% Confidence Limits |  | Z | Pr > |Z| |
| Intercept |  | 1.5381 | 0.8748 | -0.1765 | 3.2527 | 1.76 | 0.0787 |
| control |  | -0.9365 | 0.2167 | -1.3612 | -0.5118 | -4.32 | <.0001 |
| problems |  | 0.2735 | 0.0502 | 0.1752 | 0.3718 | 5.45 | <.0001 |
| sevent |  | 0.2885 | 0.0865 | 0.1189 | 0.4580 | 3.33 | 0.0009 |
| cohes |  | -0.1843 | 0.0462 | -0.2750 | -0.0937 | -3.99 | <.0001 |
| time | 1 | 0.4099 | 0.1817 | 0.0537 | 0.7661 | 2.26 | 0.0241 |
| time | 2 | 0.2799 | 0.1712 | -0.0557 | 0.6156 | 1.63 | 0.1021 |
| time | 3 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | . | . |
| Alpha1 |  | 0.7762 | 0.2966 | 0.1949 | 1.3576 | 2.62 | 0.0089 |
| Alpha2 |  | 1.2778 | 0.3382 | 0.6149 | 1.9407 | 3.78 | 0.0002 |
| Alpha3 |  | 1.6549 | 0.3632 | 0.9431 | 2.3668 | 4.56 | <.0001 |

The “Log Odds Ratio Parameter Information ” table defines the parameters ALPHA1 through ALPHA3 corresponding to the pairs of repeated measurements. The estimates of these parameters then appear as part of the main regression table in Output 8.9. Keep in mind that these are logarithms of the odds ratios, not the odds ratios themselves. What’s nice is that we get significance tests for each of these estimates, something that we couldn’t get with conventional GEE. The coefficients for the explanatory variables are very similar to what we saw in Output 8.7.

To estimate the analog of the exchangeable model, we change the REPEATED statement to read

```
REPEATED SUBJECT=subjid / WITHIN=time LOGOR=EXCH;
```

which says that there is only a single odds ratio for all pairs of repeated measurements. That produces the results in Output 8.10. The estimates and associated statistics are not much different from those in the preceding output, but now we only get a single log-odds ratio of 1.206. Exponentiating this value gives an odds ratio of 3.34. Thus, for example, if you had PTSD at time 1, your odds of having PTSD at time 3 are 3.34 what they would be if you did not have PTSD at time 1 (controlling for other variables in the model).