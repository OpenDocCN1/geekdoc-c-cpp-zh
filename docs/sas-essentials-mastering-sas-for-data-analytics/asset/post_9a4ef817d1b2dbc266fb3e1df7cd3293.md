
# CHAPTER 12: CORRELATION AND REGRESSION

# TABLE 12.6 (Continued)

| Option | Explanation |
| --- | --- |
| Common statements for PROC REG for multiple regression | |
| OUTPUT OUT=datame | Specifies output set information. For example, MODEL=Y=A1 B1; OUTPUT OUT=OUTREG P=YHAT R=YRESID; creates the variables YHAT for predicted values (P) and R for residual values. Other handy variables include LCL and UCL (confidence limits on individual values) and LCLM and UCLM (confidence limits on the mean) |
| PLOTS=options | Requests plots. Some options include COOKD, LCL, UCL, UCLM, and RESIDUALS (see SAS documentation for others) |

# TABLE 12.7 Common Options for the PROC REG MODEL statement (Options Follow/)

| Option | Explanation |
| --- | --- |
| P | Requests a table containing predicted values from the model |
| R | Requests that the residuals be analyzed |
| CLM | Prints the 95% upper and lower confidence limits for the expected value of the variable (mean) for each observation |
| CLI | Requests the 95% upper and lower confidence limits for an individual value of the dependent variable |
| INCLUDE=k | Includes the first k variables in the variable list for the model (automated selection procedures) |
| SELECT=option | Specifies the variable selection procedure. Options include BACKWARD, FORWARD, and STEPWISE (see below) |
| SLSTAY=p | Specifies the maximum p-value for a variable to stay in a model during automated selection. Default values are 0.10 for BACKWARD and 0.15 for STEPWISE |
| SLENTRY=p | Minimum p-value for a variable to enter a model for forward or stepwise selection. Default values are 0.50 for FORWARD and 0.15 for STEPWISE |

In particular, the SELECT=option specifies how variables will be considered for inclusion in the model. The BACKWARD method considers all predictor variables and eliminates the variables that do not meet the minimal SLSTAY criterion until only those meeting the criterion remain. The FORWARD method brings in the most significant variable that meets the SLENTRY criterion and continues entering variables until none meets the criterion. STEPWISE is a mixture of the two; it begins like the FORWARD method but reevaluates at each step and may eliminate a variable if it does not meet the SLSTAY criterion. Additional model selection criteria are also available in SAS.

# HANDS-ON EXAMPLE

In this example, an employer wants to be able to predict how well applicants will do the job once they are hired. He devises four tests that he thinks will measure the skills required for the job. Ten prospects are selected at random from a group of applicants and given the four tests. Then they are given an on-the-job proficiency score (JOBSCORE) by a supervisor who observes their work.

- 1. Open the program file AREG2.SAS.

```
DATA JOB;
INPUT SUBJECT $ TEST1 TEST2 TEST3 TEST4 JOBSCORE;
CARDS;
1 75 100 90 88 78
2 51 85 88 89 71
3 99 96 94 93 85
4 92 106 84 84 67
5 90 89 83 77 69
6 67 77 83 73 65
7 109 67 71 65 50
8 94 112 105 91 107
9 105 110 95 95 96;
PROC REG;
MODEL JOBSCORE=TEST1 TEST2 TEST3 TEST4;
TITLE 'Job Score Analysis using PROC REG';
RUN;
QUIT;
```

Note that the dependent variable in the MODEL statement is JOBSCORE and that the TEST variables, listed on the right side of the equal sign, are the independent variables.

- 2. Run the program and observe the analysis of variance given in Table 12.8. This table includes an overall test of significance of the model. Because p=0.0003, you would reject the null hypothesis that all β=0 and conclude that the model is predictive of JOBSCORE. In fact, R-Square=0.9754, you have evidence that the model is a good fit and provides a good prediction of JOBSCORE.

# TABLE 12.8 Analysis of Variance for PROC REG

| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
|---|---|---|---|---|---|
| Model | 4 | 2495.9648 | 623.9912 | 49.58 | 0.0003 |
| Error | 5 | 62.9352 | 12.5870 | | |
| Corrected Total | 9 | 2558.9000 | | | |
| Root MSE | | 3.5477 | R-Square | 0.9754 | |
| Dependent Mean | | 75.1000 | Adj R-Sq | 0.9557 | |
| Coeff Var | | 4.7247 | | | |

- 3. To continue examining the model, look at the parameter estimates in Table 12.9. These estimates show results for tests of significance (Pr > t) of the intercept and each coefficient. In this case, TEST1 (p = 0.0446) and TEST3 (p = 0.0015) seem to be the best predictors.

# TABLE 12.9 Parameter Estimates

| | DF | Parameter Estimate | Standard Error | t Value | Pr > t |
|---|---|---|---|---|---|
| Intercept | 1 | -0.95539 | 0.12843 | -7.45 | 0.0007 |
| TEST1 | 1 | 0.17631 | 0.06616 | 2.66 | 0.0446 |
| TEST2 | 1 | -0.22344 | 0.14354 | -1.56 | 0.1803 |
| TEST3 | 1 | 1.74602 | 0.27770 | 6.29 | 0.0015 |
| TEST4 | 1 | 0.26965 | 0.18424 | 1.46 | 0.2406 |

Examine the diagnostic plots for this analysis in Figure 12.7. General explanations for these plots were given in the previous example using simple linear regression. In this instance, note that issues with the model include a possible outlier identified by Cook's plot (observation 10). Otherwise, the residual plots look reasonable. There are also some possible issues related to variability identified in the bottom plots. For now we ignore these possible issues.

img/611344fee6085d6edba5f406f54c12_311_0.png

12.7 Visualizing a prediction interval

img/611344fee6085d6edba5f406f54c12_312_0.png

Figure12.7 (Continued)

- As in this case, the p-values for TEST2 and TEST4 are not significant (p > 0.05), a typical strategy is dropping them from the model and rerunning the program to see how the reduced model fits the data. Take TEST2 and TEST4 out of the model statement and resubmit the code

- (a) How does this change the model? The R-Square still indicate a good fit?
- (b) Are the same issues present in terms of the residual plots?
- (c) If each test costs $20 to administer, and you intend to give it to 100 applicants, do you think the reduced model is still an adequate predictor of JOBSCORE?

# 12.3.2 Automated Model Selection

It is often the case in multiple regression analysis that one of your goals is to arrive at a model that yields an optimal regression equation with the fewest parameters. In the previous Hands-Example, the predictors TEST2 and TEST4 are not significant. As mentioned, following the listing of MODEL options, a variety of automated selection procedures are available in SAS. You can choose to select variables using manual or automated methods, or a combination of both. The various model selection techniques will not always result in the same final model, and the decision which variables to include in the final model should not be based entirely on the results of any automated procedure. The researcher's knowledge of the data should always be used to guide the model selection process when automated procedures are used.

The following Hands-Example illustrates the BACKWARD elimination technique for model selection. In this technique, the full model is examined, and in successive steps the least significant variable is eliminated from the model until all remaining variables show at least a p<0.10 significance level.

```
HANDS-ON EXAMPLE
This example illustrates how to use automated model selection techniques.

1. Open the program file AREG3.SAS . This code is similar to the previous example, but includes a SELECTION Statement:

(continued)

```
MODEL JOBSCORE=TEST1 TEST2 TEST3 TEST4
/SELECTION=BACKWARD;
```

2. Submit this program. Because BACKWARD selection, it examines the full model first, and then drops variables that not predictive. In the output, not shown here, you will see that at Step 1, TEST4 is removed from the model.

# TABLE 12.10 Parameter Estimates for Revised Model

| Variable | Parameter Estimate | Standard Error | Type II SS | F Value | Pr > F |
|---|---|---|---|---|---|
| Intercept | -89.06844 | 14.38805 | 666.44835 | 38.60 | 0.0004 |
| TEST1 | 0.15607 | 0.07562 | 73.55164 | 4.26 | 0.0779 |
| TEST3 | 1.70426 | 0.14680 | 2327.04675 | 134.78 | <0001 |

3. Because TEST1 is marginally significant (and not significant at 0.05) and if each test is expensive, you might want to use a more stringent rule to retain variables (e.g., use a smaller value for SLAY). Change the model statement to retain

```
MODEL JOBSCORE=TEST1 TEST2 TEST3 TEST4
/SELECTION=BACKWARD
SLAY=0.05;
```

SLAY=0.05 tells SAS to remove variables whose significance level is 0.05 or larger (the default is 0.10). Run the revised program and observe the parameter estimates in Table 12.11, which now includes the predictor variable TEST3. Also note that $R^2 =0.924$. This model is still highly significant and appears to be strongly predictive of JOBSCORE.

# TABLE 12.11 Parameter Estimates for Final Model

| Variable | Parameter Estimate | Standard Error | Type II SS | F Value | Pr > F |
|---|---|---|---|---|---|
| Intercept | -76.81121 | 15.47905 | 598.34835 | 24.62 | 0.0011 |
| TEST3 | 1.71651 | 0.17402 | 2364.49377 | 97.30 | <0001 |
