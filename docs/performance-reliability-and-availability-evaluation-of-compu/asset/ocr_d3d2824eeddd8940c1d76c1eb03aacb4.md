# Fundamentals of Dependability

# Exponential Distribution

The reliability is specified by 16.2.8. If the failure rate function is constant, $\lambda(t) = \lambda$, then the reliability is

```
$R(t) = e^{-\int_{0}^{t} \lambda dt} = e^{-\lambda t}, \quad t \geq 0.$
```

The constant failure rate implies no aging or wear-out effects. The probability that a running system will operate for the next period $T$ is equal to that of a brand new system will operate for the same period $T$, since

```
$R(t|T) = \frac{R(t+T)}{R(T)} = e^{-\frac{\lambda (t+T)}{\lambda}},$
```

which results in

```
$R(t|T) = \frac{e^{-\lambda t} \times e^{-\lambda T}}{e^{-\lambda T}} = e^{-\lambda t} = R(t).$
```

The result presented above shows that the only continuous random variable with the memoryless property is the random variable exponentially distributed. The *CDF* of the is

```
$F_T(t) = 1 - e^{-\lambda t}, \quad t \geq 0,$
```

the density function is

```
$f_T(t) = \lambda e^{-\lambda t}, \quad t \geq 0,$
```

and the cumulative failure rate function is

```
$H(t) = \lambda \times t, \quad t \geq 0.$
```

As $MTFF = \int_{0}^{\infty} R(t) dt$, then the mean time to fail is

```
$MTFF = \int_{0}^{\infty} e^{-\lambda t} dt = \frac{1}{\lambda}.$
```

If the failure rate is constant, then a failure will never occur before a specified period, $t_0$, the exponential distribution with threshold would be adopted [115]. Now, $t_0$ is the location parameter that shifts the distribution to the right. Therefore,

```
$R(t) = e^{-\lambda (t-t_0)}, \quad t \geq 0,$
```

```
$F_T(t) = 1 - e^{-\lambda (t-t_0)}, \quad t \geq 0,$
```