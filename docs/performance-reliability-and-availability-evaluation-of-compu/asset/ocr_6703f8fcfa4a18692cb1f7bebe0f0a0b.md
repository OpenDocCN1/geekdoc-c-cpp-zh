# 38 Performance Reliability, and Availability Evaluation of Computational Systems

```
$R(t) = \int_{t}^{\infty} e^{\frac{(\log(x)-\mu)^2}{2\sigma^2}} dx, \quad t \geq 0. \quad (16.3.39)$
```

Mean time to failure:

```
$MTTF = e^{\mu+\frac{\sigma^2}{2}}. \quad (16.3.40)$
```

Standard deviation of time to failure:

```
$SD(TTF) = \sqrt{(e^{\sigma^2}-1)e^{2\mu+\sigma^2}}. \quad (16.3.41)$
```

**The Logistic Distribution** has a shape very similar to the normal distribution, however with heavier tails. Since the logistic distribution has closed-form solutions for the $R(t)$, $CDF$, and $\lambda(t)$, it is sometimes favored over the normal distribution when modeling systems whose failure rates increase over time. The logistic distribution is supported over the set of real numbers and parametrized by $\mu$, the “mean” of the distribution, and a positive real number $eta$, called the “scale parameter".

PDF:

```
$f(t) = \frac{e^{\frac{t-\mu}{\beta}}}{\beta(e^{\frac{t-\mu}{\beta}}+1)}. \quad (16.3.42)$
```

CDF:

```
$F(t) = \frac{1}{e^{\frac{t-\mu}{\beta}}+1}. \quad (16.3.43)$
```

Reliability:

```
$R(t) = 1 - \frac{1}{e^{\frac{\mu-t}{\beta}}+1}}. \quad (16.3.44)$
```

Hazard function:

```
$$\lambda(t) = \frac{1}{e^{\frac{\mu-t}{\beta}}+1}}. \quad (16.3.45)$
```

Mean time to failure:

```
$MTTF = \mu. \quad (16.3.46)$
```