![](bbox=[0.196, 0.113, 0.778, 0.343])

i.e. for a given value, $x, F(x)$ is the probability that observed value of a random variable $X$ will be at most $x$ less than or equal to $x$. For EVT there is a different function to consider based on a conditional probability (in a similar way to how the conditional expectation models the ES). That is, for an excess distribution of the return variable $X$ over a certain threshold $u$, the conditional probability distribution of $y = X - u$ such that $X > u$ can be written as:

$F_u(y) = P(X - u \le y|X > u) \quad (7.11)$

The CDF is now the probability that $y = X - u$ i.e. the excess (or exceedance) of the threshold is less than or equal to conditional on $X$ exceeding the threshold $u$ (Figure 7.12). One of the main theorems of EVT developed by Pickards (1975) states that for a reasonably high threshold, $u, F_u(y)$ can be approximated by the GPD which can be written as:

```
$G(X) = \begin{cases} 1 - (1 + \frac{\xi y}{\beta})^{-1/\xi} & \text{if } \xi \neq 0 \ 1 - \exp(-\frac{y}{\beta}) & \text{if } \xi = 0 \end{cases} \quad (7.12)$
```

where $y = X - u, \xi = 1/\alpha$ is the shape parameter, $\alpha$ the tail index and $\beta$ a simple scaling parameter. There are several approaches to estimating the parameters in (7.12), such as *maximum likelihood, elemental percentile method and the method of moments* described in the studies by Hosking and Wallis (1987), Grimshaw (1993) and Castillo and Hadi (1997).