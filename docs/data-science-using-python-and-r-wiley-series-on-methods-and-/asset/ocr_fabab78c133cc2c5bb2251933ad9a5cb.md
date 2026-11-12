6. Miss the Bigger Picture. Further, analysts should try to keep an eye on the big picture, and analysis solely at the variable level might miss the fundamentals underlying relationships among the predictors. Instead, several predictors might fall naturally into a single group (a factor or component), which addresses a single aspect of the data. For example, the variables savings account balance, checking account balance, home equity, stock portfolio value, and 401 k balance might all fall together under the single component, assets.

In summary, dimension reduction methods use the correlation structure among the predictor variables to accomplish the following:

+   1. Reduce the number of predictor items.
+   2. Help ensure that these predictor items are uncorrelated.
+   3. Provide a framework for interpretability of the results.

# 12.2 MULTICOLLINEARITY

Data scientists need to guard against multicollinearity, a condition where some of the predictor variables are correlated with each other. Multicollinearity leads to instability in the solution space, leading, for example, to regression coefficients you cannot trust, because the coefficient variability is so large. Multicollinearity is an occupational hazard for data scientists, because many of the data sets have dozens if not hundreds of predictors, some of which are often correlated.

Consider Figures 12.1 and 12.2. Figure 12.1 illustrates a situation where the predictors $x_1$ and $x_2$ are not correlated with each other; that is, they are orthogonal, or independent. In such a case, the predictors form a solid basis, upon which the response surface $y$ may rest sturdily, thereby providing stable coefficient estimates $b_1$ and $b_2$ each with small variability. On the other hand, Figure 12.2 illustrates a multicollinear situation where the predictors $x_1$ and $x_2$ are correlated with each

![](bbox=[0.1, 0.65, 0.6, 0.85])

Figure 12.1 When the predictors $x_1$ and $x_2$ are uncorrelated, the response surface $y$ rests on a solid basis, providing stable coefficient estimates.