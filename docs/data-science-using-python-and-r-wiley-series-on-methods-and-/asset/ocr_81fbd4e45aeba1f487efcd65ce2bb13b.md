![](bbox=[0.12, 0.08, 0.88, 0.34])

Figure 12.2 Multicollinearity: when the predictors are correlated, the response surface is unstable, resulting in dubious and highly variable coefficient estimates.

other, so that as one of them increases, so does the other. In this case, the predictors no longer form a solid basis upon which the response surface may firmly rest. Instead, when the predictors are correlated, the response surface is unstable, providing highly variable coefficient estimates $b_1$ and $b_2$.

The high variability associated with the estimates means that different samples may produce coefficient estimates with widely different values. For example, one sample may produce a positive coefficient estimate for $x_1$, while a second sample may produce a negative coefficient estimate. This situation is unacceptable when the analytic task calls for an explanation of the relationship between the response and the predictors, individually.

Let us look at a toy example to help us understand the problem. Consider the tiny population in Table 12.1.

Clearly, $x_1$ and $x_2$ are correlated, with $r = 0.938$, $p$-value about 0. Now, split into two samples, as shown in Tables 12.2 and 12.3. The regression equation for sample 1 is:

```
$$ \hat{y} = -0.542 + 2.552 x_1 - 0.206 x_2 $$
```

The regression equation for sample 2 is:

```
$$ \hat{y} = -1.08 + 0.547 x_1 + 1.759 x_2 $$
```

Note that the coefficient for $x_1$ is negative in sample 1 and positive in sample 2. This represents unstable behavior in the regression coefficients, caused by the correlation between the predictors. Essentially, we cannot trust the values, or even the signs, of the regression coefficients. So, interpreting the regression coefficients for our clients