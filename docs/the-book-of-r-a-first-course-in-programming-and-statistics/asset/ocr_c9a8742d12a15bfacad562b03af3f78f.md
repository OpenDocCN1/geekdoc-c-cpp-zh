# 18.5.3 Type II Errors

The issues with Type I errors might suggest that it's desirable to perform a hypothesis test with a smaller $\alpha$ value. Unfortunately, it's not quite simple; reducing the significance level for any given test leads directly to an increase in the chance of committing a Type II error.

A Type II error refers to incorrect retention of the null hypothesis—in other words, obtaining a p-value greater than the significance level when it's the alternative hypothesis that's actually true. For the same scenario you've been looking so far (an upper-tailed test for a single sample mean), Figure 18-3 illustrates the probability of a Type II error, shaded and denoted $eta$.

![](bbox=[0.238, 0.273, 0.615, 0.517])

Figure 18-3: A conceptual diagram of the Type II error probability $eta$

It's not easy to find $eta$ as it is to find the probability of making a Type I error because $eta$ depends, on other things, on what the true value of $\mu_A$ (which is in general you won't know). If $\mu_A$ is closer to the hypothesized null value of $\mu_0$, you can imagine the alternative distribution in Figure 18-3 (translating to the left), resulting in an increase in $eta$. Similarly, with Figure 18-3, imagine decreasing the significance level $\alpha$. Doing so means the vertical dashed line (denoting the critical value) moves to the right, also increasing the shaded area of $eta$. Intuitively, this makes sense—the closer the true value is to the null and/or smaller the significance level, the harder $H_A$ is to detect by rejection of $H_0$.

As noted, $eta$ usually can't be calculated in practice because of the need to know what the true distribution actually is. This quantity is useful in giving you an idea of how prone a test is to the incorrect retention of a null hypothesis under particular conditions. Suppose, for example, you're performing a one-sample t-test for $H_0: \mu = \mu_0$ and $H_A: \mu > \mu_0$ with $\mu = 0$ but that the (true) alternative distribution of the raw measurements has $\mu_A = 0.5$ and standard deviation $\sigma = 1$. Given a random sample of size $n=30$ and using $\alpha = 0.05$, the probability of committing a Type II error in any given hypothesis test (using the same standard deviation