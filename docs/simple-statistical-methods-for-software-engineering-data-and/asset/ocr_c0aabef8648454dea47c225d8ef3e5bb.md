P(X = k) = C_{k}^{r+k-1} p^{k} (1 - p)^{r}

![](bbox=[0.15, 0.16, 0.82, 0.44])

# Figure 11.2 Negative binomial for right first time delivery (r = 10, success probability p = 0.6).

The Excel function appears as follows, with four arguments:

```
NEGBINOM.DIST(number_f, number_s, probability_s, cumulative)
```

where number_f is the number of failures (k in NBD Equation 11.4), number_s is the threshold number of successes (r in NBD Equation 11.4), probability_s is the probability of success (p in NBD Equation 11.4), and cumulative is a logical value that determines the form of the function. If cumulative is true, NEGBINOM.DIST returns the cumulative distribution function; if false, it returns the probability density function.

Finding the probability of delivering 10 right sensors produced for the first time from a batch of size 12 can be directly solved as follows:

+   Batch size n = 12
+   Number of success s = 10
+   Number of failure k = 2
+   Probability of success p = 0.6

The Excel function returns the answer 0.0532. Thus, there is only a small chance of finding 10 right sensors produced for the first time.

The mean and variance of the NBD can be directly computed by entering data in Equations 11.5 and 11.6. The answers are as follows:

+   Mean = 15
+   Variance = 37.5

Figure 11.2 shows that the sensor problem peaks at the mean.