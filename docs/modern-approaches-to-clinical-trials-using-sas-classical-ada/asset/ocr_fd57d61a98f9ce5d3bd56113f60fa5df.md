# 9.5.3 Optimal Adaptive Randomization

Adaptive randomization can be optimized by minimizing the variance or minimizing the number of nonresponders in a trial [13-15]. As an illustration, let us consider a two-arm trial with dichotomous responses. Let $p_1$ and $p_2$ be the response rates of treatments 1 and 2, respectively. We are interested in testing $H_0: p_1=p_2$ versus $H_1: p_1 
eq p_2$.

Neyman's allocation is obtained by minimizing the variance of the test statistic, which results in the allocation ratio between arm 1 and arm 2 as

```
$Neyman = \frac{\sqrt{p_1(1-p_1)}}{\sqrt{p_2(1-p_2)}}$
```

From an ethical perspective, Rosenberg et al. [12] proposed an optimal allocation scheme that minimizes the expected number of nonresponders while fixing the variance of the test statistic, which leads to an optimal allocation ratio of

```
$N_{opt} = \frac{\sqrt{p_1}}{\sqrt{p_2}}$
```

For continuous outcomes, we assume normality for patients' responses in arms 1 and 2, $Y_1 \sim N(\mu_1, \sigma_1^2)$ and $Y_2 \sim N(\mu_2, \sigma_2^2)$. We are interested in testing $H_0: \mu_1=\mu_2$ versus $H_1: \mu_1 
eq \mu_2$.

By minimizing the variance of the estimated treatment difference, Neyman's allocation ratio is given by

```
$Neyman = \frac{\sigma_1}{\sigma_2}$
```

If a smaller response is preferred, we may minimize the total expected response $n_1\mu_1 + n_2\mu_2$, subject to fixing the variance as a constant. This leads to an allocation ratio of