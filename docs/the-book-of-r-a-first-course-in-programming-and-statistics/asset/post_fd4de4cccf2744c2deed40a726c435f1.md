
![](img/b2cfc85cbb129f60fe595a2bae074fe4_537_0.png)

Figure 21-3: Scatterplot of miles per gallon and engine displacement, for the mtcars data

Is the straight line that a simple linear regression model would provide the best way to represent this relationship? To investigate this, start by fitting that simple linear setup.

```R
R> car.order1 <- lm(formula = mpg~disp,data=mtcars)
R> summary(car.order1)
```

Call:
lm(formula = mpg ~ disp, data = mtcars)

Residuals:
Min 1Q Median 3Q Max
-4.8922 -2.2022 -0.9631 1.6272 7.2305

Coefficients:
Estimate Std. Error t value Pr(>|t|)
(Intercept) 29.59985 1.229720 24.070 < 2e-16 ***
disp -0.041215 0.004712 -8.747 9.38e-10 ***

Signif. codes: 0 '***' 0.001 '**' 0.01 '*' 0.05 '*' 0.1 '*'
Residual standard error: 3.251 on 30 degrees of freedom
Multiple R-squared: 0.7183, Adjusted R-squared: 0.709
F-statistic: 76.51 on 1 and 30 DF, p-value: 9.38e-10

This clearly indicates statistical evidence of a negative linear impact of displacement—for each cubic inch of displacement, the mean response decreases by about 0.041 miles per gallon.

Now, try to capture the apparent curve in the data by adding a quadratic term to the model. You can do this in two ways. First, you could create a new vector in the workspace by squaring the mtcars$disp vector and supplying the result to the formula in lm. Second, you could specify disp2 directly as an additive term in the formula. If you do this, it's essential to wrap that expression in a call to I as follows:

```R
R> car.order2 <- lm(mpg~disp+I(disp^2),data=mtcars)
R> summary(car.order2)
```

Call:
lm(formula = mpg ~ disp + I(disp^2), data = mtcars)

Residuals:

| Min | 1Q | Median | 3Q | Max |
|---|---|---|---|---|
| -3.9112 | -1.5269 | -0.3124 | 1.3489 | 5.3946 |

Coefficients:

| Estimate | Std. Error | t | Pr(>|t|) |
|---|---|---|---|
| (Intercept) | 3.583e+01 | 2.209e+00 | 16.221 | 4.39e-06 *** |
| disp | -1.053e-01 | 2.028e-02 | -5.192 | 1.49e-05 *** |
| I(disp^2) | 1.255e-04 | 3.891e-05 | 3.226 | 0.0031 ** |

Signif. codes: 0 *** 0.001 ** 0.01 * 0.05 . 0.1 ' 1

Residual standard error: 2.837 on 29 degrees of freedom
Multiple R-squared: 0.7927 Adjusted R-squared: 0.7784
F-statistic: 55.46 on 29 and 29 DF, p-value: 1.22e-10

Using the function around a given term in the formula is necessary when said term requires an arithmetic calculation—in this case, disp2—before the model itself is actually fitted.

Turning to the fitted model regression model itself, you can see that the contribution of the squared component is statistically significant—the output to I(disp^2) shows a p-value of 0.0031. This implies that even if a linear trend is taken into account, the model that includes a quadratic component (which introduces a curve) is a better-fitting model. This conclusion is supported by a noticeably higher coefficient of determination compared to the first fit (0.7927 against 0.7183). You can see the fit of this quadratic curve in Figure 21-4 (which follows shortly).

Here you might reasonably wonder whether you can improve the ability of the model to capture the relationship further by adding yet another higher-order term in the covariate of interest. To that end:

```R
R> car.order3 <- lm(mpg~disp+I(disp^2)+I(disp^3),data=mtcars)
R> summary(car.order3)
```

Call:
lm(formula = mpg ~ disp + I(disp^2) + I(disp^3), data = mtcars)

Residuals:

| Min | 1Q | Median | 3Q | Max |
|---|---|---|---|---|
| -3.0896 | -1.5653 | -0.3619 | 1.4368 | 5.7617 |

Coefficients:

| Estimate | Std. Error | t value | Pr(>|t|) |
|---|---|---|---|
| (Intercept) | 5.070e+02 | 3.809e+02 | 13.310 | 1.25e-13 *** |
| disp | -3.372e-01 | 5.526e-02 | -6.102 | 1.39e-06 *** |
| I(disp^2) | 1.109e-03 | 2.265e-04 | 4.897 | 3.685e-05 *** |
| I(disp^3) | -1.217e-02 | 2.776e-07 | -4.382 | 0.0015 *** |

Signif. codes: 0 *** 0.001 ** 0.01 * 0.05 0.1

Residual standard error: 2.22 on 28 degrees of freedom
Multiple R-squared: 0.8771, Adjusted R-squared: 0.8639
F-statistic: 66.58 on 3 and 28 DF, p-value: 7.34e-13

The output shows that a cubic component also offers a statistically significant term. However, if you were to continue adding higher-order terms, you would find that a polynomial of order 4 to these data isn't improve the fit at all, with several coefficients being insignificant (4th order not shown). So, letting $\hat{y}$ be miles per gallon and $x$ be displacement in cubic inches, and expanding the notation from the previous output, the fitted multiple regression:
$\hat{y} = 50.7 - 0.3372x + 0.0011x^2 - 0.00001x^3$
which is precisely what the order 3 line in the left panel of Figure 21-4 reflects.

# Plotting the Polynomial Fit

To address the plot itself in the usual way, you visualize the data and the first (simple linear) model in car.order1 in the usual way. To begin Figure 21-4, execute the following code:

```R
R> plot(mtcars$disp,mtcars$mpg,xlab="Displacement (cu. in.)",ylab="MPG")
R> abline(car.order1)
```

![](img/b2cfc85cbb129f60fe595a2bae074fe4_540_0.png)

**Figure 21-4:** Three models, polynomials of order 1, 2, and 3, fitted to the "mileage displacement" relationship from the mtcars data set. Left: plot limits constrained to the data. Right: plot limits widened to illustrate unreliability in extrapolation.

It's a little more difficult to add the line corresponding to either of the polynomial models equipped to handle only straight-line trends. One way to do this is to make use of predict for each value in a sequence that represents the desired values of the explanatory variable. (I favor this approach because it allows you to simultaneously calculate confidence and prediction bands if you want.) To add the line for the order 2 model only, first create the required observed range of disp.

```R
R> disp.seq <- seq(min(mtcars$disp)-50,max(mtcars$disp)+50,length=30)
```

Here, the sequence has been widened by minus and plus 50 to predict a small amount on either side of the scope of the original data, so the curve meets the edges of the graph. Then you make the prediction itself and superimpose the fitted line.

```R
R> car.order2.pred <- predict(car.order2,newdata=data.frame(disp=disp.seq))
R> lines(disp.seq,car.order2.pred,lty=2)
```

You use the same technique, followed by the final addition of the legend, for order 3 model.

```R
R> car.order3.pred <- predict(car.order3,newdata=data.frame(disp=disp.seq))
R> lines(disp.seq,car.order3.pred,lty=3)
R> legend("topright","order 1 (linear)")
```

The result of this is on the left panel of Figure 21-4. When you've read data from only one covariate, disp, the example illustrated is considered multiple regression more than one (in addition to the universal intercept $\beta_0$) required estimation in the order 2 and 3 models.

The different types of trend lines fitted to the mileage and displacement clearly show different interpretations of the relationship. Actually, you could reasonably argue that the simple linear fit is inadequate at modeling the relationship between response and predictor, but it's harder to come to a clear conclusion when choosing between the order 2 and 3 versions. The order 2 fit captures the curve that tapers off as $disp$ increases; the order 3 fit allows for a bump (in technical terms a saddle or inflection), followed by a steeper downward trend in the same domain.

So, which model is “best?” In this case, the statistical significance of the parameters suggests that the order 3 model should be preferred. Having said that, there are other things to consider when choosing different models, you'll think more carefully in Section 22.2.

# Pitfalls of Polynomials

One particular drawback associated with polynomial terms in linear regression models is the instability of the fitted trend when trying to perform any extrapolation. The right plot in Figure 21-4 shows the three models (MPG by displacement), but this time with a much wider scale for displacement. As you can see, the validity of these models is questionable—although the order 2 and 3 models fit acceptably within the range of the data, if you move even slightly outside the maximum displacement values, the predictions of the mean mileage go wildly off. You must keep this mathematical behavior of polynomial functions in mind if you're considering higher-order terms in your regression models.

# 21.4.2 Logarithmic

In statistical modeling situations where you have positive numeric observations, it's common to perform a log transformation of the data to dramatically reduce the overall range of the data and bring extreme
