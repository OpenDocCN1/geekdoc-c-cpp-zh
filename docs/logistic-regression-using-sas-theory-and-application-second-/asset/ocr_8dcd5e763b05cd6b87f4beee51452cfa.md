|  | Odds Ratio Estimates |  |  |
|---|---|---|---|
| Effect | Point Estimate | 95% Wald Confidence Limits |  |
| dark | 4.000 | 0.849 | 18.836 |
| soft | 0.111 | 0.014 | 0.877 |
| nuts | 2.333 | 0.603 | 9.023 |

Output 7.1 looks much like previous LOGISTIC output, but there are a couple of additions. The second line describes this as a “conditional analysis.” Then, a little later, there is a new table titled “Strata Summary.” We see from this table that there are 10 strata, one for each person. Each stratum has exactly one record with CHOOSE=1, and seven records with CHOOSE=0. Later, we’ll see an example in which there are several different response patterns. There are also a couple of things that are missing from the output. No intercept is reported, which is a characteristic of conditional logistic regression that I’ll explain in the next section. And we don’t get the usual “Association of Predicted Probabilities and Observed Responses” table.

We do get the usual global tests of the null hypothesis that all the coefficients are 0. In this case, all three are statistically significant, although the p-value for the Wald test is quite a bit higher than for the other two. As in other models, the likelihood-ratio test is generally preferred.

In the next table, we find coefficients and associated statistics. Only the SOFT coefficient has a p-value below .05. However, I was suspicious of those p-values for two reasons: (a) the sample size is on the small side with only 80 records contributed from 10 persons, and (b) there is a marked divergence between the global likelihood ratio chi-square and the Wald chi-square. To resolve this uncertainty, I did exact tests by adding the following statement to the previous program:

```
EXACT dark soft nuts / ESTIMATES=BOTH;
```