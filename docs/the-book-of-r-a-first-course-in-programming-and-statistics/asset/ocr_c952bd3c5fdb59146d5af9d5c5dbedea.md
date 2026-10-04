lm(formula = Height ~ Wr.Hnd + Sex + Smoke, data = survey)

# Coefficients:

| | Wr.Hnd | SexMale | SmokeNever | SmokeOccas | SmokeRegul |
|---|---|---|---|---|---||
| (Intercept) | 137.4056 | 1.6042 | 9.3979 | -0.0442 | 1.5267 | 0.9211 |

Once you have fitted your nested models, R can carry out partial F-tests using anova function (partial F-tests fall within the suite of analysis of variance methodologies). To determine whether adding Smoke as a predictor provides any statistically significant improvement in fit, simply start with the reduced model and supply the model objects as arguments.

# R anova(survmult, survurtz)
Analysis of Variance Table

+   * Model 1: Height ~ Wr.Hnd + Sex
* Model 2: Height ~ Wr.Hnd + Sex + Smoke
* Res.Df RS DF of Sum Sq F Pr(>F)
1 204 9959.2
2 201 9914.3 44.8736 0.3033 0.823

The output provides the quantities associated with calculation of $R^2_{reduced}$ and $R^2_{full}$ and the test statistic $F$ from (22,2), giving in the resulting table as $F$, which is of most useful. Using the values of $p$ and $q$ from printing survmult and survurtz, you should also confirm, for example, the values of $df1$ and $df2$ appearing in the second row of the table in the columns Df and Res.Df, respectively.

The result of this particular, obtained from a test statistic of $F = 0.3033$ with $df1=3, df2=201$, is a high $p$-value of 0.823, suggesting no evidence against $H_0$. This means that adding Smoke to the reduced model, which includes only the explanatory variables Wr.Hnd and Sex, offers no tangible improvement in fit when it comes to modeling student height. That conclusion isn't surprising, given the insignificant $p$-values of all nonlinear levels of Smoke, previously seen in Section 21.3.1.

This is how F-tests are used for model selection—in the current example, the reduced model would be the more parsimonious fit and preferred over the full model.

You can conduct comparisons among several models in a given call to anova, which can be useful for investigating such things as the inclusion of interactive terms or polynomial transformations of predictors before there's a natural hierarchy requires you to retain any lower-order terms.

For example, let's use the *diabetes* data frame in the gateway package to predict cholesterol level (chol) against age (age) and body frame (frame) and the interaction between those two predictors. Before using the partial F-tests to compare variants, you need to ensure you're using the same records for each model and that

Linear Model Selection and Diagnostics 531