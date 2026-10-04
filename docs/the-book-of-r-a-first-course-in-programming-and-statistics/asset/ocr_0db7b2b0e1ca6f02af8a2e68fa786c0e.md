the handspan of the writing hand (Wr.Hnd). The help page ?survey shows that data have also been collected on the nonwriting handspan (Nw.Hnd). It's reasonable to expect that these two variables will be highly correlated, which is precisely why I have avoided any use of Nw.Hnd previously. Indeed, executing

```
R cor(survey$Wr.Hnd,survey$Nw.Hnd,use="complete.obs")
[1] 0.948310
```

reveals a high correlation coefficient, suggesting a strong linear association between the writing and nonwriting handpans of the students. In other words, these two variables should represent much the same information in any given model.

Now, you know from previously fitted models that writing handspan has a significant and positive impact on predicting mean student height. The following code quickly confirms this via a simple linear regression.

```
R> summary(lm(Height ~Wr.Hnd,data=survey))
```

```
Call:
lm(formula = Height ~ Wr.Hnd, data = survey)
```

```
Residuals:
Min 1Q Median 3Q Max
-19.7276 -5.0706 -0.8269 4.9473 25.8704
```

```
Coefficients:
Estimate Std. Error t value Pr(|>t|)
(Intercept) 113.9536 5.4416 20.94 <2e-16 ***
Wr.Hnd 3.1166 0.2888 10.79 <2e-16 ***
```

```
Sig. codes: 0 *** 0.001 '** 0.01 '* 0.05 '* '.' ' 1
```

Residual standard error: 7.909 on 206 degrees of freedom
(29 observations deleted due to missing)
Multiple R-squared: 0.3612, Adjusted R-squared: 0.3581
F-statistic: 116.5 on 1 and 206, p-value: < 2.2e-16

The high positive correlation between Wr.Hnd and Nw.Hnd suggests that using Nw.Hnd instead should have a similar effect.

```
R> summary(lm(Height~Nw.Hnd,data=survey))
```

```
Call:
lm(formula = Height ~ Nw.Hnd, data = survey)
```

```
Residuals:
Min 1Q Median 3Q Max
-21.8285 -5.1397 -0.2867 4.5611 25.5750
```