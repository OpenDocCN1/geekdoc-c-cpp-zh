

kinds of errors. Failing to detect a disease might be regarded as a substantially more costly error than diagnosing someone with the disease who doesn’t really have it.

Now we are finally ready to talk about ROC curves. The ROC curve gives us a way of graphically summarizing the information in Output 3.17. It also provides the basis for calculating a single statistic that assesses the predictive power of the model and does not depend on the cutpoint value. The ROC curve is simply a graph with sensitivity on the vertical axis and 1 minus specificity on the horizontal axis, both of which increase as the cutpoint decreases from 1 to 0. PROC LOGISTIC can produce the curve with the following code:

```
PROC LOGISTIC DATA=penalty PLOTS(ONLY)=ROC;
    MODEL death(EVENT='1')=blackd whitvic culp ;
RUN;
```

The option ONLY after the PLOTS option is included to suppress the production of influence plots that would otherwise appear by default. We’ll discuss influence plots in the next section.

The resulting ROC curve is shown in Output 3.18. The 45-degree line represents the expected ROC curve for a model with an intercept only, that is, one with no predictive power. The more the curve departs from the 45-degree line, the greater the predictive power. The standard statistic for summarizing that departure is the area under the curve, which here is reported as .8998. As noted earlier, this is the same as the c statistic that is reported in the “Association of Predicted Probabilities and Observed Responses” table. (There may be a slight difference because different methods are used to approximate the area.) So if all you want is the area under the curve, there is no need to request the curve itself. One technical note: The predicted probabilities used in the construction of the ROC curve are not biased corrected like the ones used to produce Output 3.17.

## Output 3.18 ROC Curve for Death Penalty Model

![](img/bbec4f484c16475caccf067e8da3ac57_85_0.png)

There are lots of options for ROC curves, only a few of which we can examine here. One handy option lets you put the cutpoints on the curve. That’s accomplished by changing the PLOTS option to PLOTS(ONLY)=ROC(ID=CUTPOINT), yielding the graph in Output 3.19.

## Output 3.19 ROC Curve with Cutpoints Added

![](img/bbec4f484c16475caccf067e8da3ac57_86_0.png)

Another attractive feature is the ability to compare the ROC curves and c-statistics for different models. In the following code, I request ROC curves and c-statistics for the basic model and for three different submodels, each omitting one of the model predictors:

```
PROC LOGISTIC DATA=penalty;
    MODEL death(EVENT='1')=blackd whitvic culp;
    ROC 'omit culp' blackd whitvic;
    ROC 'omit blackd' whitvic culp;
    ROC 'omit whitvic' blackd culp;
    ROCCONTRAST / ESTIMATE=ALLPAIRS;
RUN;
```

The label (enclosed in single quotes) on each ROC statement is optional, but usually helpful in interpreting the output. The three ROC statements produce separate ROC graphs for each model (not shown) and a final graph that displays all the curves in one graph (shown in Output 3.20). Note that when the program contains ROC statements, the PLOTS option is not necessary on the PROC statement. However, you may still want to use it to control some of the plotting details (like the inclusion of cutpoints).

## Output 3.20 ROC Curves for Comparing Different Models

![](img/bbec4f484c16475caccf067e8da3ac57_87_0.png)

Besides the graphs, we also get the table in Output 3.21, which reports various ordinal measures of association between observed and predicted values for the three models specified in ROC statements, as well as for the original model. “Area” is, of course, the area under the ROC curve. For that statistic we also get standard errors and 95 percent confidence intervals. From both the graph and the table, we see clearly that the variable CULP has a much stronger impact on the association measures than the other two variables.

## Output 3.21 Association Statistics for Three Different Models

| ROC Model | Area | Standard Error | 95% Wald Confidence Limits | Somers' D (Gini) | Gamma | Tau-a |
|---|---|---:|---:|---:|---:|---:|
| Model | 0.8998 | 0.0264 | 0.8481–0.9515 | 0.7996 | 0.8272 | 0.3614 |
| omit culpl | 0.5652 | 0.0469 | 0.4732–0.6571 | 0.1303 | 0.1847 | 0.0589 |
| omit blackd | 0.8713 | 0.0331 | 0.8065–0.9362 | 0.7427 | 0.7934 | 0.3357 |
| omit whitvic | 0.8918 | 0.0269 | 0.8390–0.9445 | 0.7835 | 0.8363 | 0.3541 |

The ROCCONTRAST statement enables us to test for differences in the area under the curve (*c*-statistic) for the different models, as shown in Output 3.22. We first get an overall test of the null hypothesis that the *c*-statistic is the same across all four models (the main model with all three covariates and the three submodels that omit one covariate each). Clearly that hypothesis must be rejected. Then, because I included the ESTIMATE=ALLPAIRS option, we get the difference in the *c*-statistics for each pair of models, along with its standard error, 95 percent confidence interval, and *p*-value for testing the null hypothesis that the true difference is 0. The only significant differences are between models that include CULP and models that exclude it.

## Output 3.22 Tables Produced by ROCCONTRAST Statement

| Contrast | DF | Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|
| Reference = Model | 3 | 95.6616 | <.0001 |

| Contrast | Estimate | Standard Error | 95% Wald Confidence Limits | Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|---:|---:|
| Model - omit culpl | 0.3346 | 0.0513 | 0.2341–0.4352 | 42.5659 | <.0001 |
| Model - omit blackd | 0.0285 | 0.0179 | -0.00656–0.0635 | 2.5366 | 0.1112 |
| Model - omit whitvic | 0.00804 | 0.00921 | -0.0100–0.0261 | 0.7625 | 0.3826 |
| omit culpl - omit blackd | -0.3062 | 0.0637 | -0.4310–-0.1813 | 23.1091 | <.0001 |
| omit culpl - omit whitvic | -0.3266 | 0.0510 | -0.4265–0.2267 | 41.0821 | <.0001 |
| omit blackd - omit whitvic | -0.0204 | 0.0225 | -0.0645–0.0237 | 0.8228 | 0.3644 |

## 3.9 Predicted Values, Residuals, and Influence Statistics

Next, we turn to diagnostic statistics that are computed for each individual observation. PROC LOGISTIC can produce a large number of case-wise statistics with the OUTPUT statement, which writes selected diagnostic statistics to a SAS data set. Here are some of the statistics that can be selected:

- **Linear predictor**—Predicted log-odds for each case. In matrix notation, this is xβ, so it’s commonly referred to as XBETA.
- **Standard error of linear predictor**—Used in generating confidence intervals.
- **Predicted values**—Predicted probability of the event, based on the estimated model and values of the explanatory variables. For grouped data, this is the expected number of events.
- **Confidence intervals for predicted values**—Confidence intervals are first calculated for the linear predictor by adding and subtracting an appropriate multiple of the standard error. Then, to get confidence intervals around the predicted values, the upper and lower bounds on the linear predictor are substituted into 1/(1+ e^(-x)), where x is either an upper or a lower bound.
- **Deviance residuals**—Contribution of each observation to the deviance chi-square.
- **Pearson residuals**—Contribution of each observation to the Pearson chi-square.

For the last two statistics, standardized versions are available in SAS 9.3 and later.

Obviously, the residuals may be useful in determining which observations are poorly fit by the model. But since the dependent variable can only take on values of 0 or 1, the utility of residuals is somewhat limited. A high residual would mean that the individual had the event, even though the predicted probability of the event was low. But we know that low probability events do happen sometimes, so this doesn’t necessarily mean a failure of the model, or that something is amiss with that individual. For example, using the model for the death penalty data with CULP, WHITVIC, and BLACKD as predictors, person 10 had both the largest deviance residual (-2.38) and the largest Pearson residual (-4.00). That person did not get the death penalty even though his predicted probability was .95.

The OUTPUT statement can also produce several statistics that are designed to measure the influence of each observation. Basically, influence statistics tell you how much

