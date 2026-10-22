As an example of the case-control design, we again use the data on shelter stays, but now with STAYBABY as the dependent variable rather than as an independent variable. Output 8.23 shows the results from estimating a logistic model (with PROC LOGISTIC) for the full data set of 8,402 women. We see evidence that the probability of having a baby during the shelter stay is higher for blacks, women with more children in the household, younger women, and those with longer shelter stays.

# Output 8.23 Logistic Regression of STAYBABY for Full Sample

| Response Profile |  |  |
| Ordered Value | STAYBABY | Total Frequency |
| 1 | 0 | 7611 |
| 2 | 1 | 791 |

| Analysis of Maximum Likelihood Estimates |  |  |  |  |
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | -2.6802 | 0.2204 | 147.8532 | <.0001 |
| BLACK | 1 | 0.2857 | 0.0860 | 11.0466 | 0.0009 |
| KIDS | 1 | 0.1558 | 0.0287 | 29.5256 | <.0001 |
| DOUBLEUP | 1 | 0.1497 | 0.0832 | 3.2351 | 0.0721 |
| AGE | 1 | -0.0467 | 0.00772 | 36.6776 | <.0001 |
| DAYS | 1 | 0.00447 | 0.000224 | 399.7093 | <.0001 |

Now let’s re-estimate the model for the 791 pairs of women who are matched by number of days of shelter stay. The LOGISTIC output without adjustment for matching is shown in Output 8.24.

# Output 8.24 Logistic Regression of STAYBABY for Matched Pairs, No Adjustment for Matching

| Response Profile |  |  |
| Ordered Value | STAYBABY | Total Frequency |
| 1 | 0 | 791 |
| 2 | 1 | 791 |