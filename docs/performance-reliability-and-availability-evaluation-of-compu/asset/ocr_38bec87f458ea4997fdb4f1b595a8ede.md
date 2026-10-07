# Lifetime Data Analysis

# Dealing With Censoring

Above, we illustrated the maximum likelihood method for complete lifetime sets. Often, however, these sets contain censored data. For example, consider an experiment where n devices are observed, which finishes as soon as r failures occur. In In such a case, we are dealing with the right-censored of type II. Hence, lifetime data consider another term in its likelihood function. As mentioned earlier, the first for the complete data uses the density function. The second term for representing the censoring takes into account the complementary cumulative density function. This extended likelihood function finishes as:

```
$L(\theta, |x_1, x_2, \dots, x_n) = \prod_{i=1}^n f(\theta|x_i) \ \times \prod_{j=r+1}^n (1 - F(x_j|\theta)), \quad (25.3.33)
```

where $n-r$ is the number of censored data points , $x_j$ is the $j^{th}$ suspension, and $F(x_j|\theta)$ is the cumulative distribution, and $	heta$ are the set parameters of the distribution. The complementary cumulative density function, the second term of the likelihood function, is the survival function at $t$, and we can think of it as a weighting function applied to the density function. It is worth noting that the survival function at $t=0$ is one.

With this likelihood function, the analysis process proceeds as described previously: take the likelihood function and its partial derivatives concerning the parameters. The likelihood function for the censored lifetime data highlights some of the advantages the maximum likelihood method analysis has over other parameter estimation techniques.

Assume the TTFs are exponentially distributed with rate $\lambda_i$; suspension, we may adopt

```
$L(\lambda, |x_1, x_2, \dots, x_n) = \prod_{i=1}^r e^{-\lambda_i t_i} \ \times \prod_{j=r+1}^n e^{-\lambda_j t_j}. \quad (25.3.34)
```

Thus we

```
$L(\lambda, |x_1, x_2, \dots, x_n) = \lambda_r^r e^{-\lambda_i t_i} \ \times \prod_{j=r+1}^n e^{-\lambda_j t_j}
```

```
$L(\lambda, |x_1, x_2, \dots, x_n) = \lambda_r^r e^{-\lambda_r \sum_{i=1}^r t_i} e^{-\lambda^n t_r}
```

```
$L(\lambda, |x_1, x_2, \dots, x_n) = \lambda_r^r e^{-\lambda_r \sum_{i=1}^r t_i}
```

as the likelihood function. Differentiating $L(\lambda, |x_1, x_2, \dots, x_n)$ with respect to $\lambda$

```
$$\frac{\partial L(\lambda, |x_1, x_2, \dots, x_n)}{\partial \lambda} = \frac{\partial(\lambda_r^r e^{-\lambda_r \sum_{i=1}^r t_i})}{\partial \lambda}}$
```