The se is used for calculating the t-statistic used in statistical tests of significance. The t-statistic is compared with the value from the Student's t distribution so as to determine a p-value. The se for the intercept (a) is given by:

```
$se_a = se = \sqrt{\frac{\sum_{i=1}^n X_i^2}{n \sum_{i=1}^n (X_i - \bar{x})^2}}$
```

And for the slope (b) by:

```
$se_b = \sqrt{\frac{se^2}{\sum_{i=1}^n (X_i - \bar{x})^2}}$
```

The subsequent t-statistic for the intercept (a) is given by:

```
$t_a = \frac{a}{se_a}$
```

And for the slope (b) by:

```
$t_b = \frac{b}{se_b}$
```

The Student's t-distribution is generally defined as the probability distribution of a set of random variables that best fit the data without knowing the population deviation. The particular form of the t-distribution depends on the number of degrees of freedom i.e. the number of independent observations in a set of data. The higher the degrees of freedom, the closer the t-distribution to the standard normal distribution. The t-distribution is very similar in shape to the normal distribution but has fatter tails resulting in more values further away from the mean value as shown in Figure 4.18.
t-distribution plays a central role in the associated t-test for assessing the statistical significance of the difference between two sample means, the development of confidence intervals to determine the difference between two population means, and in linear regression analysis.