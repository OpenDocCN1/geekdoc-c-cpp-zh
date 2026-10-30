
# Exercises

In Exercises 1 through 4 compute the correlation coefficient and then fit the following data with the given models using linear regression.

- 1. x | 1 2 3 4 5
  y | 1 1 2 2 4
  (a) y = a + bx
  (b) y = a x²

- 2. Data from stretching a spring:
  x (×10⁻³) | 5 10 20 30 40 50 60 70 80 90 100
  y (×10⁵) | 0 19 57 94 134 173 216 256 297 343 390
  (a) y = a x
  (b) y = a + b x
  (c) y = a x²

- 3. Data for the ponderosa pine:
  x | 17 19 20 22 23 25 28 31 32 33 36 37 39 42
  y | 19 25 32 51 57 71 113 140 153 187 192 205 250 260
  (a) y = a x
  (b) y = a + b x
  (c) y = a x²
  (d) y = a x³
  (e) y = a₃ x³ + a₂ x² + a₁ x + a₀

- 4. Fit the model y = a x^{3/2} to Kepler's planetary data:

| Body | Period | Distance from sun (m) |
|------|--------|-----------------------|
| Mercury | 7.60 × 10⁶ | 5.79 × 10¹⁰ |
| Venus | 1.94 × 10⁷ | 1.08 × 10¹¹ |
| Earth | 3.16 × 10⁷ | 1.5 × 10¹¹ |
| Mars | 5.94 × 10⁷ | 2.28 × 10¹¹ |
| Jupiter | 3.74 × 10⁸ | 7.79 × 10¹¹ |
| Saturn | 9.35 × 10⁸ | 1.43 × 10¹² |
| Uranus | 2.64 × 10⁹ | 2.87 × 10¹² |
| Neptune | 5.22 × 10⁹ | 4.5 × 10¹² |

As noted before, good estimates of the parameters a_i are necessary for obtaining a good fit. Check Maple’s fit with default parameter values! Use the linear fit from above for estimating a0 and a1; use your knowledge of trigonometry to estimate the other parameters.

a0 = 15, a1 = 0.8, a2 = 6, a3 = 1.6, a4 = 1.

Use NonlinearRegression from the PSMov2 package.

```
> sinemodel := a1 + a3 : x + a2 : sin(a3 : x + a4) :
> paramestimates := [a0 = 15, a1 = 0.8, a2 = 6, a3 = 1.6, a4 = 1.0] :
> NonlinearRegression(Month, Tons, sinemodel, paramestimates);
```

| Coefficient | Standard Error | T-Statistic | P-value |
|---|---|---|---|
| a0 | 14.187 | 0.56742 | 25.002 | 0. |
| a1 | 0.84795 | 0.047473 | 17.862 | 0. |
| a2 | 6.6892 | 0.38351 | 17.442 | 0. |
| a3 | 1.5735 | 0.010024 | 156.98 | 0. |
| a4 | 0.082625 | 0.12415 | 0.66555 | 0.51580 |

Model: m(x) = 14.187 + 0.84795 x + 6.6892 sin(1.5735 x + 0.082625)

The coefficient’s p-values look very good, save the phase shift a4. Plot the model with the data.

```
> m := rhs(%) :
> display(plot(m, x = 0..21, thickness = 2),
pointplot(Pts, symbol = solidcircle, symbolsize = 14),
labels = [month, 'Tons Shipped'],
labeldirections = [horizontal, vertical]) :
```

![](img/0f04050177d82aebd17d3383d7334896_266_0.png)

This model captures the oscillations and upward trend nicely. The sum of squared error is only SSE = 21.8. The new SSE is quite a bit smaller than that of the linear model. Clearly the model based on sine+linear regression does a much better job in predicting the trends than just using a simple linear regression.

## Example 6.5. Modeling Casualties in Afghanistan.

In a January 2010 news report, General Barry McCaffrey, USA, Retired, stated that the situation in Afghanistan would be getting much worse. General McCaffrey claimed casualties would double over the next year. The problem is to analyze the data to determine whether it supports his assertion.

The data that Gen. McCaffrey used for his analysis was the available 2001–2009 figures shown in Table 6.5. The table also shows casualties for 2010 and part of 2011 that were not available at the time.

### TABLE 6.5: Casualties in Afghanistan by Month

| Month | 2001 | 2002 | 2003 | 2004 | 2005 | 2006 | 2007 | 2008 | 2009 | 2010 | 2011 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 |  | 12 | 10 | 25 | 6 | 7 | 21 | 19 | 83 | 199 | 308 |
| 2 |  | 13 | 9 | 17 | 5 | 17 | 39 | 18 | 52 | 247 | 245 |
| 3 |  | 53 | 14 | 12 | 16 | 7 | 26 | 53 | 78 | 346 | 345 |
| 4 |  | 8 | 13 | 11 | 29 | 13 | 61 | 37 | 60 | 307 | 411 |
| 5 |  | 2 | 8 | 31 | 34 | 39 | 87 | 117 | 156 | 443 |  |
| 6 |  | 3 | 4 | 34 | 60 | 68 | 100 | 167 | 213 | 583 |  |
| 7 |  | 6 | 10 | 25 | 38 | 59 | 100 | 151 | 394 | 667 |  |
| 8 |  | 2 | 13 | 22 | 72 | 56 | 103 | 167 | 493 | 631 |  |
| 9 |  | 5 | 19 | 34 | 47 | 70 | 88 | 122 | 390 | 674 |  |
| 10 | 5 | 8 | 5 | 38 | 27 | 68 | 131 | 90 | 348 | 631 |  |
| 11 | 10 | 4 | 27 | 18 | 12 | 51 | 75 | 37 | 214 | 605 |  |
| 12 | 28 | 6 | 12 | 9 | 20 | 23 | 46 | 50 | 168 | 359 |  |

First, do a quick “reasonability model.” Sum the numbers across the years that Gen. McCaffrey had data for (Table 6.6) and graph a scatterplot.

### TABLE 6.6: Casualties in Afghanistan by Year

| 2002 | 2003 | 2004 | 2005 | 2006 | 2007 | 2008 | 2009 |
|---|---|---|---|---|---|---|---|
| 122 | 144 | 276 | 366 | 478 | 877 | 1028 | 2649 |

The scatterplot’s shape suggests that we use a parabola as our “reasonable ability model.”

```
with(plots):
  with(Statistics):
  CasYr := [122, 144, 276, 366, 478, 877, 1028, 2649]:
  Yr := {$1..8}:
  Pts := zip((x, y) → [x, y], Yr, CasYr):
  Fit(a + b · x + c · x², Yr, CasYr, x):
  RM := unapply(evalf(%, 5), x):
  RM(9);

              RM := x → 606.39 − 404.54x + 76.726x²
                         3180.336
```

The model’s prediction, while much smaller than the actual 2010 value, is not a doubling. However, the model does suggest further analysis is required.

We will focus on the four years before 2010, that is 2006 to 2009, and ask, do we expect the casualties in Afghanistan to double over the next year, 2010, based on those casualty figures?

```
Cas := [7, 17, 7, 13, 39, 68, 59, 56, 70, 68, 51, 23, 21, 39, 26, 61, 87, 100, 100,
        103, 88, 131, 75, 46, 19, 18, 53, 37, 117, 167, 151, 167, 122, 90, 37, 50, 83, 52,
        78, 60, 156, 213, 394, 493, 390, 348, 214, 168]:
Mon := [ $1..nops(Cas) ]:
Pts := zip((x, y) → [x, y], Mon, Cas):
```

In the same fashion as before, plot both a scatterplot and a line plot of the data available to Gen. McCaffrey over that period. See Figure 6.5. The line plot may better show trends in the data, such as an upward tendency or oscillations that are not apparent in the scatterplot. However, a line plot can be very difficult to read or interpret when there are a large number of data points connected. Good graphing is always a balancing act. After modeling the data from 2006 to 2009, we can use the 2010 values to test our model for goodness of prediction. There are two trends apparent from the graphs. First, the data oscillates seasonally. This time, however, the oscillations grow in magnitude. We will try to capture that with an x · sin(x) term. Second, the data appears to have an overall upward trend. We will attempt to capture that feature with a linear component. The nonlinear model we choose is

$$m(x) = a_0 + a_1 \cdot x + a_2 \cdot x \cdot \sin(a_3 \cdot x + a_4).$$

Using the techniques described in the previous example, we fit the nonlinear model: a growing-amplitude sine plus a linear trend. We estimate the parameters from the scatterplot:

$$[a_0 = 10, a_1 = 2, a_2 = 47, a_3 = 0.5, a_4 = 0.3].$$

## One-Predictor Logistic Regression

We begin with three one-predictor logistic regression model examples in which the dependent variable is binary, i.e., {0,1}. The logistic regression model form that we will use is

$$f(x)=\frac{e^{b_0+b_1x}}{1+e^{b_0+b_1x}}.$$

The logistic function, approximating a unit step function, gave the name logistic regression. The most general form handles dependent variables with a finite number of states.

### Example 6.6. Damages versus Flight Time.

After a number of hours of flight time, equipment is either damaged or not. Let the dependent variable $y$ be a binary variable with

$$y=\begin{cases}1 & \text{there is damage}\\0 & \text{there is no damage}\end{cases}$$

and let $t$ be the flight time in hours.

Over a reporting period, the data of Table 6.7 has been collected.

**TABLE 6.7: Damage vs. Flight Time**

| $t$ | 4 | 2 | 4 | 3 | 9 | 6 | 2 | 11 | 6 | 7 | 3 | 2 | 5 | 3 | 3 | 8 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| $y$ | 1 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 0 |

| $t$ | 10 | 5 | 13 | 7 | 3 | 4 | 2 | 3 | 2 | 5 | 6 | 6 | 3 | 4 | 10 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| $y$ | 0 | 1 | 0 | 0 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 1 | 0 | 1 | 0 |

Calculate a logistic regression for damage.

```
with(Statistics):

 t := [4, 2, 4, 3, 9, 6, 2, 11, 6, 7, 3, 2, 5, 3, 3, 8,
       10, 5, 13, 7, 3, 4, 2, 3, 2, 5, 6, 6, 3, 4, 10]:
 y := [1, 1, 0, 1, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 0,
       0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 0, 1, 0, 1, 0]:
 Pts := zip((u, v) -> [u, v], t, y):
 LM := exp(a + b*x)/(1 + exp(a + b*x))
```

Now, the fit.

```
NonlinearFit(LM, t, y, x, initialvalues = [a = 1.5, b = -0.5]):
Damage := unapply(evalf(%, 5), x);

Damage := x -> \frac{e^{-0.39190 x + 1.4432}}{1 + e^{-0.39190 x + 1.4432}}
```
