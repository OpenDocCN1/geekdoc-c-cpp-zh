The third column has a dual interpretation. The coefficients represent the effect of the explanatory variables on being in category 1 vs. category 2, conditional on not being in category 3. But they also represent the difference between the coefficients in the first two columns. PUNISH is the only variable whose coefficient declined significantly from column 1 to column 2. Equivalently, PUNISH is the only variable having a significant effect on keeping both vs. keeping the money only. Each one-level increase of PUNISH more than doubles the odds of keeping both vs. keeping the money only.

With a TEST statement, we can test the null hypothesis that *all* the coefficients in the first column are identical to the corresponding coefficients in the second column:

```
PROC LOGISTIC DATA=wallet;
    MODEL wallet = male business punish explain / LINK=GLOGIT;
    TEST male_1=male_2, business_1=business_2,
         punish_1=punish_2, explain_1=explain_2;
RUN;
```

As this program shows, we can refer to the coefficient for a variable in the first equation by putting _1 after the variable name in the TEST statement. To refer to a coefficient in the second equation, we append _2. The value after the underscore must be the actual value that the variable takes on, which could be a character value. Thus, if WALLET had values of A, B, and C instead of 1, 2, and 3, the TEST statement would have MALE_A=MALE_B, and so on.

The TEST statement tests the null hypothesis that all four pairs of coefficients are equal. It produces a Wald chi-square of 12.2844 with 4 degrees of freedom, yielding a *p*-value of .0154. We conclude that the coefficients estimated in columns 1 and 2 of Table 5.1 are *not* the same. If this test had produced a high *p*-value, it would suggest that categories 1 and 2 of WALLET could be combined into a single category.

How do we know if the model fits the data? The best way to approach this question is to consider the ways in which the model might be wrong. First, there could be interactions among the predictors in their effects on WALLET. And, second, treating PUNISH as a quantitative variable could be incorrect. That is, the effect of going from category 1 of PUNISH to category 2 could be different from the effect of going from 2 to 3.

Since all the predictors are discrete with a small number of values, we can test for both of these possibilities by requesting goodness-of-fit statistics, using the AGGREGATE and SCALE=NONE options: