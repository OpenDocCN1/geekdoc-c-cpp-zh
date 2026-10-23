
# Regression Reports

Regression reports give textual information about the fit.

## The Summary of Fit Table

The Summary of Fit table appears first and shows the following numeric summaries of the response for the multiple regression model:

**Rsquare** (*R²*) estimates the proportion of the variation in the response around the mean that can be attributed to terms in the model, rather than to random error.

It is also the square of the correlation between the actual and predicted response. An *R²* of 1 occurs when there is a perfect fit (the errors are all zero). An *R²* of 0 means that the fit predicts the response no better than the overall response mean.

**Rsquare Adj** adjusts *R²* to make it more comparable over models with different numbers of parameters. Since adding terms to an existing model always increases *R²*, this adjustment compensates for adding terms to a model that already has terms in it. It is a ratio of mean squares instead of sums of squares.

**Root Mean Square Error** estimates the standard deviation of the random error. It is the square root of the mean square for error in the corresponding analysis of variance table, and it is commonly denoted as *s*.

The **Mean of Response** is the overall mean of the response values. It is important as a base model for prediction because all other models are compared to it. The variance measured around this mean is the **Corrected Total (C Total)** mean square in the Analysis of Variance table.

**Observations (or Sum of Weights)** records the number of observations used in the fit. If there are no missing values and no excluded rows, this is the same as the number of rows in the data table. If there is a column assigned the role of weight, this is the sum of that column’s values. Weights are used in weighted least squares — an advanced topic.

## The Analysis of Variance Table

The Analysis of Variance table shows the basic calculations for a linear model. The table compares the model to a model containing only the mean:

**Source** lists the three sources of variation, called **Model**, **Error**, and **C Total**.

**DF** records an associated degrees of freedom for each source of variation.

The **C Total** degrees of freedom is for the simple mean model. There is only one degree of freedom used (the estimate of the mean parameter) in the calculation of variation, so the **C Total DF** is always one less than the number of observations.

The total degrees of freedom are partitioned into the **Model** and **Error** terms:

- The **Model** degrees of freedom is the number of parameters (except for the intercept) used to fit the model.
- The **Error DF** is the difference between the **C Total DF** and the **Model DF**.

**Sum of Squares** records an associated sum of squares for each source of variation. Each is the sum of squares of the differences between the fitted response and the actual response.

- The **Total (C Total) SS** is the sum of squared distances of each response from the sample mean.
- The **Error SS** is the sum of squared differences between the fitted values and the actual values. This sum of squares corresponds to the unexplained error (residual) after fitting the regression model.

A **Mean Square** is a sum of squares divided by its associated degrees of freedom. This computation converts the sum of squares to an average.

The **F Ratio** is the model mean square divided by the error mean square. It tests the hypothesis that all the regression parameters (except the intercept) are zero. If there is a significant effect in the model, the F Ratio is higher than expected by chance alone.

**Prob>F** is the probability of obtaining a greater F value by chance alone if the specified model fits no better than the overall response mean. Significance probabilities of 0.05 or less are often considered evidence that there is at least one significant regression factor in the model.

Note that large values of Model SS and small values of Error SS lead to large F ratios and low *p* values—desirable if the goal is to declare that terms in the model are significantly different from zero. Most practitioners check this F test first and make sure that it is significant before delving further into the details of the fit. This significance is also shown graphically by the whole-model leverage plot, described in “Leverage Plots,” p. 91.

## The Lack of Fit Table

The Lack of Fit table shows a special diagnostic test and appears only when the data and the model provide the opportunity. Sometimes, it is possible to estimate the error variance independently of whether the right form of the model is the one under consideration. This occurs when observations are exact replicates of each other in terms of the X variables. The error for these exact replicates is called *pure error*. This is the portion of the sample error that cannot be explained or predicted no matter which form the model uses for the X variables.

The difference between the residual error from the model and the pure error is called *lack of fit error*. A lack of fit error can be significantly greater than pure error if a regressor is in the model with the wrong functional form, or if too few interaction effects exist in an analysis of variance model. In these cases, consider adding interaction terms, if appropriate, to try to better capture the functional form of a regressor.

There are two common situations where there is no lack of fit test:

- There are no exactly replicated points with respect to the X data, and therefore there are no degrees of freedom for pure error.
- The model is saturated, meaning that the model itself has a degree of freedom for each different X value; therefore, there are no degrees of freedom for lack of fit.

The Lack of Fit table shows information about the error terms:

**Source** lists the three sources of variation called **Lack of Fit**, **Pure Error**, and **Total Error**. Note that the pure error DF is pooled from each group where there are multiple rows with the same values for each effect.

The remaining portions of the Lack of Fit table are similar to those of the Analysis of Variance Table. The only additional information is the **Max RSq**, the maximum *R²* that can be achieved by using only the variables in the model.

Figure 5.7 Example Leverage Plot from Denim Data

![](img/a858f3b35ed4923af65c22e8829ee5a8_92_0.png)

In addition, there is a special leverage plot titled Whole Model that shows the actual values of the response plotted against the predicted values. This Whole Model leverage plot dramatizes the test that all the parameters (except intercepts) in the model are zero. This illustrates the same test reported in the Analysis of Variance report.

In general, the horizontal line on the plot represents what the values of the model would be if the effect was removed from the model. The sloped line represents the values of the model with the effect included. Significance of the effect is seen by comparing the slope of the sloped line with that of the horizontal one, as in Figure 5.9.

Figure 5.8 General Leverage Plot

![](img/a858f3b35ed4923af65c22e8829ee5a8_92_1.png)

points farther out pull on the line of fit with greater leverage than the points near the middle

Figure 5.9 Significance of Effects

![](img/a858f3b35ed4923af65c22e8829ee5a8_92_2.png)

Significant
confidence curve crosses horizontal line

Borderline
confidence curve asymptotic to horizontal line

Not Significant
confidence curve does not cross horizontal line

confidence curve crosses horizontal line

confidence curve asymptotic to horizontal line

confidence curve does not cross horizontal line

## Effect Details

In a Standard Least Squares analysis, the following effect details are available, dealing with *least squares means*, designated LS Means by JMP Student Edition. More detailed descriptions of each command are available in the online help.

**Figure 5.10**  Effect Details

![](img/a858f3b35ed4923af65c22e8829ee5a8_93_0.png)

- **LS Means Table** shows predicted values from the specified model across the levels of a categorical effect. The other model factors are *controlled*—that is, set to neutral values. Least squares means shows which levels produce higher or lower responses, holding the other variables in the model constant. Least squares means are also called *adjusted means* or *population marginal means*.
- **LS Means Plot** plots the LSMeans for nominal and ordinal main effects and two-way interactions.
- **LS Means Contrast** displays a dialog for specifying contrasts with respect to an effect. (See “Linear Contrasts,” p. 84 for an example of using contrasts.) This command is enabled only for categorical effects. To construct a contrast, click the + and - buttons beside the levels to be compared. If possible, the dialog normalizes after each click to make the sum for a column zero and the absolute sum equal to two after each click. It adds to the plus or minus score proportionately.
- The **LS Means Student’s t** command requests multiple comparison tests.

## Exploring the Estimates

The following commands allow you to further explore the estimated coefficients of the model.

### Expanded Estimates

The standard Fit Model output includes a Parameter Estimates Table, as seen in Figure 5.11. For continuous effects, the estimates are the (estimated) coefficients of each term in the linear model. For nominal effects, the estimates are the coefficients of dummy variables whose value is 1 for all levels of the variable except the last, which gets the value -1. Ordinal effects show coefficients for dummy variables that measure the difference at levels of the variable from the mean of all levels of the effect.

**Figure 5.11**  Parameter Estimates Table

| Term | Estimate | Std Error | t Ratio | Prob>|t| |
|---|---|---:|---:|---:|---:|
| Intercept | 16.964153 | 2.727789 | 6.22 | <.0001* |
| Method[Alpha Analyze] | -6.132609 | 1.155205 | -5.31 | <.0001* |
| Method[Caustic Soda] | 4.552406 | 1.146512 | 3.97 | 0.0001* |
| Size of Load (lbs) | 0.0465825 | 0.014287 | 3.26 | 0.0016* |
| Sand blasted?[no] | -1.800295 | 0.814471 | -2.21 | 0.0295* |

The **Expanded Estimates** command shows the same information, but with a coefficient for each continuous variable and each level of other variables.
