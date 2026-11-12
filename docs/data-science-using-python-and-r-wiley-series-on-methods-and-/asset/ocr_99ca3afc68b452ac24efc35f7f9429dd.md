| | Estimate | Std. Error | z value | Pr(>|z|) |
|---|---|---|---|---|
| (Intercept) | 0.4634478 | 0.0872706 | 5.310 | 1.09e-07 *** |
| Days | -0.0034721 | 0.0004221 | -8.226 | < 2e-16 *** |
| Web | 1.0972994 | 0.2829570 | 3.878 | 0.000105 *** |
Signif. codes: 0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Figure 13.4 Logistic regression results from R for the test data set.

To validate the model, run the model on the test data and obtain the summary of the model (Figure 13.4). The code is given below.

```
logreg01_test <- glm(formula = CC ~ Days + Web, data =
sales_test, family = binomial)
summary(logreg01_test)
```

# 13.5 POISSON REGRESSION

There are many other kinds of regression models that fall under the umbrella of GLM. We will examine one other: Poisson regression. Poisson regression is used when you want to predict a count of events, such as how many times a customer will contact customer service. The distribution of the response variable will be a count of occurrences, with a minimum value of zero.

The link function for a count response variable is \(g(\mu) = \text{ln}(\mu)\). We set the link function equal to our linear predictor to obtain

\(X\beta = \text{ln}(\mu)\)

After isolating \(\mu\), we have

\(\mu = e^{X\beta}\)

Working backwards from our abbreviated notation, we find the parametric version of the Poisson regression equation

\(y = e^{\beta_0 + \beta_1 x_1 + \beta_2 x_2 + \cdots + \beta_p x_p} + \varepsilon\)

from which we can write the descriptive form

\(\hat{y} = e^{\hat{\beta}_0 + \hat{\beta}_1 x_1 + \hat{\beta}_2 x_2 + \cdots + \hat{\beta}_p x_p}\)

# 13.6 AN APPLICATION OF POISSON REGRESSION MODELING

We will use the churn data set to build a model that estimates the number of customer service calls based on whether a customer churned. Our response variable is an integer-valued variable, which is why we use Poisson regression instead of linear regression for this estimation.