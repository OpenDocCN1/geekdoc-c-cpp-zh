estimate σ_X (as is more common in practice). You've seen that the standard error is defined as the standard deviation divided by the square root of n. For a small n, you must also assume that the raw observations are normally distributed, since the CLT will not apply.

To construct an appropriate interval, you must first find the critical value corresponding to α. By definition the CI is symmetric, so this translates to a central probability of (1 − α) around the mean, which is exactly α/2 in the lower tail and the same in the upper tail.

Return to the example from Section 17.1.1, dealing with the mean daily maximum temperatures (degrees Celsius) in January for Dunedin, New Zealand. Suppose you know the observations are normally distributed but you don't know the true mean μ_X (which is set at 22) or the true standard deviation σ_X (which is set at 1.5). Setting it up in the same way as earlier, assume you've made the following five independent observations:

```
R> temp.sample <- rnorm(n=5,mean=22,sd=1.5)
R> temp.sample
[1] 20.46097 21.45658 21.06410 20.49367 24.92843
```

As you're interested in the sample mean and its sampling distribution, you must calculate the sample mean x̄, the sample standard deviation s, and the appropriate standard error of the sample mean, s/√n.

```
R> temp.mean <- mean(temp.sample)
R> temp.mean
[1] 21.68075
R> temp.sd <- sd(temp.sample)
R> temp.sd
[1] 1.862456
R> temp.se <- temp.sd/sqrt(5)
R> temp.se
[1] 0.8329155
```

Now, let's say the aim is to construct a 95 percent confidence interval for the true, unknown mean μ_X. This implies α = 0.05 (the total amount of tail probability) for the relevant sampling distribution. Given the fact that you know the raw observations are normal and that you're using s (not σ_X), the appropriate distribution is the t-distribution with n − 1 = 4 degrees of freedom. For a central area of 0.95 under this curve, α/2 = 0.025 must be in either tail. Knowing that R's q functions operate based on a total lower tail area, the (positive) critical value is therefore found by supplying a probability of 1 − α/2 = 0.975 to the appropriate function.

```
R> 1-0.05/2
[1] 0.975
R> critval <- qt(0.975,df=4)
R> critval
[1] 2.776445
```