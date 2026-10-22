In general, for any dummy variable, its expected value is just the probability that it is equal to 1. But assumptions 1 and 2 also imply another expression for this expectation. Taking the expected values of both sides of the equation in assumption 1, we get

```
E(y_i) = E(α + βx_i + ε_i)
      = E(α) + E(βx_i) + E(ε_i)
      = α + βx_i.
```

Putting these two results together, we get

```
p_i = α + βx_i,  (2.1)
```

which is sometimes called the *linear probability model*. As the name suggests, this model says that the probability that y=1 is a linear function of x. Regression coefficients have a straightforward interpretation under this model. A 1-unit change in x produces a change of β in the probability that y=1. In Output 2.1, the coefficient for SERIOUS was .038. So we can say that each 1-point increase in the SERIOUS scale (which ranges from 1 to 15) is associated with an increase of .038 in the probability of a death sentence, controlling for the other variables in the model. The BLACKD coefficient of .12 tells us that the estimated probability of a death sentence for black defendants is .12 higher than for nonblack defendants, controlling for other variables.

Now let’s consider the variance of ε_i. Because x is treated as fixed, the variance of ε_i is the same as the variance of y_i. In general, the variance of a dummy variable is p_i(1−p_i). Therefore, we have

```
var(ε_i) = p_i(1 − p_i) = (α + βx_i)(1 − α − βx_i).
```

We see, then, that the variance of ε_i must be different for different observations and, in particular, it varies as a function of x. The disturbance variance is at a maximum when p_i=.5 and gets small when p_i is near 1 or 0.

We’ve just shown that a dichotomous dependent variable in a linear regression model necessarily violates assumptions of homoscedasticity (assumption 3) and normality (assumption 5) of the error term. What are the consequences? Not as serious as you might think. First of all, we don’t need these assumptions to get *unbiased* estimates. If just assumptions 1 and 2 hold, ordinary least squares will produce unbiased estimates of α and β. Second, the normality assumption is not needed if the sample is reasonably large. The central limit theorem assures us that coefficient estimates will have a distribution that is