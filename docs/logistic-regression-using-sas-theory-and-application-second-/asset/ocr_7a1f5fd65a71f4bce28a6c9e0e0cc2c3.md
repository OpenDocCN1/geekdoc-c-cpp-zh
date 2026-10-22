If we have access to the individual-level data, we can simply estimate a logit model directly, as with the following LOGISTIC program:

```
PROC LOGISTIC DATA=penalty;
    MODEL death(EVENT='1') = blackd;
RUN;
```

Results are shown in Output 4.1. The odds ratio is identical to what we got in Section 2.4 by hand calculation. It is not statistically significant.

# Output 4.1 PROC LOGISTIC Output for a 2 x 2 Table

| Testing Global Null Hypothesis: BETA=0 |
|---|---|---|---|
| Test | Chi-Square | DF | Pr > ChiSq |
| Likelihood Ratio | 1.2205 | 1 | 0.2693 |
| Score | 1.2184 | 1 | 0.2697 |
| Wald | 1.2134 | 1 | 0.2707 |

| Analysis of Maximum Likelihood Estimates |
|---|---|---|---|---|---|
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | -0.8602 | 0.2543 | 11.4390 | 0.0007 |
| blackd | 1 | 0.3857 | 0.3502 | 1.2134 | 0.2707 |

| Odds Ratio Estimates |
|---|---|---|---|
| Effect | Point Estimate | 95% Wald Confidence Limits | |
| blackd | 1.471 | 0.740 | 2.921 |

Now, suppose we don’t have the individual-level data. All we have is Table 4.1. There are two different ways to get the tabular data into PROC LOGISTIC. The first method is to create a data set that has one record for each of the four cell frequencies in the table, together with appropriately coded variables that represent the defendant’s race and sentence: