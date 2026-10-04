Assume a simple linear regression line has been fitted to $n$ observations such that $\hat{y}=eta_0+eta_1x$. A $100(1-\alpha)$ percent confidence interval for the mean response given a value of $x$ is calculated with

```
$$\hat{y} \pm t_{(1-\alpha/2,n)}s_e \sqrt{1 + \frac{(x-\hat{x})^2}{(n-1)s_x^2}} \quad (20.5)$
```

Here, $\hat{y}$ is the fitted value (from the regression line) at $x$; $t_{(1-\alpha/2,n)}$ is the appropriate critical value from a $t$-distribution with $n-2$ degrees of freedom (which others, resulting in an upper-tail area of exactly $\alpha/2$); $s_e$ and $s_x^2$ represent the sample mean estimated standard error; and the variance of the predictors, respectively.

A prediction interval (PI) for an observed response is different from the confidence interval in terms of context. CLs are used to describe the variability of the *mean* response, a PI is used to provide the possible range of values that an *individual realization* of the response variable might take, given $x$. This is subtle but important: the CI corresponds to a mean, and the PI corresponds to an individual observation.

Let's remain with the previous notation. It can be shown that $100(1-\alpha)$ percent interval for an individual response given a value of $x$ is calculated with the following:

```
$$\hat{y} \pm t_{(1-\alpha/2,n)}s_e \sqrt{1 + \frac{(x-\hat{x})^2}{(n-1)s_x^2}} \quad (20.6)$
```

It turns out that the only difference from (20.5) is the 1+ that appears in the square root. As such

# 20.4.2 Interpreting Intervals

R> as.numeric(beta0.hat+beta1.hat+14.5)
[1] 159.1446
R> as.numeric(beta0.hat+beta1.hat+24)
[1] 188.7524

According to the model, you can expect means to be around 159.14 and 188.75 cm, respectively. As.numeric* coercion function (first encountered in Section 6.2.4) is used simply to strip the result of the annot names that are otherwise present from the beta0.hat and beta1.hat objects.