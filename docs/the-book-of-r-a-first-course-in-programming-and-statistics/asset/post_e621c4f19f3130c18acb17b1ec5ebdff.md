
![](img/b2cfc85cbb129f60fe595a2bae074fe4_310_0.png)

**Figure 13-3:** Comparing two hypothetical data vectors that share an identical arithmetic mean (marked by the vertical dotted line) but have different magnitudes of spread. Identical observations are jittered slightly.

The sample variance measures the degree of the spread of numeric observations around their arithmetic mean. The variance is a particular representation of the average squared distance of each observation compared to the mean. For a set of $n$ numeric measurements labeled $x = \{x_1, x_2, \dots, x_n\}$, the sample variance $s_x^2$ is given by the following, where $\hat{x}$ is the sample mean described in Equation (13.1):

```
$$s_x^2 = \frac{(x_1 - \hat{x})^2 + (x_2 - \hat{x})^2 + \dots + (x_n - \hat{x})^2}{n-1} = \frac{1}{n-1} \sum_{i=1}^n (x_i - \hat{x})^2 \quad (13.3)$$
```

For example, if you take the eight illustrative observations 2, 4, 4, 3, 2, 2, 2, 4, their sample variance is as follows when rounded to three decimal places (some terms are hidden with ... for readability):

```
$$\frac{(2 - 2.825)^2 + (4.4 - 2.825)^2 + \dots + (7 - 2.825)^2}{7} = \frac{(-0.825)^2 + (1.575)^2 + \dots + (1.175)^2}{7} = \frac{6.355}{7} = 0.908$$
```

The standard deviation is the square root of the variance. Since the variance is a representation of the average squared distance, the standard deviation provides a valuable interpretable with respect to the scale of the original observations. With the same notation for a sample of $n$ observations, the sample standard deviation $s$ is found by taking the square root of Equation (13.3).

```
$$s_x = \sqrt{s^2} = \sqrt{\frac{1}{n-1}\sum_{i=1}^n (x_i - \hat{x})^2} \quad (13.4)$$
```

For example, based on the sample variance calculated earlier, the standard deviation of the eight hypothetical observations is as follows (to three decimal places):

$\sqrt{0.9088} = 0.953$

Thus, a rough way to interpret this is 0.953 represents the average distance of each observation from the mean.
Unlike the variance and standard deviation, the interquartile range (IQR) is not computed with respect to the sample mean. The IQR measures the width of the "middle 50 percent" of the data, that is, the range of values that lie within 25th percentile on either side of the median. As such, the IQR is computed as the difference between the upper and lower quartiles of your data. Formally, where $Q_x(\cdot)$ denotes the quantile function (as defined in Section 13.2.3), the IQR is given as

$IQR_x = Q_x(0.75) - Q_x(0.25) \quad (13.5)$

The direct R commands for computing these measures of spread are var (variance), sd (standard deviation), and IQR (interquartile range).

```
R var(xdata)
[1] 0.9078571
R sd(xdata)
[1] 0.9528154
R IQR(xdata)
[1] 1.25
```

You can confirm the relationship between the sample variance and standard deviation using the square root function sqrt from var, and you can reproduce the IQR by calculating the difference between the third and first quartiles.

```
R sqrt(var(xdata))
[1] 0.9528154
R as.numeric(quantile(xdata,0.75)-quantile(xdata,0.25))
[1] 1.25
```

Note that as.numeric (see Section 6.2.4) strips away the percentile annotations (that label the results by default) from the returned object of quantile.
Now, do the same with the ydata observations that have the same arithmetic mean as xdata. The calculations give you the following:

```
R sd(ydata)
[1] 2.0126393
R IQR(ydata)
[1] 1.6
```

ydata is on the same scale as xdata, so the results confirm what you can see in Figure 13-3—that the observations in the former are more spread out than the latter.

For two final examples, let's return again to the chicks and quakes data sets. In Section 13.2.1, you saw that the mean weight of all the chicks is 261.3099 grams. You can now find that the standard deviation of the weights is as follows:

```
R sd(chickwts$weight)
[1] 78.0737
```

Informally, this implies that the weight of each chick is, on average, around 78.1 grams away from the mean (technically, though it is merely the square root of a function of the squared distances—see the following). In Section 13.2.3, you used summary to obtain the five-number summary of magnitudes of some of the quakes. Looking at the first and third quartiles in these results (4.4 and 4.9, respectively), you can quickly determine that the IQR of this subset is 0.5. This can be confirmed using IQR.

```
R IQR(quakes$mag[quakesdepth>=400])
[1] 0.5
```

The definition of variance (and hence standard deviation) referred to the sample estimator, the default in R, which uses divisor of $n-1$ when the observations represent a sample. In these cases, the divisor of $n-1$ is more accurate, providing what is known as an unbiased estimate of the true population value.

## Exercise 13.3

- a. Using the chickwts data frame, compute the 10th, 30th, and 90th percentiles of all the weights and then use tapply to determine which type is associated with the highest sample variance.
- b. Turn to the seismic event data in quakes and complete the following tasks:
    - i. Find the IQR of the recorded depths.
    - ii. Find the five-number summary of all magnitudes that occur at a depth of 400 km or deeper. Compare this to the summary of those events occurring less than 400 km and briefly comment on what you notice.
    - iii. Use your knowledge of cut (Section 4.3) to create a new factor depthcat that identifies evenly spaced categories of quakes so that when you use levels(depthcat), it gives you the following:
> levels(depthcat)
[1] "0,200" "200,360" "360,520" "520,680"
    - iv. Find the mean and standard deviation of the magnitudes associated with each category of depth according to depthcat.
    - v. Use apply to compute the quantile of the magnitudes in quakes, split by depthcat.

## 1.2.5 Covariance and Correlation

When analyzing data, it's often useful to investigate the relationship between two numeric variables to assess trends. For example, you might expect height and weight observations to have a noticeable relationship—taller people tend to weigh more. Conversely, you might imagine that handspan and length would have less of an association. One of the simplest and most common ways such associations are quantified and compared is correlation, for which you need the covariance.

The covariance expresses how much two numeric variableschange together" and the nature of that relationship, whether it is positive or negative. Suppose for individuals you have a sample of observations for two variables, labeled $x=[x_1,x_2,...,,x_n]$ and $y=[y_1,y_2,...,,y_n]$, where $x_i$ corresponds to $y_i$ for $i=1,...,n$. The sample covariance $r_{xy}$ is computed with the following, where $\bar{x}$ and $\bar{y}$ represent the sample mean of sets of observations:

```
$$r_{xy} = \frac{1}{n-1}\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y}) \quad (13.6)$$
```

When you get a positive result for $r_{xy}$, it shows that there is a positive relationship—as $x$ increases, $y$ increases. When you get a negative result, a negative linear relationship—as $x$ increases, $y$ decreases, and vice versa. When $r_{xy}=0$, this indicates that there is no linear relationship between the values of x and y. It is useful to note that the variables in the formula itself doesn't matter; in other words, $r_{xy} \equiv r_{yx}$.

To demonstrate, let's use the original illustrative observations, which I'll denote with $x = (2,4,4,3,3,2,2,2,4)$, and the additional eight observations denoted with $y = (1,4,4,1,3,2,2,2,7)$. Remember that both x and y have mean of 2.825. The sample covariance of two sets of observations is as follows (rounded to three decimal places):

```
$(2 - 2.825) \times (1 - 2.825) + \dots + (4 - 2.825) \times (7 - 2.825) / \frac{7}$
(-0.825) \times (-1.825) + \dots + (1.175)(4.175) / \frac{7}$
$\frac{10.355}{7} = 1.479$
```

The figure is a positive number, so this suggests there is a positive relationship between the observations in x and y.

Correlation allows you to interpret the covariance further by identifying both the direction and the strength of any association. There are different types of correlation, but the most common of them are Pearson's product-moment correlation coefficient, the default implemented by R (which I will use in this chapter). Pearson's sample correlation coefficient $\rho_{xy}$ is computed by dividing the covariance by the product of the standard deviation of each data set. Formally, where $r_{xy}$ corresponds to Equation (13.6) and [Wait, text cut fragmented].

When $\rho_{xy} = -1$, a perfect negative relationship exists. Any result less than zero shows a negative relationship, and the relationship gets weaker the nearer to zero the coefficient gets, until $\rho_{xy} = 0$, showing no relationship at all. As the coefficient increases above zero, a positive relationship is shown, until $\rho_{xy} = 1$, which is a perfect linear relationship.

If you take the standard deviations already computed for x and y in Section 13.2.4 ($s_x = 0.953$ and $s_y = 2.013$ to find the following to three decimal places),

```
\frac{1.479}{0.953 \times 2.013} = 0.771
```

$\rho_{xy}$ is positive like $r_{xy}$; the value of 0.771 indicates a moderate-to-strong positive association between the observations in x and y. Again, $\rho_{xy} \equiv \rho_{yx}$.

The R commands cov and cor are used for the sample covariance and correlation; you need only to supply the two corresponding vectors of data.

```
R xdata <- c(2,4,4,3,3,2,2,2,4)
R ydata <- c(1,4,4,1,3,2,2,2,7)
```
