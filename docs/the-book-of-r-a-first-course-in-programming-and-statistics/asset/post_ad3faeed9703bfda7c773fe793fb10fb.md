
goodness-of-fit. The real question, however, is whether improvement in goodness-of-fit is large enough to make the additional complexity involved with including any additional predictor terms "worth it." This is precisely the question that the partial F-test tests to answer in the context of nested regression models. Its goal is to test whether these extra $q - p$ terms, which produce the full model rather than the reduced model, provide a statistically significant improvement in goodness-of-fit. The partial F-test addresses these hypotheses:

```
$H_0 : \beta_{p+1} = \beta_{p+2} = \dots = \beta_q = 0$
$H_A : \text{At least one of the } \beta_j \neq 0 \quad(\text{for } j = p, \dots, q)$ (22.1)
```

The calculation of the test statistic to address these hypotheses follows the same ideas behind the omnibus F-test automatically by R when summarizing a fitted linear model (detailed in Section 21.3.5). Denote the coefficient of determination for the reduced and full models with $R^2_{redu}$ and $R^2_{full}$, respectively. If $n$ refers to the sample size of the data used to fit both models, the test statistic given by

```
$\mathcal{F} = \frac{(R^2_{full} - R^2_{redu})(n - q - 1)}{(1 - R^2_{full})(q - p)}$$ (22.2)
```

follows an F distribution with $df = q - p, df = n - q$ degrees of freedom under the assumption of $H_0$ in (22.1). The $p$-value is found as the upper-tail area from $F$ as usual; the smaller it is, the greater the evidence against the null hypothesis, which states that one or more of the additional parameters have impact on the response variable.

Take the model objects survmult and survmult2 from Section 21.3.1 as an example. The survmult model aims to predict mean student height from writing hands and sex based on the survey data from the MASS package; survmult adds smoking status to these predictors. If you need to, return to Section 21.3.1 to refit these models. Printing the objects to the console screens the two fits and makes it easy to confirm that the smaller model is needed within the larger model in terms of its explanatory variables:

```
R survmult
```

```
Call:
lm(formula = Height ~ Wr.Hnd + Sex, data = survey)
```

Coefficients:
| | Wr.Hnd | SexMale |
|---|---|---|
| (Intercept) | 1.594 | 9.490 |

```

```
R survmult2
Call:
```
lm(formula = Height ~ Wr.Hnd + Sex + Smoke, data = survey)

# Coefficients:
```

| | Wr.Hnd | SexMale | SmokeNever | SmokeOccas | SmokeRegul |
|---|---|---|---|---|---|
| (Intercept) | 137.4056 | 1.6042 | 9.3979 | -0.0442 | 1.5267 | 0.9211 |
```

Once you have fitted your nested models, R can carry out partial F-tests using `anova` function (partial F-tests fall within the suite of analysis of variance methodologies). To determine whether adding Smoke as a predictor provides any statistically significant improvement in fit, simply start with the reduced model and supply the model objects as arguments.

```R
R anova(survmult, survmult2)
Analysis of Variance Table
```

| | Model 1: Height ~ Wr.Hnd + Sex | Model 2: Height ~ Wr.Hnd + Sex + Smoke |
| Res.Df | RS | DF of Sum Sq | F | Pr(>F) |
|---|---|---|---|---|
| 1 | 204 | 9959.2 | | |
| 2 | 201 | 9914.3 | 44.8736 | 0.3033 | 0.823 |

The output provides the quantities associated with calculation of $R^2_{reduced}$ and $R^2_{full}$ and the test statistic $F$ from (22.2), giving in the resulting table as $F$, which is of most useful. Using the values of $p$ and $q$ from printing survmult and survmult2, you should also confirm, for example, the values of $df1$ and $df2$ appearing in the second row of the table in columns Df and Res.Df, respectively. The result of this particular, obtained from a test statistic of $F = 0.3033$ with $df1=3, df2=201$, is a high $p$-value of 0.823, suggesting no evidence against $H_0$. This means that adding Smoke to the reduced model, which only the explanatory variables Wr.Hnd and Sex, offers no tangible improvement in fit when it comes to modeling student height. That conclusion isn't surprising, given the insignificant $p$-values of all levels of Smoke previously seen in Section 21.3. This is how F-tests are used for model selection—in the current example, the reduced model would be the more parsimonious fit and preferred over the full model.

Before using the partial F-tests to compare variants, a natural hierarchy requires you to retain lower-order terms. You can conduct comparisons among several models in a given call to `anova`, which can be useful for investigating such things as the inclusion of interactive terms or polynomial transformations of predictors. For example, let's use the *diabetes* data to predict cholesterol level (chol) against age (age) and body frame (frame) and the interaction between those two predictors. You need to ensure you are using the same records for each model and that there are missing values for any of the predictors. To do this, you need to first define a version of diabetes that removes missing values in the predictors you are using. Use logical subsetting:

```
R> diabetes <- diabetes[-which(is.na(diabetes$frame))]
```

Now, fit the four models using your new data:

```
R> dia.model1 <- lm(chol,data=data)
R> dia.model2 <- lm(age,data=data)
R> dia.model3 <- lm(age+frame,data=data)
R> dia.model4 <- lm(chol+age+frame,data=data)
```

The first model is just an intercept, the second adds age as a predictor, the third adds age and frame, and the fourth includes the interaction. Nesting is evident, and we can now compare the significance of the improvements in goodness-of-fit as we increase the complexity of the model at each step.

```
R> anova(dia.model1,dia.model2,dia.model4)
Analysis of Variance Table
```

| | Model 1: chol ~ 1 | Model 2: chol ~ age | Model 3: chol ~ age + frame | Model 4: chol ~ age * frame |
| Res.Df | RSS | Sum of Sq | F | Pr(>F) |
|---|---|---|---|---|---|
| 1 | 389 | 747265 | | | |
| 2 | 388 | 720178 | 35187 | 19.6306 | 1.227e-05 *** |
| 3 | 386 | 697527 | 14551 | 4.0589 | 0.01801 * |
| 4 | 388 | 688295 | 9223 | 2.5755 | 0.07443 |
```

```
Signif. codes: 0 *** .001 ** .01 * .05 ' .1 ' 
```

If you hadn't deleted the records containing missing values in predictors, you would have received an error telling you that the data sets for the four models were not equal. The results suggest that including age provides a significant improvement to modeling chol; including a main effect for frame provides a further mild improvement; and there's very weak evidence, if any, that including an interactive effect is beneficial to goodness-of-fit. From this, you might prefer to use dia.model3, the main-effects-only model, as the most parsimonious representation of mean cholesterol out of these models.

## 2.2.2 Forward Selection

Partial F-tests are a natural way to investigate nested models but can be difficult to manage if you have many different models to fit, for example, you have many predictor variables.

This is where forward selection (also referred to as forward elimination) comes in. The idea is to start with an intercept-only model and then perform a series of independent tests to determine which of your predictor variables significantly improves the goodness-of-fit. Then you update your model object by adding term and execute the series of tests for all remaining terms to determine which of those would further improve the fit in a statistically significant way. The ready-to-use R functions `add` and `update` perform the series of tests and update your fitted regression model.

You'll use the nuclear data in the boot library from Exercise 21.1 on page 499 and Section 21.5.3 as an example. The goal is to choose the most informative model for prediction of cost. Load boot and access the help file nuclear to remind yourself of the variable definitions. First model for construction cost with an overall intercept term only.

```
R> lm(cost,data=nuclear)
R> summary(null)
```

```
Call:
formula = cost ~ 1, data = nuclear

Residuals:
Min Median 3Q Max
-254.05 -151.24 -13.46 150.40 419.68

Coefficients:
Estimate Std. Error t value Pr(|t|)
(Intercept) 461.56 30.07 15.35 4.95e-16 ***

Signif. codes: 0 *** .001 ** .01 * .05 ' .1

Residual standard error: 170.1 on 31 degrees of freedom
```

The first argument to add is all you are aiming to update. The second argument, scope, is critical—must supply a formula object defining the "fullest", most complex model you'd fitting. For this
