![](bbox=[0.23635, 0.06935, 0.68365, 0.33535000000000004])

Note from earlier R output that unless not explicitly defined at creation, the levels of a factor appearing in alphabetical order by default—is the case for Smoke—and R will automatically select the first one (as shown in the output of a call to calls) as the reference level when that factor is used as a predictor in subsequent model fitting. Fitting the linear model in using lm, you can see from a subsequent call to summary that indeed the first level of Smoke, for “heavy”, has been used as the reference:

```
R survfit3 <- lm(Height~Smoke,data=survey)
R> summary(survfit3)
```

Call:
lmm(formula = Height ~ Smoke, data = survey)

Residuals:
Min 1Q Median 3Q Max
-25.02 -6.82 -1.64 8.18 28.18

Coefficients:
Estimate Std. Error t value Pr(>|t|)
(Intercept) 173.7720 3.1028 56.005 <2e-16 ***
SmokeNever -1.9520 3.1933 -0.611 0.542
SmokeOccas -0.7433 3.9553 -0.188 0.851
SmokeRegul 3.6451 4.0625 0.897 0.371

Signif. codes: 0 *** 0.001 ** 0.01 * 0.05 ' ' 0.1 ' ' 1

Residual standard error: 9.812 on 205 degrees of freedom (28 observations deleted due to missingness)