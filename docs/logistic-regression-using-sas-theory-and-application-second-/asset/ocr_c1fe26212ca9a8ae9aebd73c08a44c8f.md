```
0 0 2  5
0 0 3  13
;
PROC LOGISTIC DATA=afterlif;
    FREQ count;
    MODEL belief=white female / LINK=GLOGIT AGGREGATE
        SCALE=NONE;
RUN;
```

Each of the two predictor variables is coded 1 or 0. The dependent variable BELIEF is coded: 1=Yes, 2=Undecided, and 3=No. Because “No” has the highest value, it becomes the reference category for the model.

Results are shown in Output 5.6. The deviance and Pearson chi-square tests indicate no significant lack of fit. Because the only difference between this model and a “saturated” model is the interaction between race and gender, the high p-values for the goodness of fit statistics simply mean that there is no evidence for that interaction. All of the three chi-square tests for the “global null hypothesis” give p-values of around .065. So there is only marginal evidence that either of the two predictors has an effect on the response. From the Type 3 table, however, we see evidence for a gender effect but no indication of a race effect.

# Output 5.6 PROC LOGISTIC Results for Afterlife Data

| Response Profile |
| Ordered Value | belief | Total Frequency |
| 1 | 1 | 710 |
| 2 | 2 | 108 |
| 3 | 3 | 173 |

Logits modeled use belief=3 as the reference category.

| Deviance and Pearson Goodness-of-Fit Statistics |
| Criterion | Value | DF | Value/DF | Pr > ChiSq |
| Deviance | 0.8539 | 2 | 0.4269 | 0.6525 |
| Pearson | 0.8609 | 2 | 0.4304 | 0.6502 |