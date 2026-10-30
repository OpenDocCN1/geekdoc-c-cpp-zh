
**TABLE 6.1: Linearity Likelihood for Math, Science, and Engineering Data; Devore**

| Correlation ρ | Relationship |
|---|---|
| 0.8 < |ρ| ≤ 1.0 | Strong linear relationship |
| 0.5 < |ρ| ≤ 0.8 | Moderate linear relationship |
| 0.0 ≤ |ρ| ≤ 0.5 | Weak linear relationship |

**TABLE 6.2: Linearity Likelihood for Non-Math, Non-Science, and Non-Engineering Data; Johnson**

| Correlation ρ | Relationship |
|---|---|
| 0.5 < |ρ| ≤ 1.0 | Strong linear relationship |
| 0.3 < |ρ| ≤ 0.5 | Moderate linear relationship |
| 0.1 ≤ |ρ| ≤ 0.3 | Weak linear relationship |
| 0.0 ≤ |ρ| ≤ 0.1 | No linear relationship |

In our modeling efforts, we emphasize the interpretation of ρ ≈ 0. A very small correlation coefficient can be interpreted as indicating either no linear relationship or the existence of a nonlinear relationship. Many neophyte analysts fail to pick up on the importance of potential nonlinear relationships in their interpretation.

Let’s look at an example where we attempt to fit a linear model to data that may not be linear.

## Example 6.1. Exponential Decay.

Build a mathematical model to predict the degree of recovery after discharge for orthopedic surgical patients. There are two variables: time t in days in the hospital, and a medical prognosis index for every v with larger values indicating a better prognosis. The data in Table 6.3 comes from Neter et al. [NKNW1996, p. 469].

**TABLE 6.3: Hospital Stay vs. Recovery Index Data**

| t | 2 | 5 | 7 | 10 | 14 | 19 | 26 | 31 | 34 | 38 | 45 | 52 | 53 | 60 | 65 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| y | 54 | 50 | 45 | 37 | 35 | 25 | 20 | 16 | 18 | 13 | 8 | 11 | 8 | 4 | 6 |

First, a scatterplot of the data.

```
t := [2, 5, 7, 10, 14, 19, 26, 31, 34, 38, 45, 52, 53, 60, 65];
y := [54, 50, 45, 37, 35, 25, 20, 16, 18, 13, 8, 11, 8, 4, 6];
Pts := zip((x, y) → [x, y], t, y);
```

```
pointplot(Pts, labels = [days, ‘Recovery Index‘], labeldirections =
  [horizontal, vertical], title = "Hospital Stay vs. Recovery Index");
```

![](img/0f04050177d82aebd17d3383d7334896_255_0.png)

The scatterplot shows a clear negative trend.

Check the correlation ρ.

```
ρ := Statistics:-Correlation(t, y);
‘R² := ρ²;

ρ := −0.941052825413336
R² := 0.885580420218423
```

Using either rule of the thumb, the correlation coefficient ρ = −0.94 indicates a strong linear relation. With this value in hand, looking at the scatterplot leads us to think we will have an excellent linear regression model.

Let’s determine the linear model, calling it RI.

```
Statistics:-Fit(a · x + b, t, y, x);
RI := unapply(evalf(%, 6), x);
RI := x ↦ −0.752508 x + 46.4604
```

It’s time for diagnostics. Calculate the residuals and percent relative errors, then plot the residuals.

```
Residuals := [seq(yᵢ − RI(tᵢ), i = 1..15)]:
```

```
RelErr := [seq(Residualsᵢ / yᵢ · 100, i = 1..15)];
```

Look at the worst percent relative error values.

```
SRE := sort(RelErr);
SRE[1..2], SRE[-2.. -1];
[-57.46925000, -44.5707500], [67.25200000, 140.8770000]
```

```
plotplot(ResidualPts, symbol = soliddiamond, symbolsize = 16,
    title = "Residuals");
```

![](img/0f04050177d82aebd17d3383d7334896_256_0.png)

We’ve obtained the model, $y = f(t) = 49.4601 - 0.75251t$. The sum of squared error is 451.1945, the correlation is −0.94, and $R^2$, the coefficient of determination which is the correlation coefficient squared, is 0.886. These are all indicators of a “good” linear model.

But...

Although some percent relative errors are small, others are quite large, with eight of the fifteen over 20%. The largest two positive errors are ≈ 67% and 140%, and the largest two negative errors are ≈ −45% and −57%. How much confidence would you have in making predictions with this model? The residual plot clearly shows a curved pattern. The residuals and percent relative errors show that we do not have an adequate model. Advanced courses in statistical regression will show how to attempt to correct this inadequacy.

Further, suppose we need to predict the index when time was 100 days.

```
RI(100);
−28.790400
```

A negative value is clearly unacceptable and makes no sense in the context of our problem since the index is always positive. This model does not pass the common sense test.

With a strong correlation of −0.94, what went wrong? The residual plot diagnostic shows a curved pattern. In many regression analysis books, the

suggested first-attempt cure for a curved residual is adding a nonlinear term that is missing from the model. Since we only have (t, y) data points, we’ll add a nonlinear term a2x² to the model.

## Example 6.2. Multiple Linear Regression.

Fit a parabolic model f(x) = a0 + a1x + a2x² to the Hospital Stay vs. Recovery Index Data of Table 6.3.

This model, although a parabola, is linear in the “variables” a0, a1, and a2.

Let’s find the fit with Maple.

```
> with(Statistics):
> Fit(a0 + a1·x + a2·x², t, y, x):
> QF := unapply(evalf(%), x);
QF := x -> 55.82 − 1.710x + 0.01481x²
```

Use the formula R S = 1 − S S E / S S T to compute R², the coefficient of determination for the quadratic fit.

```
> SSE := sum((y_i − QF(t_i))², i = 1..15);
> μ := Mean(y):
> SST := sum((y_i − μ)², i = 1..15);
SSE := 72.34557123
SST := 3943.333333
> RSq := 1 − SSE/SST;
RSq := 0.9816537013
```

These diagnostics look quite good. The sum of the squares of the errors is much smaller. The coefficient of determination R² is larger, and the correlation has increased to 0.99.

Let’s plot the new residuals to see if there is still a curved pattern.

```
> QRResidualPts := [seq([t_i, y_i − QF(t_i)], i = 1..15)]:
```

## A ridiculous value!

Care must be taken with the selection of the initial values for the unknown parameters (see, e.g., Fox [Fox2012]). Maple yields good models when the calculations are based upon good input parameters. How can we get reasonable approximations to a0 and a1? Let’s use a standard technique: transform the model to make it linear. Apply logs to our model.

y = a0 e^{a1 x}
ln(y) = ln(a0 e^{a1 x})
= ln(a0) + a1 x

Relabel ln(y) = Y and ln(a0) = A0 to obtain
Y = A0 + a1 x

Now use Maple to fit the transformed model.

```
> LinearFit(A0 + a1·x, t, ln~(y), x);
4.03715886613379 - 0.0379741808112946·x
```

Good estimates to use for the parameters are
 a0 = e^{A0} = 56.667 and a1 = -0.03797.

```
> NonlinearFit(a0·exp(a1·x), t, y, x,
initialvalues = [a0 = 56.667, a1 = -0.03797]);
NEDF := unapply(evalf(%,5), x);
NEDF(100);
NEDF := x ↦ 58.607 e^{-0.039586 x}
1.118797159
```

This prediction is much closer to what we expect. A common technique used to test the result is to recompute the model with different, but close, initial values. Try it!

Note how close the nonlinear-fitted parameter values are to the estimates. The difference comes from where least squares is applied in the computation: to the logs of data points, rather than to the points. Write the general least squares formulas for the model and the transformed model to see the difference. Also, compare the model from Maple’s ExponentialFit to the one we have found.

For a nonlinear model, linear correlation and R² have no meaning. Computing the sum of squared error gives SSE = 45.495. This value is substantially smaller than SSE = 451.1945 obtained by the linear model. The nonlinear model appears reasonable. Now check the nonlinear model’s residual plot for patterns.

```
> EDResidualPts := [seq([ti, yi - NEDF(ti)], i = 1..15)]:
```

```
> plotpoint(EDResidualPts, symbol = soliddiamond, symbolsize = 16,
>     title = "Exponential Decay Fit’s Residuals");
```

![](img/0f04050177d82aebd17d3383d7334896_260_0.png)

[Figure 6.3] shows the exponential decay model overlaid on the data

![](img/0f04050177d82aebd17d3383d7334896_260_1.png)

FIGURE 6.3: Exponential Decay Fit to Hospital Recovery Data

The percent relative errors are also much improved—only four are larger than 20%, and none are beyond 36.3%. Verify this!
