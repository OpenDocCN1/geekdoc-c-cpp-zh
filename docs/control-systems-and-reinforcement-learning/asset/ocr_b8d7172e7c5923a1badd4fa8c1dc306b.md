# Control Crash Course

${x \in X : V(x) \leq V(x^0)\}$ is a bounded set for $x^0 \in X$.

That is, the set $S_V(r)$ takes on one of three forms for any $r$: $S_V(r) = X$, or $S_V(r) \subset X$ is bounded.

In most cases, we find that $S_V(r) = X$ is impossible, so that we arrive at the stricter coercion assumption:

![](bbox=[0.145, 0.165, 0.395, 0.258])

**Figure 2.4** Inf-compact and coercive.

```
$$\lim_{|x| \to \infty} V(x) = \infty$.
```

(the function on the left is bounded). In this case, under our standing assumption (2.22), the set $S_V(r)$ is either empty or bounded for each $r$. Figure 2.4 illustrates the two classes of functions with $X = \mathbb{R}$ here are three numerical examples:

+   (i) $V(x) = x^2$ is coercive (2.29).
(ii) $V(x) = x^2/(1+x^2)$ is inf-compact but not coercive: $S_V(r) = \mathbb{R}$ for $r \geq 1$, and $S_V(r) = [-a, a]$ (a bounded interval) for $0 \leq r < 1$, with $a = \sqrt{r/(1-r)}$.
(iii) $V(x) = e^x$ is neither: $S_V(r) = (-\infty, \log(r))$ is not a bounded subset of $\mathbb{R}$ for $r > 0$.

The function $J$ satisfies the intuitive properties of a Lyapunov function under $c$ and the value function $J$ defined in (2.24) are nonnegative and finite valued.

+   $J(x(k))$ is nonincreasing, and $\lim_{k \to \infty} J(x(k)) = 0$ for each initial condition.
(ii) In addition that $J$ is continuous, inf-compact, and vanishes only at $x^c$. Then, for each initial condition, $lim(k) = x^c$.

The proof is postscribed to Section 2.4.4, but we note here the first steps: the dynamic programming equation (2.25) implies that for each $k \geq 0$,

```
$J(x(k+1)) = J(x(k)) - c(x(k)) \leq J(x(k)).
```

That is, $J(x(k))$ is nonincreasing, so that $x(k) \in S_J(r)$ for each $k \geq 0$, with $r = J(x(0))$. The inf-compact assumption implies that the state trajectory is “bottled-up” in the bounded set $S_J(r)$.

In the context of total-cost optimal control, the basic drift inequality in this book is *Poisson’s inequality*: for nonnegative functions $V, c: X \to \mathbb{R}_+$, and a constant $\eta \geq 0$,

```
$V(F(x)) \leq V(x) - c(x) + \eta$.
```

The reference to a French mathematician is explained in the notes. Poisson’s inequality is a relaxation of the dynamic programming equation (2.25) through the introduction of $\eta$, as well as the inequality.

Poisson’s inequality is defined with attention to the dynamics: on combining (2.31) and (2.21), we obtain (similar to 2.30))

```
$V(x(k+1)) \leq V(x(k)) - c(x(k)) + \eta, \quad k \geq 0$.
```