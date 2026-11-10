![](bbox=[0.105, 0.07, 0.895, 0.45])

FIGURE 12.3 The false position method on $[-\pi, \pi]$.

```
~~~
sage: phi(s, t) = (s + t) / 2
sage: bisection = intervalgen(f, phi, a, b)
sage: iterate(falsepos)
After 15 iterations: 2.15846441170219
sage: iterate(bisection)
After 20 iterations: 2.15847275559132
~~~
```

# **Newton's Method.**

Like the false position method, Newton's method uses a linear approximation of the function $f$. From a graphical point of view, we consider a tangent to the graph of $f$ as approximating this graph.

We assume that $f$ is differentiable and the derivative $f'$ has the same sign in the interval $[a,b]$; hence $f$ is monotone. We also assume that $f$ changes sign in the interval $[a,b]$. The equation $f(x)=0$ then has a unique solution in this interval; we denote it by $\alpha$.

Let $u_0 \in [a,b]$. The tangent to the graph of $f$ at the point of $x$-coordinate $u_0$ has equation

$$ y = f'(u_0)(x-u_0)+f(u_0). \qquad (12.2) $$

The coordinates of intersection of this line with the $x$-axis are

$$ (u_0 - f(u_0)/f'(u_0), 0). $$