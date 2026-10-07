
enough that these estimators are consistent so that

$$\frac{1}{l_j} = Var[\hat{\theta}(t_j)]$$

If these estimators are maximum likelihood estimators, they are also asymptotically normal and efficient. The estimates produced by most SAS procedures are maximum likelihood estimators and they are efficient. Schoen, Tsiatis, and Robins have shown that under the above conditions, if we are interested in testing the following general hypothesis $H_0: \theta = \theta_0$, the joint distribution of Wald statistics $Z(t_j) = \frac{\hat{\theta}(t_j)-\theta_0}{\sqrt{Var[\hat{\theta}(t_j)]}}, j=1, \dots$ computed at information fractions $t_1, \dots, t_j$, is asymptotically multivariate normal with $E[Z(t_j)] = \eta, Var[Z(t_j)] = 1$ and for $t_{j1} < t_{j2}, Cov[Z(t_{j1}), Z(t_{j2})] = \sqrt{\frac{t_{j1}}{t_{j2}}}$ where $\eta = (\theta-\theta_0)\sqrt{t_j}$ is known as the drift parameter. In this parameterization, the expectation of Wald statistic is simply proportional to the square root of information fraction.

An alternative parameterization is to express the same result in terms of stochastic process increments. We can define $S(t_j) = \sqrt{t_j}Z(t_j)$, then the joint distribution of $S(t_{j1}), S(t_{j2}), \dots, S(t_j)$ is asymptotically multivariate normal with $E[S(t_j)] = \eta, Var[S(t_j)] = t_j$ and for $t_{j1} < t_{j2}, Cov[S(t_{j1}), S(t_{j2})] = t_{j1}$. We can readily see that for $t_{j1} < t_{j2}$, the random variables $S(t_{j1})$ and the increment $S(t_{j2}) - S(t_{j1})$ are independent.

There are a few important implications following this result:

- First, in most clinical trials that use normal, binomial or survival endpoint, the test statistic $Z(t_j)$ is often utilized. Therefore, by above theorem, the distributional structure of these statistics is asymptotically the same as $S(t_j)$. Therefore, one can construct group sequential boundaries for the $S(t_j)$ stochastic process using the property that the overall probability of crossing a boundary is limited to the desired error rate, $\alpha$, under the null hypothesis $H_0: \theta = \theta_0$ or equivalently when $\eta = 0$, trials with normal, binomial or survival endpoint or even more general endpoints. Details on boundary construction will be given in 2.4 Types of Stopping Boundaries.

- Second, having generated the appropriate boundaries, one may compute efficacy probabilities for the stochastic process $S(t_j)$ under the alternative hypothesis $H_1: \theta = \theta_1$ or equivalently when $\eta = \eta_1$, where $\eta_1 = (\theta_1 - \theta_0)\sqrt{t_j}$. One can, therefore, search for the value of $\eta_1$ at which the overall boundary probability equals the desired power, $1 - \beta$. By substituting this value of $\eta_1$ into equation
$$l_j = \left[\frac{\eta_1}{\theta_1 - \theta_0}\right]^2$$
one can estimate $l_j$ and hence $n_j$, the sample size needed to attain the desired power, $1 - \beta$, at any pre-specified clinically meaningful treatment difference $\theta = \theta_1$.

- Third, due to the structure of independent increments for $S(t_j)$, it is possible to perform the actual computations that lead to these group sequential boundaries and their crossing probabilities by the technique of recursive integration.

We have just developed the general distribution theory which is applicable to any data generated from any arbitrary probability model in which a single parameter $\theta$ characterizes the relationship under investigation. In the following sections, we will consider two-arm randomized clinical trials with normal, binomial or time-to-event endpoints as examples to illustrate that different models provide us with a test statistic whose distribution is same as that of the stochastic process $S(t_j)$. In addition, when testing for superiority of one treatment over the other, it is customary to assume that $\theta_0 = 0$, but when testing for non-inferiority of one treatment to other, $\theta_0$ is often referred to as the non-inferiority margin, usually taking on a negative value.

## 2.3.2 Normal Endpoint

We can consider a randomized clinical trial designed to compare a test treatment, T, to a standard control treatment, C. The efficacy endpoint of interest is assumed to be a normally distributed random variable, X. For the test treatment, we assume the model for test treatment, $X_T \sim N(\mu_T, \sigma_T^2)$, and for control treatment, $X_C \sim N(\mu_C, \sigma^2)$, so that they have a common variance. If the investigators are interested in designing this trial as a group sequential trial with $J$ monitoring stages with cumulative samples of $n_1, n_2, \dots, n_J$ patients, then the information fraction at the end of the $j$-th stage is given by $t_j = n_j / n_J$. If the treatment effect is denoted as
$$\theta = \mu_T - \mu_C$$
the null hypothesis can be constructed as $H_0: \theta = 0$. We want to construct a $j$-stage group sequential level-$\alpha$ test of $H_0$ having $1 - \beta$ power at the alternative hypothesis $H_1: \theta = \theta_1$. We can let $\bar{X}_T(t_j)$ and $\bar{X}_C(t_j)$ be the sample means of the treatment and control groups, respectively, at time $t_j$. If we further assume that $r$ is the proportion of sample allocated to treatment
$$\hat{\theta}(t_j) = \bar{X}_T(t_j) - \bar{X}_C(t_j)$$
$$Var[\hat{\theta}(t_j)] = \frac{\sigma^2}{r(1-r)n_j}$$
Therefore, using parameterization of stochastic process,
$$S(t_j) = \sqrt{t_j}\frac{\hat{\theta}(t_j)-\theta_0}{\sigma/\sqrt{r(1-r)}}$$
$j=1, \dots, J$, and $S(t_j)$ is distributed as $N(\eta t_j, t_j)$. $\eta$ is the drift parameter such that $\eta = 0$ under null hypothesis but $\eta = \eta_1$, where $\eta_1 = (\theta_1 - \theta_0)\sqrt{t_j}$ under the alternative hypothesis. If this trial is a non-inferiority trial, then the null hypothesis is constructed as $H_0: \theta \le \theta_0$ where $\theta_0$ is the non-inferiority margin. Then using the same notation, the stochastic process
$$S(t_j) = \frac{X_T(t_j) - X_C(t_j)}{\sigma/\sqrt{r(1-r)}}$$
follows $N(\eta t_j, t_j)$ with $\eta = 0$ under null hypothesis but $\eta_1$. In both superiority and non-inferiority testing cases, we can search for the value of $\eta_1$ and $l_j$ such that the power is $1-\beta$. From the previous section, we know that
$$n_j = \frac{\sigma^2 l_j}{r(1-r)}$$
We can use this formula to convert the maximum information $l_j$ needed to achieve target power into the sample size $n_j$. However, we note that in order to make translation, we need to know the value of $\sigma^2$ which is the nuisance parameter. The value of this nuisance parameter is typically unknown. In practice, we usually replace $\sigma^2$ with its sample variance $s^2(t_j)$ at each interim monitoring point $t_j$ when the endpoint is assumed to be normally distributed. Therefore, we cannot track the path of these statistics in the course of a clinical trial and cannot know for sure if these statistics have crossed the stopping boundaries. However, under large sample condition, the operating characteristics of this sequential testing by tracking modified test statistics will be the same as those that would have been obtained by tracking original statistics.

## 2.3.3 Binomial Endpoint

In this section, we consider a randomized clinical trial comparing a test treatment, T, to a standard control treatment, C. We assume that the efficacy endpoint is now a binary response variable, $X$, which takes on the value of 1 if the response occurs or 0 otherwise, such that $P(X_T=1) = \pi_T$ and $P(X_C=1) = \pi_C$ where $X_T$ and $X_C$ are the response variables for the experimental and control treatments, respectively. We want to monitor the trial up to $J$ times after accruing $n_1, n_2, \dots, n_J$ patients. The information fraction at the $j$th stage is given by $t_j = n_j / n_J$. We let $r$ be the fraction of subjects allocated to the experimental treatment. Similarly, we define the treatment effect to be the difference in probabilities
$$\theta = \pi_T - \pi_C$$
Other parameters such as odds ratio can also be used and its logarithm (i.e., logit) is usually assumed to be normally distributed when the sample size is sufficiently large. The null hypothesis of interest is $H_0: \theta = 0$. We want to construct a $j$-stage group sequential level-$\alpha$ test having desired power of $1-\beta$ at the alternative hypothesis $H_1: \theta = \theta_1$.

We can further let $\hat{\pi}_T(t_j)$ and $\hat{\pi}_C(t_j)$ be the sample means, which are also the maximum likelihood estimators of $\pi_T$ and $\pi_C$ respectively, at time $t_j$ such that
$$\hat{\theta}(t_j) = \hat{\pi}_T(t_j) - \hat{\pi}_C(t_j)$$
$$Var[\hat{\theta}(t_j)] = \frac{\pi_T(1-\pi_T)}{n_J r} + \frac{\pi_C(1-\pi_C)}{n_J(1-r)}$$
