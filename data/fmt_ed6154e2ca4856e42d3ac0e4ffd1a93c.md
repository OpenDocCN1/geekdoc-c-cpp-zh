
That is, the difference between the mean of the rival company packs and the original manufacturer's packs, when the original is subtracted from the rival, bigger than zero. The “no-change” scenario, the null hypothesis, is that the two means are the same, so their difference is truly zero.

Now that you've constructed the hypotheses, let's look at how to test them. The difference between two means is the quantity of interest. For two independent samples arising from populations with means $\mu_1$ and $\mu_2$, sample means $\bar{x}_1$ and $\bar{x}_2$, and standard deviations $s_1$ and $s_2$, respectively (and that meet the relevant conditions for the validity of the $t$-distribution), the standardized test statistic $T$ for testing the difference between $\mu_2$ and $\mu_1$, in that order, is as

```
$T = \frac{\bar{x}_2 - \bar{x}_1}{\sqrt{s_1^2/n_1 + s_2^2/n_2}}, \quad (18.3)$
```

whose distribution is approximated by a $t$-distribution with $\nu$ degrees of freedom,

```
$$\nu = \frac{(s_1^2/n_1 + s_2^2/n_2)^2}{(s_1^2/n_1)^2/(n_1-1) + (s_2^2/n_2)^2/(n_2-1)} \quad (18.4)$$
```

In (18.3), $\mu_0$ is the value of interest—typically zero in tests concerned with “difference” statistics. This term would therefore disappear from the numerator of the test statistic. The denominator of $T$ is the standard error of the difference between two means in this setting.

[$\cdot]$ denotes a floor operation rounding strictly to the nearest integer.

The two-sample $t$-test, conducted using Equation (18.3), is also called Welch’s $t$-test. This refers to use of Equation (18.4), called the Welch-Satterthwaite equation. Crucially, it assumes that the two samples have different variances, which is why we use the unpooled version of the test.

It's important to be consistent when defining your two sets of parameters when constructing the hypotheses. In this example, since the test aims to find evidence for $\mu_2$ being greater than $\mu_1$, a difference of $\mu_2–\mu_1 > 0$ forms $H_A$ (a greater-than, upper-tailed test), and this order of subtraction is mirrored when calculating $T$. The same test could be carried out if you defined the difference the other way. In your case, alternative hypothesis would suggest a lower-tailed test if you are testing for $\mu_2$ being bigger than $\mu_1$, $H_A$ would correctly be written as $\mu_1–\mu_2 < 0$. Again, this would modify the order of subtraction in the numerator of Equation (18.3).

The same care must apply to the use of `t.test`, two-sample comparisons. The two samples must be supplied as the arguments `x` and `y`, by the function interprets `x` as greater than `y` when doing an upper-tailed test and interprets `x` as less than `y` when doing a lower-tailed test. Therefore,

performing the test with `alternative="greater"` for the snack pack example, it's `snacks2` that must be supplied to `x`:

```
R> test(x=snacks2,y=snacks,alternative="greater",conf.level=0.9)
```

### Welch Two Sample t-test

data: snacks2 and

t = 2.4455, df = 60.091, p-value = 0.008706

alternative hypothesis: true difference in means is greater than 0

90 percent confidence interval:

Inf

sample estimates:

mean of x mean of y

0.859714 78.91068

With a small p-value of 0.008706, you'd conclude that there is sufficient evidence to reject H0 in favor of H1 (indeed, the p-value is critically smaller than the stipulated alpha = 0.1 significance level as implied by `conf.level=0.9`). The evidence suggests that the mean weight of snacks from the rival manufacturer's 80-gram packs is greater than the mean weight for the original manufacturer.

Note that output from `t.test` has a df value of 60.091, which is the unfloored result of (18.4). You also receive a one-sided confidence bound (based on the aforementioned confidence level), triggered by the one-sided nature of this test. Again, the more common two-sided 90 percent interval is also useful; knowing that $\nu = [60.091] = 60$ and using the statistic and the standard error of interest (numerator and denominator of Equation (18.3), respectively), you can calculate it.

```
R> (snack2.mean-snack.mean) +
c(-1,1)*qt(0.95,df=60)*sqrt(snack.sd^2/44+snack2.sd^2/31)
[1] 0.394917 0.097120
```

Here, you used the previously used sample statistics `snack.mean`, `snack.sd` (the mean and standard deviation of 44 raw measurements from the original manufacturer's), `snack2.mean`, and `snack2.sd` (the same quantities for the 31 observations corresponding to the rival manufacturer). Note that the CI takes the same form as detailed by Equation (17.2) on page 378 and to provide the 1-alpha area, the q-function of the t-distribution requires 1-alpha/2 as its probability value. You can interpret this as being "90 percent confident that the true difference in mean weight between the rival and the original manufacturer (in order) is somewhere between 0.395 and 2.098 grams." The fact that zero is not included in the interval, and the interval is wholly positive, supports the conclusion from the hypothesis test.

## Unpaired/Independent Samples: Pooled Variance

In the unpooled variance example just passed, there was no assumption that the variances of the two populations whose members were being compared were equal. This is an important note to make because it leads to the use of (18.3) for the test statistic calculation and (18.4) for the associated degrees of freedom in the corresponding t-distribution. However, if you can assume equivalence of variances, the precision of the test—use a different formula for the standard error of the difference and for calculating the associated df.

Again, the quantity of interest is the difference between two means, written as $\mu_1 - \mu_2$. Assume you have two independent samples of sizes $n_1$ and $n_2$ arising from populations with true means $\mu_1$ and $\mu_2$, sample means $\bar{x}_1$ and $\bar{x}_2$, and standard deviations $s_1$ and $s_2$, respectively, and assume that the relevant conditions for the validity of the t-distribution have been met. Additionally, assume that the true variances of the samples, $\sigma_1^2$ and $\sigma_2^2$, are equal such that $\sigma_1^2 = \sigma_2^2$.

> There is a simple rule of thumb to check the validity of the "equal variance" assumption. If the ratio of the larger sample standard deviation to the smaller sample standard deviation is less than 2, you can assume equal variances. For example, if $s_1 > s_2$, if $\frac{s_1}{s_2} < 2$, you can use the pooled variance test statistic that follows.

The standardized test statistic $T$ for this scenario is given as

```
T=\frac{\bar{x}_2 - \bar{x}_1}{\sqrt{s_p^2(1/n_1 + 1/n_2)}} \quad (18.5)
```

whose distribution is a t-distribution with $\nu = n_1 + n_2 - 2$ degrees of freedom, where

```
s_p^2=\frac{(n_1-1)s_1^2 + (n_2-1)s_2^2}{n_1+n_2-2} \quad (18.6)
```

is the pooled estimate of the variance of all the raw measurements. This is substituted in place of $s_1$ and $s_2$ in the denominator of Equation (18.3), resulting in Equation (18.5).

All other aspects of the two-sample test remain as earlier: the construction of appropriate hypotheses, the typical null value of $\mu_0$, and the calculation and interpretation of the p-value.

For the comparison of the two means in the snack example, you'd find it difficult to justify the pooled version of the t-test. The rule of thumb, the two estimated standard deviations ($s_1 \simeq 3.06$ and $s_2 \simeq 1.21$ for the original and rival manufacturer's samples, respectively) have a large-to-small ratio that is greater than 2.

- > `snack.sd/snack2.sd`

[1] 2.51795

尽管这比较非正式，如果该假设不能合理地做出，最好坚持使用未合并版本的检验。

为了说明这一点，让我们考虑一个新的例子。智商（IQ）是一个通常被假定为衡量一个人聪明的数量。IQ 分数被合理地假定为正态分布，且人口的平均 IQ 被认为是 100。假设你有兴趣评估男性和女性之间的平均分数是否存在差异，提出以下假设，你有 $n_{men} = 12$ 和 $n_{women} = 20$：

```
$H_{0} : \mu_{men} - \mu_{women} = 0$
$H_{A} : \mu_{men} - \mu_{women} \neq 0$
```

你随机抽样了以下数据：
