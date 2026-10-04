
+   g. The friend inspects a histogram of her raw measurements and notices that her raw data are heavily right-skewed. Briefly identify and describe the nature of the sampling distribution with respect to the sample mean and calculate the appropriate standard error.

+   h. Using the standard error from (g) and the appropriate probability distribution, calculate the probability that in another sample of the same size, the sample mean time between cars passing is as:
ni. More than 40 seconds
ii. Less than half a minute
iii. Between the given sample mean and 40 seconds

## 17.1.3 Sampling Distributions for Other Statistics

So far you've looked at sampling distributions in cases dealing with a single sample mean or sample proportion, though it's important to note that many problems require more complicated measures. Nevertheless, you can apply the ideas explored in this section to any statistic estimated from a finite-sized sample. The key, always, is to understand the variability associated with your point estimates.

In some cases, such as those covered so far, the sampling distribution is parametric, meaning the functional (mathematical) form of the probability distribution itself is known and depends only on the proportion of specific parameter values. This is contingent upon the satisfaction of certain conditions, as you've seen with the application of the normal distribution covered in this chapter. For other statistics, it may be the case that you do not know the form of the appropriate sampling distribution—in these cases, you could use computer simulation to obtain the required probabilities.

In the remainder of this chapter and over the next few, you will continue to explore statistics that are tied to sampling distributions for tests and models.

The variability of an estimated quantity is actually only one side of the coin. Just as important is the issue of bias. Where "natural variability" should be associated with random error, bias is associated with systematic error, in the sense that a biased statistic does not settle on the corresponding true value as the sample size increases. Bias can be caused by flaws in a study design or collection of data or can be the result of a poor estimator of statistical interest. Bias is an undesirable trait of any given estimator and statistical analysis unless it can be quantified and removed, which is often difficult if not impossible in practice. I've therefore dealt so far only with unbiased statistical estimators, many of which you may already be familiar with (for example, the arithmetic mean), and I'll continue to assume unbiasedness moving forward.

## 17.2 Confidence Intervals

A confidence interval (CI) is an interval defined by a lower limit $l$ and an upper limit $u$, to describe possible values of a corresponding true population parameter in light of observed sample data. Interpretation of a confidence interval therefore allows you to state a "level of confidence" that a true parameter of interest falls between this and lower limit, often expressed as a percentage. As such, it is a common and useful tool built directly from the sampling distribution of the statistic of interest.

The following are the important points to note:

Confidence intervals may be constructed in different ways, depending on the type of statistic and the shape of the corresponding sampling distribution. For symmetrically distributed sample statistics, like those involving means and proportions that will be used in this chapter, a general formula is

```
statistic \pm critical value \times standard error, \eqno (17.2)
```

where statistic is the sample statistic under scrutiny, critical value is a value from the standardized version of the sampling distribution that corresponds to $\alpha$, and standard error is the standard deviation of the sampling distribution. The product of the critical value and standard error is referred to as the error component of the interval; subtraction of the error component from the value of the statistic provides $l$, and addition provides $u$.

With reference to the appropriate sampling distribution, all that a CI yields are the two values of the distribution that mark off the central $100 \times (1 - \alpha)$ percent of the area under the density. This is the process that was briefly mentioned in Exercise 17.1 (f.) You use the CI to make further interpretations concerning the true (typically unknown) parameter value that's being estimated by the statistic of interest.

### 17.2.1 An Interval for a Mean

You know from Section 17.1.1 that the sampling distribution of a single sample mean depends heavily on whether you know the true standard deviation of the raw measurements, $\sigma_X$. Then, provided the sample size for this mean is roughly $n \geq 30$, the CLT ensures a symmetric distribution—which will be normal if you know the true value of $\sigma_X$, or $t$ based with $\nu = n-1$ df if you must use the sample standard deviation, $s$, to

estimate $\sigma_X$ (as is more common in practice). You've seen that the standard error is defined as the standard deviation divided by the square root of $n$. For a small $n$, you must also assume that the raw observations are normally distributed, so that the CLT will not apply.

To construct an appropriate interval, you must first find the critical value corresponding to $\alpha$. By definition the CL is symmetric, which translates to a central probability of $(1-\alpha)$ around the mean, which is exactly $\alpha/2$ in the lower tail and the same in the upper tail.

Return to the example from Section 17.1.1, dealing with the mean daily maximum temperatures (degrees Celsius) in January of Dunedin, New Zealand. Suppose you know the observations are normally distributed but you don't know the true mean $\mu_X$ (which is set at 22) or the true deviation $\sigma_X$ (which is at 1.5). Setting it up the following independent observations:

```
R> temp.sample <- rnorm(n=5,mean=22,sd=1.5)
R> temp.sample
[1] 20.46097 21.45568 21.06410 20.49367 24.92843
```

As you're interested in the sample mean and its sampling distribution, you must calculate the sample mean $\bar{X}$, the sample standard deviation $s$, and the appropriate standard error of the sample mean, $s/\sqrt{n}$.

```
R> temp.mean <- mean(temp.sample)
R> temp.mean
[1] 21.68075
R> temp.sd <- sd(temp.sample)
R> temp.sd
[1] 1.862456
R> temp.se <- temp.sd/sqrt(5)
R> temp.se
[1] 0.832955
```

Now, let's say the aim is to get a 95 percent confidence interval for the true, unknown mean $\mu_X$. This implies $\alpha=0.05$ (the total amount of tail probability) for the relevant sampling distribution. Given that you know the raw observations are normal and that you are using $s$ (not $\sigma_X$), the appropriate distribution is the $t$-distribution with $n-1=4$ degrees of freedom. For a central area of $0.95$ over this curve, $\alpha/2=0.025$ is met in either tail. Noting that R's $q$ functions operate based on a lower tail area, area of $1-\alpha/2=0.975$ is therefore found by supplying a probability

```
R> 1-0.05/2
[1] 0.975
R> critval <- qt(0.975,df=4)
R> critval
[1] 2.776445
```

Sampling Distributions and Confidence 379

Figure 17-3 shows why the qt function is used in this way (since I used similar code throughout Chapter 16, I haven't reproduced the code for Figure 17-3 here).

area under curve (p)
0.975 ←
0.025 ←

![](img/b2cfc85cbb129f60fe595a2bae074fe4_413_0.png)

Figure 17-3: Illustrating the role of the critical value in a confidence interval for a sample mean, using the Dunedin temperature example. The sampling distribution is t with 4 df, and the use of qt with respect to symmetric tail probabilities related to $\alpha/2 = 0.025$ yields a central area of 0.95.

Note that when viewed with respect to the negative version of the same critical value (“reflected”) around the mean and obtained by using qt(0.025,4), the central, symmetric area under the curve must be 0.95. You can confirm this using pt.

```
R> pt(critval,4)-pt(-critval,4)
[1] 0.95
```

So, all the ingredients are present. You find the 95 percent confidence interval for the true mean $\mu_X$ via Equation (17.2) with the following lines, which give $l$ and $u$, respectively:

```
R> temp.mean-critval*temp.se
[1] 19.36821
R> temp.mean+critval*temp.se
[1] 23.99329
```
