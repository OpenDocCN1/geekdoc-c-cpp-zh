# Display 8.19 Output from polynomial regression model

![](bbox=[0.12, 0.18, 0.78, 0.71])

The fit of the model yields the following prediction equation:

```
predicted sqrt(Total)=5.25-0.01×(conc-157)-0.00056×(conc-157)²
```

In this model, the count response is square-root transformed. (It is square-root transformed because we assumed Total was a Poisson variate, and, as a result, a variance-stabilizing transformation should be applied.) The concentration variable is centered. A variable CCONC2 is constructed that contains the square of the centered variable. Try this at home: Do the collinearity diagnostics change if you don’t center the CONC predictor and you square it? How would you interpret the parameters of this model?