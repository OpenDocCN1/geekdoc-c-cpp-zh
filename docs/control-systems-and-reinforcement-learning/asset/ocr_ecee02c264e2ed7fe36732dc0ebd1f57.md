# Control Crush Course

![](bbox=[0.21, 0.07, 0.79, 0.318])

**Figure 2.5** If $V$ is a Lyapunov function, then $V(x_t)$ is nonincreasing with time.

![](bbox=[0.243, 0.368, 0.756, 0.455])

**Figure 2.6** Geometric interpretations of a Lyapunov drift condition: the gradient $
abla V(x)$ is orthogonal to the set $\{y : V(y) = V(x)\}$, which is the boundary of the set $S_V(r)$ with $r = V(x)$.

**Proposition 2.5** If there exists a Lyapunov function $V$ satisfying the assumptions for global asymptotic stability, the equilibrium $x^*$ is globally asymptotically stable.

Proposition 2.5 is a partial extension of Proposition 2.3 to the continuous time model. A full extension requires $c: \mathbb{R}^n 	o \mathbb{R}_+$ is continuous, $V: \mathbb{R}^n 	o \mathbb{R}_+$ is continuously differentiable, and $\eta \geq 0$ is a constant, jointly satisfying

```
$(\nabla V(x),f(x)) \leq -c(x) + \eta, \quad x \in X.$
```

An application of the chain rule implies that this is a continuous time version of (2.31):

```
$$\frac{d}{dt}V(x_t) \leq -c(x_t) + \eta, \quad t \geq 0.$
```

And with a bit more work, we reach the following conclusions:

**Proposition 2.6** If (2.39) holds for nonnegative $c,V,\eta$, then

```
$V(x_T) + \int_{0}^{T} c(x_t) dt \leq V(x_0) + T\eta, \quad x_0 \in X, T > 0.$
```

If $\eta = 0$, then the total cost is finite:

```
$$\int_{0}^{\infty} c(x_t) dt \leq V(x), \quad x_0 \in X.$
```