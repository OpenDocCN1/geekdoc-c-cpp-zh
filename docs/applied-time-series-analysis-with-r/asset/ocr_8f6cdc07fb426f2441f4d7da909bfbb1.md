# Stationary Time Series

1. In Example 1.3

$X(t) = C\cos(\lambda t + Y),$

where, as before, C and $\lambda$ are real-valued constants, and we examine the special case in which $Y \sim \text{Uniform} [0, 2\pi]$. We recall from Example 1.3 that $\mu=0$ and $\gamma(h) = (C^2)/cos(\lambda h)$. Thus, $\gamma(h)$ is a periodic function of period $2\pi/\lambda$ or said another way, $\gamma(h)$ has a frequency $\lambda/(2\pi)$. The spectrum as defined in Equation 1.23

```
$P_X(f) = \int_{-\infty}^{\infty} e^{-2\pi fh} \gamma(h)dh,$
```

```
$P_X(f) = \frac{C^2}{2} \int_{-\infty}^{\infty} e^{-2\pi fh} \cos(\lambda h)dh$
```

```
$P_X(f) = \frac{C^2}{4} \int_{-\infty}^{\infty} [\delta(f-\frac{\lambda}{2\pi}) + \delta(f+\frac{\lambda}{2\pi})]dh,$
```

where $\delta$ denotes the Dirac delta function.
Remark: The integral in Equation 1.32 is not convergent if one considers it as an improper Riemann integral. Moreover, the $\delta$-function in Equation 1.33 is not really a function but instead a function. Nevertheless, the results of Equations 1.32 and 1.33 can be made rigorous by interpreting the integral in Equation 1.32 as a “sequence of $\delta$ integrals and by interpreting $\delta$ as a “generalized function.”

For discussions of generalized functions, see Kanwal (1998) and Lighthill (1959). Properties of the Dirac function that we need in this book are:

```
$$\int_{-\infty}^{\infty} \delta(t-t_0)f(t)dt = F(t_0).$
```

```
$$\int_{-\infty}^{\infty} e^{-2\pi itu} du = \delta(t).$
```

Figure 1.14 shows a plot of $P_X(f)$ given in Equation 1.33 for $f \ge 0$ and for the special case $\lambda=0.2\pi$. The fact that “frequency content” of the data is concentrated at the single frequency $\lambda/(2\pi)=0.1$ is indicated by the infinite spike at 0.1.