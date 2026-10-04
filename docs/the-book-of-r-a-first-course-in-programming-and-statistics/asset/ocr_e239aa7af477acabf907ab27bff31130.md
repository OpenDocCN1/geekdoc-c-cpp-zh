Here you might reasonably wonder whether you can improve the ability of the model to capture the relationship further by adding yet another higher-order term in the covariate of interest. To that end:

```
R car.order3 <- lm(mpg$disp+I(disp^2)+I(disp^3),data=mtcars)
R summary(car.order3)
```

Call:

```
lm(formula = mpg ~ disp + I(disp^2) + I(disp^3), data = mtcars
```

Residuals:

| Min | 1Q | Median | 3Q | Max |
|---|---|---|---||}{
| -3.0896 | -1.5653 | -0.3619 | 1.4368 | 5.7617 |

Coefficients:

| Estimate | Std. | t value | Pr(|t|) |
|---|---|---|---||}{
| (Intercept) | 5.070e+02 | 3.809e+02 | 13.310 | 1.25e-13 *** |
| disp | -3.372e-01 | 5.526e-02 | -6.102 | 1.39e-06 *** |
| I(disp^2) | 1.109e-03 | 2.265e-04 | 4.897 | 3.685e-05 *** |
| I(disp^3) | -1.217e-02 | 2.776e-07 | -4.382 | 0.00015 *** |

Signif. 0 *** 0.001 ** 0.01 * 0.05 ' ' 1

Residual standard error: 2.22 on 28 degrees of freedom
Multiple R-squared: 0.8771, Adjusted R-squared: 0.8639
F-statistic: 66.58 on 3 and 28 DF, p-value: 7.347e-13

The output shows that a cubic component also offers a statistically significant term. However, if you were to continue adding higher-order terms, you would find that a polynomial of 4 to these data isn't to improve the fit at all, with several coefficients being rendered nonsignificant (the 4th order not shown).

So, letting $\hat{y}$ be miles per gallon and $x$ be displacement in cubic inches, and expanding the e-notation from the previous output, the fitted multiple regression

```
$\hat{y} = 50.7 - 0.03372x + 0.0011x^2 - 0.000001x^3$
```

which is precisely what the order 3 line in the left panel of Figure 21-4 reflects.

# Plotting the Polynomial Fit

To address the plot itself in the usual way, you visualize the data and the first (simple linear) model in car.order1 in the usual way. To begin Figure 21-4, execute the following code:

```
R plot(mtcars$disp,mtcars$mpg,xlab="Displacement (cu. in.)",ylab="MPG"
R abline(car.order1)
```