# Fundamentals of Dependability

The mean time to failure is

```
$MTTF = \frac{k}{\lambda} \quad (16.3.25)$
```

The variance of the time to failure is

```
$Var(TTF) = \frac{k}{\lambda^2}. \quad (16.3.26)$
```

# Cox Distributions

As mentioned in Chapter 5 and Section 13.3.8, the advantage of using phase-type distributions is the fact that they can approximate any non-negative distribution closely. Cox distributions can be adopted to match the first central moment about the origin (mean) and the second central moment (variance) of empirical devices' lifetime. For details about this process, please refer to Section 13.3.8.

**Weibull Distribution** is widely used in reliability and life data analysis due to its versatility. In general, it is defined by three parameters, $\alpha \in \mathbb{R}$ ("shape parameter"), $eta \in \mathbb{R}^+$ ("scale parameter"), and $\mu \in \mathbb{R}^+$ ("location parameter"). In addition, the distribution has support on the interval $[\mu, \infty)$.

The value of $\alpha$ modifies the shape of the failure rate (see Figure 16.10). Values below one ($\alpha<1$) specify a failure rate that decreases with time. If $\alpha = 1$, the failure rate is constant ($\alpha<1$ is an exponential distribution). Failure rates increasing with time are obtained when $\alpha > 1$.

```
$\lambda(t) = \frac{(t-\\mu)^{\alpha-1}}{\beta}, \quad t \geq \mu. \quad (16.3.27)$
```

![](bbox=[0.215, 0.606, 0.781, 0.856])

**Figure 16.10** Hazard Function - $\alpha = 0.6, \alpha = 1$, and $\alpha = 4 - \mu = 0$ and $\beta = 10$.