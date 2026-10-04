
Though this is rather informal, if the assumption cannot reasonably be made, it's best to stick with the unpooled version of the test.
To illustrate this, let's consider a new example. The intelligence quotient (IQ) is a quantity commonly assumed to measure how clever a person is. IQ scores are reasonably assumed to be normally distributed, and the average IQ of the population is said to be 100. Say you're interested in assessing whether there is a difference in mean scores between men and women, suggesting the following hypotheses that you have $n_{men} = 12$ and $n_{women} = 20$:

```
$H_{0} : \mu_{men} - \mu_{women} = 0$
$H_{A} : \mu_{men} - \mu_{women} \neq 0$
```

You randomly sample the following data:

```
$R$
men <- c(102,87,101,96,107,91,85,108,67,85,82)
$R$
women <- c(73,81,111,109,143,95,92,120,93,119,79,90,126,62,92,77,106,105,111)$
```

As usual, let's calculate the basic statistics:

- mean(men)
- [1] 92.66667
- sd(men)
- [1] 12.0705
- mean(women)
- [1] 98.65
- sd(women)
- [1] 19.94802

These give the sample averages $\bar{x}_{men}$ and $\bar{x}_{women}$, as well as their respective sample standard deviations $s_{men}$ and $s_{women}$. Enter the following to quickly check the ratio of the standard deviations:

```
$sd(women)/sd(men)$
-[1] 1.652622
```

You can see that the ratio of the larger sample standard deviation to the smaller is less than 2

```
$R t.test(x=men,y=women,alternative="two.sided",conf.level=0.95,var.equal=TRUE)
```

## Two Sample t-test

data: men and women
t = -0.9376, df = 30, p-value = 0.3559

alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
-19.016393 7.049727

sample estimates:
mean of x mean y
92.66667 98.65000

Note also for this example implies a two-tailed test, hence the provision of alternative="two-sided".

The resulting p-value of this test, 0.3559, is certainly larger than the conventional cutoff level of 0.05. Thus, your conclusion is that there is no evidence to reject H0—there is insufficient evidence to support a true difference in the mean IQ scores of men compared to women.

## Paired/Dependent Samples

Finally, we'll look at comparing two means in paired data. This setting is distinct from that of unpaired t-tests because it concerns the way the data have been collected. The issue concerns dependence pairs of observations across the two groups of interest—previously, the measurements in each group have been defined as independent. This notion is important consequences for how the test can be carried out.

Paired data occurs if the measurements forming the two sets of observations are recorded on the same individual or if they are related in other important or obvious way. A classic example of this is "before" and "after" observations, such as two measurements made on each person before and after some kind of intervention treatment. These situations still focus for the difference between the mean outcomes in each group, but rather than working with the two data sets separately, a paired t-test with a single mean—the true mean of the individual paired differences $\mu_d$.

As an example, consider a company interested in the efficacy of a drug designed to reduce resting heart rates in beats per minute (bpm). The resting rates of 16 individuals are measured. The individuals are then administered a course of the treatment, and their resting heart rates are again measured. The data are provided in the two vectors before and rate.after as follows:

```
R rate.before <- c(52,66,89,87,72,66,65,69,72,50,72,57,63,65,61)
R rate.after <- c(51,66,71,73,70,68,50,51,40,57,65,63,56,60,59)
```

It becomes clear why any test comparing these two groups must take dependence into account. Heart rate is affected by an individual's age, build, and level of physical fitness. An unfit individual older than 60 is likely to have a baseline resting heart rate higher than a 20-year-old, and if both are given the same drug to lower their heart rate, their final heart rates are still likely to reflect the baselines. Any true effect of the drug therefore has the potential to be hidden if you approached the analysis using either of the unpaired t-tests.

To overcome this problem, the paired two-sample considers the difference between each pair of values. Labeling one set of n measurements as $x_1, \dots, x_n$ and the other set of n observations as $y_1, \dots, y_n$, the difference, is defined as $d_i = y_i - x_i; i=1, \dots, n$. In R, you can easily compute the pairwise differences:

```
R rate.d <- rate.after-rate.before
R rate.d
[1] -1 0 -18 -14 -19 -4 -14 -9 -5 1 -11 -7 -5 -2
```

The following code calculates the mean $\bar{d}$ and standard deviation $s_d$ of these differences:

```
R rate.dbar <- mean(rate.d)
R rate.dbar
[1] -7.4375
R rate.sd <- sd(rate.d)
R rate.sd
[1] 6.19637
```

You want to see how much the heart rate is reduced by, so the test at hand will be concerned with the following hypotheses:

> $H_0 : \mu_d = 0$
> $H_A : \mu_d < 0$

Give the order or subtraction to obtain the differences, detection of a successful reduction in heart rate will be represented by an "after" mean that is smaller than the "before" mean.
Expressing this mathematically, the value of interest is the true mean difference, $\mu_d$, between two means of dependent pairs of measurements. There are two sets of $n$ measurements, $x_1, \dots, x_n$ and $y_1, \dots, y_n$, with pairwise differences $d_1, \dots, d_n$. The relevant conditions for the validity of the $t$-distribution must be met; in this case, if the number of $n$ is less than 30, then you must be able to assume the raw data are normally distributed. The test statistic $T$ is given as

> $T = \frac{\bar{d}-\mu_0}{s_d/\sqrt{n}}$

where $\bar{d}$ is the mean of the pairwise differences, $s_d$ is the standard deviation of the pairwise differences, and $\mu_0$ is the null value (usually zero). The statistic $T$ follows a $t$-distribution with $n-1$ df.
The form of Equation (18.7) is actually the same as the form of the test statistic in (18.2), once the sample statistics for the individual paired differences have been calculated. Furthermore, it's important to note that n represents the total number of pairs, not the total number of individual observations.

For the current example hypotheses, you can find the test statistic and p-value with rate.bar and rate.sd.

```
R> rate.T <- rate.bar/(rate.sd/sqrt(16))
R> rate.T
[1] -4.801146
R> pt(rate.T,df=15)
[1] 0.00016681
```

These results suggest evidence to reject H0. In t.test, the optional logical argument paired set to TRUE.

```
R> t.test(x=rate.after,y=rate.before,alternative="less",conf.level=0.95,paired=TRUE)
```

Paired t-test

```
data: rate.after and rate.before
t = -4.8011, df = 15, p-value = 0.0001167
alternative hypothesis: true difference in means is less than 0
95 percent confidence interval:
-Inf -4.721833
sample estimates:
mean of the differences
-7.4375
```

Note that the order you supply your data vectors to the x and y arguments follows the same rules as for the unpaired tests, given the desired value of alternative. The same pvalue as calculated manually through the use of t.test, and since this is an assumed conventional significance level of α = 0.05, a valid conclusion would be to state that there is statistical evidence that the medication reduces the mean resting heart rate. You could go on to say you're 95 percent confident that the true mean difference in heart rate after taking the course of medication lies somewhere between

```
R> rate.bar-qt(0.975,df=15)*(rate.sd/sqrt(16))
[1] -10.73935
```

and

```
R> rate.bar-qt(0.975,df=15)*(rate.sd/sqrt(16))
[1] -4.135652
```

On some occasions, such as when your data strongly indicate non-normality, you may not be comfortable assuming the validity of the CLT (refer back to Section 17.1.1). An alternative approach to the tests discussed here is to employ a nonparametric technique that relaxes these requirements. In the two-sample case, you could employ the Mann-Whitney U test (also known as the Wilcoxon rank-sum test). This is a hypothesis test that compares two medians, as opposed to two means. You can use the R function wilcox.test to access this methodology; its help page provides useful comments and references on the particulars of the technique.

## Exercise 18.2

In the package MASS you'll find the data set anorexia, which contains data on pre- and post-treatment weights (pounds) of 72 young women suffering from the disease, obtained from Hand et al. (1994). One group of women is the control group (in other words, no intervention), and the other groups are the cognitive behavioral program and support intervention program groups. Load the library and ensure you can access the data frame and its contents. $\mu_d$ denote the mean difference in weight, computed as (post-weight – pre-weight).

- Regardless of which treatment group the participants fall into, conduct and conclude an appropriate hypothesis test with $\alpha = 0.05$ for the entire set of weights for the following hypotheses:

```
$H_0 : \mu_d = 0$
$H_A : \mu_d > 0$
```

- Next, conduct three separate hypothesis tests using the defined hypotheses, based on which treatment group the participants fall into. What do you notice?

Another ready-to-use data set in R is Plantgrowth (Dobson, 1983), which records a continuous measure of the yields of a certain plant, looking at the potential effect of two supplements administered during growth to increase the yield when compared to a control group with no supplement.

- Set up hypotheses to test whether the mean yield for the control group is less than the mean yield from a plant given either of the treatments. Determine whether this test should proceed using a pooled estimate of the variance or whether Welch's t-test would be more appropriate.

- Conduct the test and make a conclusion (assuming normality of the raw observations).
