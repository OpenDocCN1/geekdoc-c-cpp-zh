```
```
sage: integrate(1/(1+x^2), x, -infinity, infinity)
pi
sage: integrate(exp(-x**2), x, 0, infinity)
1/2*sqrt(pi)
```
```

```
```
sage: integrate(exp(-x), x, -infinity, infinity)
Traceback (most recent call last):
...
ValueError: Integral is divergent.
```
```

**EXAMPLE.** Let us compute, for $x\in\mathbb{R}$, the integral $\varphi(x)=\int_0^{+\infty}\frac{x\cos u}{u^2+x^2}\,du$.

```
```
sage: u = var('u'); f = x * cos(u) / (u^2 + x^2)
sage: assume(x>0); f.integrate(u, 0, infinity)
1/2*pi*e^(-x)
sage: forget(); assume(x<0); f.integrate(u, 0, infinity)
-1/2*pi*x
```
```

We thus have: $\forall x\in\mathbb{R}^*,\ \varphi(x)=\frac{\pi}{2}\cdot\operatorname{sgn}(x)\cdot e^{-|x|}$.

To compute numerically an integral on an interval, we have at our disposal the `integral_numerical` function, which returns a pair, whose first value is the approximation of the integral, while the second value is an estimate of the corresponding error.

```
```
sage: integral_numerical(sin(x)/x, 0, 1)
(0.946083070367183, 1.0503632079297087e-14)
sage: g = integrate(exp(-x**2), x, 0, infinity)
sage: g, g.n()
(1/2*sqrt(pi), 0.886226925452758)
sage: approx = integral_numerical(exp(-x**2), 0, infinity)
sage: approx
(0.886226925452758, 1.714774436012769e-08)
sage: approx[0]-g.n()
-1.11022302462516e-15
```
```

**Exercise 7** (The BBP formula (*)). Let us establish by a symbolic computation the BBP formula (or Bailey–Borwein–Plouffe formula); this formula directly gives the $n$-th digit of $\pi$ in radix 2 (or 16) without computing the previous digits, and with very little memory usage and time. For $N\in\mathbb{N}$, let us define

$$S_N=\sum_{n=0}^{N}\left(\frac{4}{8n+1}-\frac{2}{8n+4}-\frac{1}{8n+5}-\frac{1}{8n+6}\right)\left(\frac{1}{16}\right)^n.$$

+   1. Consider the function $f\colon t\longmapsto 4\sqrt{2}-8t^3-4\sqrt{2}\,t^4-8t^5$. For $N\in\mathbb{N}$, express the following integral as a function of $S_N$:

$$I_N=\int_0^{1/\sqrt{2}} f(t)\left(\sum_{n=0}^{N} t^{8n}\right)\,dt.$$