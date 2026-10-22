for the deviance in the “main effects” model. The absence of an interaction means that race has the same effect for both boys and girls. And gender has the same effect for both blacks and whites.

# Output 4.4  PROC LOGISTIC Output for a Saturated Model

| Deviance and Pearson Goodness-of-Fit Statistics |  |  |  |  |
|---|---:|---:|---:|---:|
| Criterion | Value | DF | Value/DF | Pr > ChiSq |
| Deviance | 0.0000 | 0 | . | . |
| Pearson | 0.0000 | 0 | . | . |

| Analysis of Maximum Likelihood Estimates |  |  |  |  |  |
|---|---:|---:|---:|---:|---:|
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | -0.4925 | 0.2706 | 3.3118 | 0.0688 |
| white | 1 | -1.2534 | 0.3441 | 13.2674 | 0.0003 |
| male | 1 | 0.7243 | 0.3888 | 3.4696 | 0.0625 |
| white*male | 1 | -0.1151 | 0.4765 | 0.0583 | 0.8092 |

What exactly are those effects? In Output 4.3, the odds ratio for MALE is 1.91. We can say, then, that the estimated odds of having had sexual intercourse by age 15 are nearly twice as large for males as for females, after adjusting for racial differences. It would probably be a mistake to put too much faith in the exact value 1.91, however. The 95% confidence interval is between 1.23 and 2.97.

For WHITE, the highly significant adjusted odds ratio is .269, indicating that the odds of intercourse for whites is a little more than one-fourth the odds for blacks. It may be easier to interpret the reciprocal 1/.269 = 3.72, which says that the odds for blacks are nearly four times the odds for whites, controlling for gender differences. This has a 95% confidence interval of 2.3 to 5.9 (obtained by taking the reciprocal of the confidence limits in Output 4.3). That’s about all we can usefully do with this table. We could examine residuals but because the model fits so well, there’s little point.

# 4.4  A Four-Way Table

Things are only a little more complicated with 4-way tables except that more interactions are possible. Consider Table 4.3, reported by Seeman (1977) based on surveys of adult males conducted in France and the United States. In each country, the respondent was asked about