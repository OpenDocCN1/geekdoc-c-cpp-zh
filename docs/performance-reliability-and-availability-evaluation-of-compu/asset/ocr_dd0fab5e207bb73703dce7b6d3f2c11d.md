# Fundamentals of Dependability

Standard deviation:

```
$$SD(TTF) = \frac{\pieta}{\sqrt{3}}$ $\quad (16.3.47)$
```

**The Loglogistic Distribution** is similar to the logistic distribution. Lifetime data follows a loglogistic distribution if the natural logarithms to failure obey a logistic distribution. The relation between the logistic and logistic distribution is similar to the relation between normal and lognormal distributions. Accordingly, the loglogistic and lognormal distributions share many similarities. This distribution is continuous, supported over the interval $[0, \infty)$, and is parametrized by two positive real numbers $\gamma$ ("shape parameter") and $\sigma$ ("scale parameter").

PDF:

```
$$f(t) = \frac{\gamma\sigma^{-\gamma}t^{\gamma-1}}{\left(\frac{t}{\sigma}ight)^\gamma + 1}$ $\quad (16.3.48)$
```

CDF:

```
$$F(t) = \frac{1}{\left(\frac{t}{\sigma}ight)^\gamma + 1}$ $\quad (16.3.49)$
```

Reliability:

```
$$R(t) = \frac{1}{\left(\frac{t}{\sigma}ight)^\gamma}$ $\quad (16.3.50)$
```

Hazard function:

```
$$\lambda(t) = \frac{\gamma}{\left(\frac{t}{\sigma}ight)^\gamma + 1}$ $\quad (16.3.51)$
```

Mean time to failure:

```
$$MTTF = \frac{\pi\sigma\csc\left(\frac{\pi}{\gamma}ight)}{\gamma} \quad \gamma > 1.$ $\quad (16.3.52)$
```

Standard deviation:

```
$$SD(TTF) = \sqrt{\frac{\pi\sigma\sqrt{2\gamma\csc\left(\frac{2\pi}{\gamma}ight)-\pi\csc^2\left(\frac{\pi}{\gamma}ight)}}{\gamma}} \quad \gamma > 2.$ $\quad (16.3.53)$
```