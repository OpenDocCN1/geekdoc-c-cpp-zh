
# 18.2.1 Single Mean

As you've already met the standard error formula, $s/\sqrt{n}$, and the R function needed to obtain quantiles and probabilities from the t-distribution (qt and pt), the only new concepts to introduce here are related to the definition of the hypotheses and the interpretation of the result.

## Calculation: One-Sample t-Test

Let's dive straight into an example—a one-sample t-test. Recall the problem in Section 16.2.2 where a manufacturer of snack was interested in the mean weight of contents in an advertised 80-gram pack. Say that a consumer calls with a complaint—over time they have bought and precisely weighed the contents of the 44 randomly selected 80-gram packs from stores recorded the weights as:

```
R snacks <- c(87.7,80.01,77.28,78.76,81.52,74.2,80.71,79.5,77.87,81.94,80.7,
82.32,75.78,80.19,79.4,77.47,77.52,81.4,74.89,82.95,
73.59,77.92,77.18,79.83,81.23,79.28,78.44,79.01,80.47,76.23,
78.89,77.14,69.94,78.54,79.7,82.45,79.25,75.52,71.21,75.99,
81.94,80.41,77)
```

The customer claims that they've been shorted because their data cannot arise from a distribution with mean $\mu = 80$, so the true mean weight must be less than 80. To investigate this case, the manufacturer conducts a hypothesis test using a significance level of $\alpha = 0.05$.

First, the hypotheses must be defined, with a null value of 80 grams. Remember, the alternative hypothesis is “what you're testing for”; in this case, $H_A$ is that $\mu$ is smaller than 80. The null hypothesis, interpreted as “no change,” will be defined as $\mu = 80$: that the true mean is in fact 80 grams. These are formalized as follows:

> $H_0 : \mu = 80$
> $$H_A : \mu < 80 \quad (18.1)$$

Second, the mean and standard deviation must be estimated from the sample.

```
R n <- length(snacks)
R snack.mean <- mean(snacks)
R snack.mean
[1] 78.91068
R snack.sd <- sd(snacks)
R snack.sd
[1] 3.056023
```

The question your hypotheses seek to answer is this: given the standard deviation, what's the probability of observing a sample mean (when $n = 44$) of 78.91 grams or less if the mean is 80 grams? To answer this, you need to calculate the relevant statistic.

Formally, the test statistic $T$ in a hypothesis test for a single mean with respect to a null value of $\mu_0$ is given as

```
$T = \frac{\bar{x}-\mu_0}{s/sqrt{n}} (18.2)$
```

based on a sample of size $n$, a sample mean of $\bar{x}$, and a standard deviation of $s$ (the denominator is the estimated standard error of the mean). Assuming the relevant conditions have been met, $T$ follows a $t$-distribution with $\nu = n - 1$ degrees of freedom.

In R, the following provides you with the standard error of the sample mean for the snacks:

```
R snack.se <- snack.sd/sqrt(n)
R snack.se
[1] 0.4607128
```

Then, $T$ can be calculated as follows:

```
R snack.T <- (snack.mean-80)/snack.se
R snack.T
[1] -2.364419
```

Finally, the test statistic is used to obtain the $p$-value. Recall that the $p$-value is the probability that you observe $T$ or something more extreme. The nature of "more extreme" is determined by the alternative hypothesis $H_A$, which, as a less-than statement, directs you to a left-hand, lower-tail probability as $p$. In other words, the $p$-value is provided as the area under the sampling distribution (a $t$-distribution with 43 df in the current example) to the left of a vertical line at $T$. From Section 16.2.3, this is easily shown, as here:

```
R pt(snack.T,df=n-1)
[1] 0.0132175
```

Your results state that if the $H_0$ were true, there would be only a little more than a 1 percent chance that you'd observe the customer's sample mean of $\bar{x}=78.91$, or less, as a random phenomenon. Since this $p$-value is smaller than the predefined significance level of $\alpha=0.05$, the manufacturer concludes that there is sufficient evidence to reject the null hypothesis in favor of the alternative, suggesting the true value of $\mu$ is in fact less than 80 grams.

Note that if you find the 95 percent CI for the single sample mean, as described in Section 17.2.1 and given by

```
R snack.mean+c(-1,1)*qt(0.975,n-1)*snack.se
[1] 77.98157 79.83980
```

it does not include the null value of 80, mirroring the result of the hypothesis test at the 0.05 level.

## R Function: t.test

The result of the one-sample t-test can also be found with the built-in t.test function.

```
R> t.test(x=snacks,mu=80,alternative="less")
```

# One Sample t-test

```
data: snacks
t = -2.3644, df = 43, p-value = 0.01132
alternative hypothesis: mean is less than 80
95 percent confidence interval:
-Inf 79.68517
```

sample estimates:
mean of x
78.91068

The function takes the raw data vector as x, the null value for the mean mu, and the direction of the test (in other words, how to find the p-value under the appropriate t-curve) as alternative. The alternative argument has three available options: "less" for $H_A$; "greater" for $H_A$; and "two-sided" for $H_A$. The default value of alpha is 0.05. If you want a different significance level than 0.05, this must be provided to t.test as 1-α, passed to the argument conf.level.

Note that the value of T is reported in the output of t.test as are the degrees of freedom and the p-value. You also get a 95 percent "interval," but its values of -Inf and 79.68517 do not match the interval calculated just a moment ago. The manually calculated interval is in fact a two-sided—a bounded interval formed by using an error component that's equal on both sides.

The CI in t.test output, on the other hand, takes instruction from the alternative argument. It provides a one-sided confidence bound. For a lower-tailed test, it provides an upper bound on the statistic that the entire lower-tail of the sampling distribution is 0.95, as opposed to a central area as the traditional two-sided interval does. One-sided bounds are less frequently used than the fully bounded two-sided interval, which can be obtained (the component conf.int) from a relevant call to t.test by setting alternative="two.sided".

```
R> t.test(x=snacks,mu=80,alternative="two.sided")$conf.int
[1] 77.98157 79.83980
attr(,"conf.level")
[1] 0.95
```

This result matches your manually computed version from earlier. Note also that the corresponding confidence level, $1 - \alpha$, is stored alongside this component (refer to Section 6.2.1).

In examining the result for the snack example, be careful when interpreting hypothesis tests. With $\alpha$ at 0.05 for this particular test, $H_0$ is rejected. But what if the test were carried out with $\alpha=0.01$? The p-value is greater than 0.01, so in that case, $H_0$ would be retained, for no reason other than the arbitrary movement of the $\alpha$. In these situations, it's helpful to comment on the perceived strength of the evidence against the null hypothesis. Reasonably state that there exists some evidence to support $H_A$ but that this evidence is not especially strong.

# Exercise 18.1

- a. Adult domestic cats of a certain breed are said to have an average weight of 3.5 kilograms. A feline enthusiast disagrees and collects a sample of 73 weights of cats of this breed. From her sample, she calculates a mean of 3.97 kilograms and a standard deviation of 2.21 kilograms. Perform a hypothesis test to test her claim that the true mean $\mu$ is not 3.5 kilograms by setting up the appropriate hypothesis, carrying out the analysis, and interpreting the p-value (assume the significance level is $\alpha = 0.05$).
- b. Suppose it was previously believed that the mean magnitude of seismic events off the coast of Fiji is 4.3 on the Richter scale. Use the data in the mag variable of the ready-to-use quake set, providing 1,000 sampled seismic events in that area, to test the claim that the true mean magnitude is in fact greater than 4.3. Set up appropriate hypotheses, use t.test (conduct the test at a significance level of $\alpha = 0.01$), and draw a conclusion.
- c. Manually compute a two-sided confidence interval for the true mean of (b).

# 18.2.2 Two Means

Often, testing a single sample mean is not enough to answer the question you're interested in. In many settings, a researcher wants to directly compare the means of two distinct groups of measurements, which boils down to a hypothesis test for the true difference between two means; call them $\mu_1$ and $\mu_2$.

The way in which two groups of data relate to each other affects the specific form of standard error for the difference between two sample means and therefore the test statistic itself. The actual comparison of the two
