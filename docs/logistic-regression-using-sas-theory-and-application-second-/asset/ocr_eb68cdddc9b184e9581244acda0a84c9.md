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

# Output 6.8  Results from Alternative Dichotomizations of General Happiness

1 vs. (2,3)

| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|---:|---:|
| **Analysis of Maximum Likelihood Estimates** |  |  |  |  |  |
| Intercept | 1 | -1.4615 | 0.0574 | 647.4056 | <.0001 |
| married | 1 | 0.9931 | 0.0624 | 253.2451 | <.0001 |
| year 1 | 1 | 0.2204 | 0.0699 | 9.9348 | 0.0016 |
| year 2 | 1 | 0.2271 | 0.0716 | 10.0650 | 0.0015 |
| year 3 | 0 | 0 | . | . | . |