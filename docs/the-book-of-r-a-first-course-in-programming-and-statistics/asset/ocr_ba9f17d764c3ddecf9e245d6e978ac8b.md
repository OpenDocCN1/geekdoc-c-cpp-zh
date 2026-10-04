```
(Intercept) 49.80842  3.60516 13.816 5.01e-14 ***
hp          -0.12010  0.02470 -4.863 4.04e-05 ***
wt          -8.21662  1.26971 -6.471 5.20e-07 ***
hp:wt        0.02785  0.00742  3.753 0.000811 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 2.153 on 28 degrees of freedom
Multiple R-squared:  0.8848,    Adjusted R-squared:  0.8724
F-statistic: 71.66 on 3 and 28 DF,  p-value: 2.981e-13
```

The model is written as

```
“Mean MPG” = 49.80842 − 0.12010 × “horsepower”
               − 8.21662 × “weight”
               + 0.02785 × “horsepower : weight”
             = 49.80842 − 0.12010 × “horsepower”
               − 8.21662 × “weight”
               + 0.02785 × “horsepower” × “weight”
```

The second version of the model equation provided here reveals for the first time an interaction expressed as the product of the values of the two predictors, which is exactly how the fitted model is used to predict the response. (Technically, this is the same as when at least one of the predictors is categorical—but the dummy coding simply results in zeros and ones for the respective terms, so multiplication just amounts to the presence or absence of a given term, as you’ve seen.)

You can interpret an interaction between two continuous predictors by considering the sign (+ or −) of the coefficient. Negativity suggests that as the values of the predictors increase, the response is reduced after computing the result of the main effects. Positivity, as is the case here, suggests that as the values of the predictors increase, the effect is an additional increase, an amplification, on the mean response.

Contextually, the negative main effects of hp and wt indicate that mileage is naturally reduced for heavier, more powerful cars. However, positivity of the interactive effect suggests that this impact on the response is “softened” as horsepower or weight is increased. To put it another way, the negative relationship imparted by the main effects is rendered “less extreme” as the values of the predictors get bigger and bigger.

Figure 21-9 contrasts the main-effects-only version of the model (obtained using lm with the formula mpg~hp+wt; not explicitly fitted in this section) with the interaction version of the model fitted just above as the object car.fit.