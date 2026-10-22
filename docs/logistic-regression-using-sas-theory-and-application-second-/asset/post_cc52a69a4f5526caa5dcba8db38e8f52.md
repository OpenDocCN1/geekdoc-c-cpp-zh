
```sas
DATA tab4_1a;
    INPUT f blackd death;
    DATALINES;
22 0 1
28 1 1
52 0 0
45 1 0
;
```

Then we use the FREQ statement in LOGISTIC to specify that each of these data lines is to be replicated, using the number of replications given by the variable F:

```sas
PROC LOGISTIC DATA=tab4_1a;
    FREQ f;
    MODEL death(EVENT='1') = blackd;
RUN;
```

Results are identical to those in Output 4.1.

The other way to handle tabular data is to use the events/trials syntax. Instead of inputting all four internal cell counts in the table, we input the cell frequencies for death sentences along with the column totals, i.e., the number of black defendants and the number of non-black defendants:

```sas
DATA tab4_1b;
    INPUT death total blackd;
    DATALINES;
22 74 0
28 73 1
;
```

We can describe this data set as follows: among 74 non-black defendants, 22 got the death penalty; among 73 black defendants, 28 got the death penalty.

Next we specify a dependent variable that has two parts, separated by a slash:

```sas
PROC LOGISTIC DATA=tab4_1b;
    MODEL death/total = blackd;
RUN;
```

Instead of replicating the observations, LOGISTIC treats the variable DEATH as having a binomial distribution with the number of trials (an apt term for these data) given by the variable TOTAL. Note that with this syntax, you do not need the EVENT='1' option in the MODEL statement. That’s because using DEATH as the number of events directly specifies death penalty (rather than life sentence) as the event of interest. Again, results are identical to those in Output 4.1.

For a 2 × 2 table, we can also produce many of these results with PROC FREQ:

```sas
PROC FREQ DATA=tab4_1a;
    WEIGHT f;
    TABLES blackd*death / CHISQ RELRISK;
RUN;
```

Selected results are shown in Output 4.2.

### Output 4.2 PROC FREQ Results

Statistics for Table of blackd by death

| Statistic | DF | Value | Prob |
|---|---|---|---|
| Chi-Square | 1 | 1.2184 | 0.2697 |
| Likelihood Ratio Chi-Square | 1 | 1.2205 | 0.2693 |
| Continuity Adj. Chi-Square | 1 | 0.8644 | 0.3525 |
| Mantel-Haenszel Chi-Square | 1 | 1.2101 | 0.2713 |
| Phi Coefficient |  | 0.0910 |  |
| Contingency Coefficient |  | 0.0907 |  |
| Cramer's V |  | 0.0910 |  |

Estimates of the Relative Risk (Row1/Row2)

| Type of Study | Value | 95% Confidence Limits |
|---|---|---|
| Case-Control (Odds Ratio) | 1.4707 | 0.7404 | 2.9214 |

The CHISQ option gives us several statistics for testing the null hypothesis that the two variables are independent, which is equivalent to the hypothesis that the slope is 0 in the logit model. Notice that Pearson’s chi-square (labeled simply chi-square in Output 4.2) is identical to the score statistic in the PROC LOGISTIC Output 4.1. The likelihood ratio chi-square in Output 4.2 is identical to the chi-square labeled −2LOG L in Output 4.1. The RELRISK option gives us the odds ratio, which is identical to the odds ratio in the PROC LOGISTIC output.

## 4.3 A Three-Way Table

As we’ve just seen, using LOGISTIC to estimate a logit model for a 2 × 2 table doesn’t tell you much more than you would get with PROC FREQ. But with a 3-way table, things get more interesting.

Consider Table 4.2, which shows the cross classification of race, gender, and occurrence of sexual intercourse for a national sample of 15- and 16-year-olds, reported by Morgan and Teachman (1988).

### Table 4.2 Race by Gender by Sexual Intercourse

| Race | Gender | Yes | No |
|---|---|---|---|
| White | Male | 43 | 134 |
| White | Female | 26 | 149 |
| Black | Male | 29 | 23 |
| Black | Female | 22 | 36 |

Let’s analyze Table 4.2 as a logit model, with intercourse as the dependent variable and race and sex as independent variables. Using the events/trials syntax in LOGISTIC, we have:

```sas
DATA interco;
    INPUT white male yes no;
    total=yes+no;
    DATALINES;
1 1 43 134
1 0 26 149
0 1 29 23
0 0 22 36
;
PROC LOGISTIC DATA=interco;
    MODEL yes/total=white male / SCALE=NONE;
RUN;
```

The SCALE=NONE option is included so that we can get the deviance and Pearson chi-square tests for goodness of fit. When you use the events/trials syntax, the AGGREGATE option is not needed because the data are already in aggregated form.

### Output 4.3 PROC LOGISTIC Output for Analysis of Three-Way Table

**Deviance and Pearson Goodness-of-Fit Statistics**

| Criterion | Value | DF | Value/DF | Pr > ChiSq |
|---|---|---|---|---|
| Deviance | 0.0583 | 1 | 0.0583 | 0.8091 |
| Pearson | 0.0583 | 1 | 0.0583 | 0.8092 |

**Analysis of Maximum Likelihood Estimates**

| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
|---|---|---|---|---|---|
| Intercept | 1 | -0.4555 | 0.2221 | 4.2045 | 0.0403 |
| white | 1 | -1.3135 | 0.2378 | 30.5132 | <.0001 |
| male | 1 | 0.6478 | 0.2250 | 8.2872 | 0.0040 |

**Odds Ratio Estimates**

| Effect | Point Estimate | 95% Wald Confidence Limits |
|---|---|---|
| white | 0.269 | 0.169 | 0.429 |
| male | 1.911 | 1.230 | 2.971 |

Selected results are shown in Output 4.3. The first thing to notice is that the deviance and Pearson chi-square statistics are both only .058 with 1 degree of freedom, yielding a p-value of .81. Because this is a goodness-of-fit test, a high p-value means that the model fits well. Clearly this model fits the data extremely well.

But what is the deviance testing? Remember that the deviance always compares the fitted model with a saturated model. For a 2 × 2 × 2 table, the saturated logit model includes an interaction between the two explanatory variables in their effects on the dependent variable. There’s one coefficient for this interaction, corresponding to the single degree of freedom for the deviance. So, in this case, the deviance is testing the null hypothesis that the interaction coefficient is 0. We conclude that there’s no evidence for an interaction.

To see this more explicitly, let’s actually fit the model with the interaction:

```sas
PROC LOGISTIC DATA=interco;
    MODEL yes/total=white male white*male/ SCALE=NONE ;
RUN;
```

In Output 4.4 we see that the deviance is 0, as it should be for a saturated model. The interaction term has a chi-square of .0583 with a p-value of .8092, identical to what we got for the deviance in the “main effects” model. The absence of an interaction means that race has the same effect for both boys and girls. And gender has the same effect for both blacks and whites.

### Output 4.4 PROC LOGISTIC Output for a Saturated Model

**Deviance and Pearson Goodness-of-Fit Statistics**

| Criterion | Value | DF | Value/DF | Pr > ChiSq |
|---|---|---|---|---|
| Deviance | 0.0000 | 0 | . | . |
| Pearson | 0.0000 | 0 | . | . |

**Analysis of Maximum Likelihood Estimates**

| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
|---|---|---|---|---|---|
| Intercept | 1 | -0.4925 | 0.2706 | 3.3118 | 0.0688 |
| white | 1 | -1.2534 | 0.3441 | 13.2674 | 0.0003 |
| male | 1 | 0.7243 | 0.3888 | 3.4696 | 0.0625 |
| white*male | 1 | -0.1151 | 0.4765 | 0.0583 | 0.8092 |

What exactly are those effects? In Output 4.3, the odds ratio for MALE is 1.91. We can say, then, that the estimated odds of having had sexual intercourse by age 15 are nearly twice as large for males as for females, after adjusting for racial differences. It would probably be a mistake to put too much faith in the exact value 1.91, however. The 95% confidence interval is between 1.23 and 2.97.

For WHITE, the highly significant adjusted odds ratio is .269, indicating that the odds of intercourse for whites is a little more than one-fourth the odds for blacks. It may be easier to interpret the reciprocal 1/.269 = 3.72, which says that the odds for blacks are nearly four times the odds for whites, controlling for gender differences. This has a 95% confidence interval of 2.3 to 5.9 (obtained by taking the reciprocal of the confidence limits in Output 4.3). That’s about all we can usefully do with this table. We could examine residuals but because the model fits so well, there’s little point.

## 4.4 A Four-Way Table

Things are only a little more complicated with 4-way tables except that more interactions are possible. Consider Table 4.3, reported by Seeman (1977) based on surveys of adult males conducted in France and the United States. In each country, the respondent was asked about
