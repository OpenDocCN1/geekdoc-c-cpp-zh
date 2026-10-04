the fitted value of that line. The simple linear regression line estimated as per (20.3) is the line that lies "closest to all observations." By this, it is meant that the fitted regression model is represented by the estimated line that passes through the coordinate provided by the variable means(\bar{x},\bar{y}), it's the line that yields the smallest overall measure of the squared residual distances. For this reason, another name for a least-squares-estimated regression equation line like this is the line of best fit.

# 20.3 Statistical Inference

The estimation of a regression equation is relatively straightforward, but this is merely the beginning. You should now think about what can be inferred from your result. In simple linear regression, there's a natural question that should be asked: Is there statistical evidence to support the presence of a relationship between the predictor and the response? To put it another way, is there evidence of change in the explanatory variable affects the mean outcome? You investigate this following the same ideas that were introduced in Chapter 17 when you began thinking about the variability in estimated statistics and then continued to infer from your results using confidence intervals and, in Chapter 18, hypothesis testing.

# 20.3.1 Summarizing the Fitted Model

This kind of model-based inference is automatically carried out by R when lm objects are produced. Using the summary function on an object created by lm provides you with output more detailed than simply printing the object to the console. For the moment, you will focus on two aspects of the information presented in summary: the significance tests associated with the regression coefficients and the interpretation of the so-called coefficient of determination (labeled R-squared in the output), which I'll explain shortly.

Use summary on the current model object survfit, and you'll see the

```
R> summary(survfit)
```

```
Call:
lm(formula = ~ Wr.Hnd, data = survey)
```

Residuals:
Min 1Q Median 3Q Max
-19.7276 -5.0706 -0.8269 4.9473 25.8704

Coefficients:
Estimate Std. Error t value Pr(|t|)
(Intercept) 113.9536 5.4416 20.94 <2e-16 ***
Wr.Hnd 3.1166 0.2888 10.79 <2e-16 ***

Signif. codes: 0 *** 0.001 ** 0.01 '*' .05 ' . ' ' 1