
the sample size to 20 (from 30) results in an increased simulated Type II error rate compared with the most recent result of 0.5501, increasing the sample size to 40 improves the rate.

```
R typeII.tester(mu0=0,muA=0.5,sigma=1.2,n=20,alpha=0.01)
[1] 0.7319
R typeII.tester(mu0=0,muA=0.5,sigma=1.2,n=40,alpha=0.01)
[1] 0.4219
```

Finally, as noted at the beginning of the discussion, the specific value of $\mu$A itself is easy to adjust as you expect. Again, keeping the latest values for all other components, which resulted in my case in $\beta$=0.4219, shifting the "true" mean closer to $\mu$A by changing from $\mu$A=0.5 to $\mu$A=0.4 means the probability of committing a Type II error is increased; the opposite side is true if the difference is increased to $\mu$A=0.6.

```
R typeII.tester(mu0=0,muA=0.4,sigma=1.2,n=40,alpha=0.01)
[1] 0.6147
R typeII.tester(mu0=0,muA=0.6,sigma=1.2,n=40,alpha=0.01)
[1] 0.2287
```

To summarize, although these simulated rates have been applied to the specific situation in which the hypothesis test is an upper-tailed test for a single mean, the general concepts and ideas discussed here for any hypothesis test. It is easy to establish that the Type I error matches the predefined significance level and can be decreased by reducing $\alpha$. In contrast, controlling the Type II error rate is a complex balancing act that can involve sample size, significance level, observation variability, and magnitude of the difference between the true value and the null. This problem is largely academic as the "truth" is typically unknown in practice. However, the Type II error rate's direct relationship to statistical power often plays a critical role in preparing for data collection, especially when using the next sample size requirements, as you will see in the next.

## Exercise 18.5

+   a. Write a new version of typeI.tester function should be able to simulate the Type I error rate for tests of a single mean in any direction (one or two-sided). The new function should also add an additional argument, test, which takes a character string "less", "greater", or "two.sided" depending on the type of desired test. You can achieve this by modifying typeI.tester as:
    Instead of calculating and storing the p-values directly in the loop, simply store the test statistic.

-   When the loop is complete, set up stacked if-else statements that cater to each of the three types of test, calculating the p-value as appropriate.
-   For the two-sided test, remember that the p-value is defined as twice the area "more extreme" than the null. Computationally, this means you must use the upper-tail area if the test statistic is positive and the lower-tail area otherwise. If this area is less than half of $\alpha$ (since it is subsequently multiplied by 2 in a "real" hypothesis test), then a rejection of the null should be flagged.
-   If the value of test is not one of the three possibilities, the function should show an appropriate error using stop.

+   i. Experiment with using the first example testing in the text with $\mu_0 = 0, \sigma = 1, n = 40$, and $\alpha = 0.05$. Call typeI.mean three times, using each of the possible options for test. You should find that all simulated results close to 0.05.
ii. Repeat (using) the second example in the text with $\mu_0 = -4, \sigma = 0.3, n = 60$, and $\alpha = 0.01$. Again, you should find that all simulated results close to the value of $\alpha$.

+   b. Modify typeII.test in the same way you did typeI.test; call the new function typeII.mean. Simulate the Type II errors for the following hypothesis tests. As per the text, assume $\mu_A$, $\sigma$, and $n$ denote the true mean, standard deviation of variation, significance level, and sample size, respectively.

+   i. $H_0 : \mu = -3.2, H_A : \mu \neq -3.2$
with $\mu = -3.3, \sigma = 0.1, \alpha = 0.05$, and $n = 25$.
ii. $H_0 : \mu = 8994, H_A : \mu > 8994$
with $\mu = 5600, \sigma = 3888, \alpha = 0.01$, and $n = 9$.
iii. $H_0 : \mu = 0.44, H_A : \mu > 0.44$
with $\mu = 0.4, \sigma = 2.4, \alpha = 0.05$, and $n = 68$.

## 18.5.4 Statistical Power

For any hypothesis test, it is useful to consider its potential statistical power. Power is the probability of correctly rejecting a null hypothesis that is untrue. For a test that is a Type II error rate of $\beta$, the statistical power is found simply with $1 - \beta$. It's desirable for a test to have a power as high as possible. The simple relationship with the Type II error probability means that all factors affecting the value of $\beta$ directly affect power.

For the same one-sided $H_0 : \mu = \mu_0$ and $H_A : \mu > \mu_0$ example discussed in the previous section, Figure 18-4 shows the power of the test—complement to the Type II error rate. By convention, a hypothesis test that has a power greater than 0.8 is considered *statistically powerful*.

# Distribution under $H_0: \mu = \mu_0$ Distribution under $H_A: \mu > \mu_0$

![](img/b2cfc85cbb129f60fe595a2bae074fe4_462_0.png)

You can numerically evaluate power under specific testing conditions using simulation. For the previous discussion on Type II errors, you're able to subtract all simulated results of $\beta$ from 1 to evaluate the power of that particular test. For example, the power of detection of $\mu_A = 0.6$ when $\mu_0 = 0$, taking samples of size $n = 40$ and with $\sigma = 1.2$ and $\alpha = 0.01$, is simulated as $1 - 0.2287$ (using my most recent result of $\beta$ from earlier). This means there's a 77 percent chance of correctly detecting the true mean of 0.6 in a hypothesis test based on a sample of measurements generated under those conditions.

Researchers are often interested in the relationship between power and sample size (though it is important to bear in mind that this is only one of the influential ingredients in the determination of power). Before you collect data to examine a particular hypothesis, you might have an idea of the true value of the parameter of interest from past research or pilot studies. This is useful in determining your sample size, such as in helping to answer questions like "How big does my sample size need to be in order to conduct a statistically powerful test to reject $H_0$, if the true mean is actually $\mu_A$"

## Simulating Power

For the most recent testing conditions, with a sample size of $n = 40$, you've seen that there's a power of around 0.77 of detecting $\mu_A = 0.6$. For the purposes of this example, let's say you want to find how much you should increase $n$ by order to conduct a statistically powerful test. To answer this, define the following function `power` in the editor:

```
power.test <- function(nvec,...{
  nlen <- length(nvec)
  result <- rep(NA,nlen)
  pbar <- txtProgressBar(min=0,max=nlen,style=3)
  for(i in 1:nlen){
```

```
result[i] <- 1-typeII.tester(n=nvec[i],...)

setTxtProgressBar(pbar,i)

close(pbar)
return(result)
```

power.tester function uses the typeII.tester function defined in Section 18.5 to evaluate the power of a given upper-tailed hypothesis test of a single sample mean. It takes a vector of sample sizes using the nvec argument (pass all other arguments to typeII.tester using an ellipsis—refer to Section for loop defined in power.tester cycles through the entries of nvec one at a time, simulates the power for each sample size, and stores them in a corresponding vector that's returned to the user. Remember, typeII.tester, this function is using random generation of hypothetical data, so there may be some fluctuation in the results you observe every time you run power.tester.

There can be a slight delay when evaluating the power for many individual sizes, so this function also provides a good opportunity to show a progress bar in a practical implementation (refer to Section 12.2.1 for details).

Set up the following vector, which uses colon operator (see Section 2.3.2) to construct a sequence of integers between 5 and 100 inclusive for the sample sizes to be examined:

```
R> sample.sizes <- 5:100
```

Importing the power function, you can then simulate the power for each of these integers for this particular test (ITERATIONS is halved to 5000 to reduce the overall completion time).

```
R> power.tester(nvec=sample.sizes, mu=0,muA=0.6,sigma=1.2,alpha=0.01,ITERATIONS=5000)
```

| [1] | 0.0630 | 0.0752 | 0.1018 | 0.1226 | 0.1588 | 0.1834 | 0.2162 | 0.2440 | 0.2638 | 0.2863 |
| [2] | 0.2904 | 0.3122 | 0.3278 | 0.3504 | 0.3664 | 0.3974 | 0.4232 | 0.4478 | 0.4680 | 0.4920 |
| [3] | 0.5258 | 0.5452 | 0.5615 | 0.5916 | 0.6124 | 0.6328 | 0.6626 | 0.6638 | 0.6838 | 0.6844 |
| [4] | 0.6910 | 0.7288 | 0.7412 | 0.7552 | 0.7778 | 0.7972 | 0.8050 | 0.8078 |
| [5] | 0.8418 | 0.8316 | 0.8524 | 0.8600 | 0.8700 | 0.8722 | 0.8820 | 0.8968 | 0 [89]  |
| [6] | 0.8976 | 0.9116 | 0.9218 | 0.9218 | 0.9328 | 0.9320 | 0.9370 | 0.9338 |
| [7] | 0.9430 | 0.9434 | 0.9580 | 0.9582 | 0.9568 | 0.9648 | 0.9658 | 0.9784 | 0.9750 |
| [8] | 0.9742 | 0.9770 | 0.9770 | 0.9804 | 0.9804 | 0.9806 | 0.9854 | 0.9848 | 0.9844 |
| [9] | 0.9864 | 0.9866 | 0.9890 | 0.9888 | 0.9910 | 0.9984 | 0.9906 | 0.9930 | 0.9926 | 0.9938 |
| [10]| 0.9930 | 0.9936 | 0.9948 | 0.9942 | 0.9942 | 0.9952

As expected, the power of detection rises steadily as n increases; the results as you are seeing
