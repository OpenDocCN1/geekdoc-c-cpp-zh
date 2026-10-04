plants. For the sake of this example, assume you don’t have the data on these predictors. Can the cost of construction be adequately modeled using only the variables that describe characteristics of the plant itself?

Load the boot package and access the ?nuclear help page to find details on the variables: cap (continuous variable describing the capacity of the plant); cum.n (treated as continuous, describing the number of similar constructions the engineers had previously worked on); ne (binary, describing whether the plant was in the northeastern United States); and ct (binary, describing whether the plant had a cooling tower).

The following model is fitted with the final construction cost of the plant as the response; a main effect for capacity; and main effects of, and all two-way interactions and the three-way interaction among, cum.n, ne, and ct:

```
R> nuc.fit <- lm(cost~cap+cum.n*ne*ct,data=nuclear)
R> summary(nuc.fit)
```

Call:

lm(formula = cost ~ cap + cum.n * ne * ct, data = nuclear)

Residuals:
Min 1Q Median 3Q Max
-162.475 -50.368 -8.833 43.370 213.131

Coefficients:
Estimate Std. Error t value Pr(>|t|)
(Intercept) 138.0336 99.9599 1.381 0.180585
cap 0.5085 0.1127 4.513 0.000157 ***
cum.n -24.2433 6.7874 -3.572 0.001618 **
ne -260.1036 164.7650 -1.579 0.128076
ct -187.4904 76.6316 -2.447 0.022480 *
cum.n:ne 44.0196 12.2880 3.582 0.001577 **
cum.n:ct 35.1687 8.0660 4.360 0.000229 ***
ne:ct 524.1194 200.9567 2.608 0.015721 *
cum.n:ne:ct -64.4444 18.0213 -3.576 0.001601 **
---
Signif. codes: 0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 107.3 on 23 degrees of freedom
Multiple R-squared: 0.705, Adjusted R-squared: 0.6024
F-statistic: 6.872 on 8 and 23 DF, p-value: 0.0001264

In this code, you specify the higher-order interactions by extending the number of variables connected with a * (using * instead of : since you want to include all the lower-order effects of those three predictors as well).

In the estimated results, the main effect for cap is positive, showing that an increased power capacity is tied to an increased construction cost. All other main effects are negative, which at face value seems to imply that a