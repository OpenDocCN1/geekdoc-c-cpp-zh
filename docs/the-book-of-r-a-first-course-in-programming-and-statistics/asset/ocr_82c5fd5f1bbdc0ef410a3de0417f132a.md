| Murders | Police | Unemployment | Guns |
|---|---|---||}{
| 8.60 | 260.35 | 11.0 | 178.15 |
| 8.90 | 269.80 | 7.0 | 156.41 |
| 8.52 | 272.04 | 5.2 | 198.02 |
| 8.89 | 272.96 | 4.3 | 222.10 |
| 13.07 | 272.51 | 3.5 | 301.92 |
| 14.57 | 261.34 | 3.2 | 391.22 |
| 21.36 | 268.89 | 4.1 | 665.56 |
| 28.03 | 295.99 | 3.9 | 1131.21 |
| 31.49 | 319.87 | 3.6 | 837.60 |
| 37.39 | 341.43 | 7.1 | 794.90 |
| 46.26 | 356.59 | 8.4 | 817.74 |
| 47.24 | 376.69 | 7.7 | 583.17 |
| 52.33 | 390.19 | 6.3 | 709.59 |

+   i. Create your own data frame in your R workspace and produce a scatterplot matrix. The variables of which appears to be strongly related to the murder rate?
j. Fit a multiple linear regression model using the number of murders as the response and all other variables as predictors. Write down the model equation and interpret the coefficients. Is it reasonable to state that all relationships between the response and the predictors are causal?
k. Identify the amount of variation in the response attributed to the three explanatory variables. Then refit the model excluding the predictor with the largest (in words, "most insignificant") p-value. Compare the new coefficient of determination with that of the previous model. Is there much difference?
j. Use your model from (k) to predict the mean number of murders for 100,000 residents, with 300 police officers and 500 issued gun licenses. Compare this to the mean response if there were no gun licenses issued and provide 99 percent confidence intervals for both predictions.

# ## 21.4 Transforming Numeric Variables

Sometimes, the linear function as strictly defined by the standard regression equation, (21.1), can be inadequate when it comes to capturing relationships between a response and selected covariates. You might, for example, observe curvature in a scatterplot between two numeric variables to which a perfectly straight line isn't necessarily best suited. To a certain extent, the