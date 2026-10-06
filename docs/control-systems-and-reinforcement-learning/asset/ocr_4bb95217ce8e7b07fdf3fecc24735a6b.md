# Example: The Scalar Linear State Model

Consider the scalar model,

```
X(k+1) = \alpha X(k) + N(k+1), \quad k \geq 0, \quad (6.28)
```

where $N$ i.i.d., with zero mean and finite second moment $\sigma_N^2$ (not necessarily Gaussian).
The cost function is the quadratic, $c(x) = \frac{1}{2}x^2$.
Let $V(x) = \frac{1}{2}\kappa x^2$, with $\kappa > 0$. We then have the following:

```
$PV(x) = E[V(X(k+1)) \mid X(k)=x]\\= \frac{1}{2}\kappa(\alpha x + N(1))^2\\= V(x) + \frac{1}{2}\kappa(\alpha^2 - 1)^2 + \frac{1}{2}\kappa\sigma_N^2., \quad (6.29)
```

Provided $|\alpha| < 1$, we can set $\kappa = (1-\alpha^2)^{-1}$ in the definition of $V$ to obtain a solution to Poisson's equation with forcing $\eta$

```
$PV(x) = V(x) + \eta(x), \quad with \ \eta = \frac{1}{2}(1-\alpha^2)^{-1}\sigma_N^2., \quad (6.30)
```

It follows from Proposition 6.4 that $\eta(x) \leq \Gamma$ each $x$. In fact, the preceding steps show that $E[\eta(X(k))] \to \bar{\eta}$ for each initial condition, so we have equality: $\eta(x) = \bar{\eta}$.\nIf $N$ is Gaussian, then $P^k(x, \cdot)$ converges to a Gaussian $N(0, \sigma_{\eta}^2)$ distribution as $k \to \infty$, with $\sigma_{\eta}^2 = (1-\alpha^2)^{-2}\sigma_N^2$.

# 6.6.2 Discounted Cost

*In the long run we are all dead.* This quote is attributed to John Maynard Keynes, and is commonly used to justify the use of discounting in optimal control. I believe this is a mistake in most control applications. However the discount to obtain is based on a false impression that the average cost $\eta(x)$ only reflects the cost “at infinity.” Lyapunov bounds and their consequences, as the elementary bounds in (6.4), indicate that a policy with steady-state behavior will have good transient behavior. In particular, if the average cost is finite, then there is a solution to (6.27), from which we obtain the transient presented in Proposition 6.4.

However, the discounted criterion is sometimes convenient because it is easier to analyze, and I am also forced to cover this performance criterion because it is preferred in many disciplines (in particular, operations research and economics).
The discounted-cost function was introduced briefly in Section 6.4: Given a parameter $\gamma \in (0,1)$, the discounted cost from initial condition $x$ is defined as the sum:

```
$h_{\gamma}(x) = \sum_{k=0}^{\infty} \gamma^k E[c(X(k)) \mid X(0)=x]. \quad (6.31)
```

Once again, this has the operator-theoretic form:

```
$h_{\gamma} = \sum_{k=0}^{\infty} \gamma^k P^k c., \quad (6.32)
```