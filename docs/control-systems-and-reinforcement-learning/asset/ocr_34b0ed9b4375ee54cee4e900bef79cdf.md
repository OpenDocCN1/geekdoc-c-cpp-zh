# 6.6 Lyapunov Functions

and from this we obtain a dynamic programming equation:

```
$h_{\gamma} = c + \gamma Ph_{\gamma}$. (6.33)
```

If $c$ is nonnegative valued, the lower bound $h_{\gamma}(x) \geq c(x)$ holds, so that the discounted cost is unbiased whenever this is true of $c$. And, again, we obtain a bound on $h_{\gamma}$ under Poisson's inequality.

**Proposition 6.5** If (6.27) holds with $V \geq 0$ everywhere, $h_{\gamma}(x) \leq V(x) + \bar{\eta}(1-\gamma)^{-1}$ for each $x$, and $\gamma \in (0,1)$.

Proof The bound (6.27) gives

```
$\gamma PV \leq V - g + \gamma\bar{\eta}$. (6.34)
```

where $g = (1-\gamma)V + \gamma c$, is a convex combination of the Lyapunov function and the cost function. Applying $\gamma P$ to each side gives

```
$(gamma P)^2V \leq \gamma PV - Pg + \gamma^2\bar{\eta}$.
```

and then, using (6.34),

```
$(gamma P)^n V \leq V - g - \sum_{k=0}^{n-1} \gamma^k P^k g + \bar{\eta} \sum_{k=0}^{n-1} \gamma^k k+1$.
```

As in the average-cost problem, we obtain the following by induction:

From the definition $g = (1-\gamma)V + \gamma c$, we obtain

```
$\sum_{k=0}^{\infty} \gamma^k P^k c(x) + (1-\gamma) P^k V(x) \leq V(x) + \frac{\bar{\eta}}{1-\gamma}$. (6.35)
```

Using the fact that $V \geq 0$, we can drop all term involving $V$ on the left-hand side of (6.35) to obtain the following:

```
$(1-\gamma)V(x) + \gamma \sum_{k=0}^{\infty} \gamma^k P^k c(x) \leq V(x) + \frac{\bar{\eta}}{1-\gamma}$.
```

The bound $h_{\gamma} \leq V + \bar{\eta}(1-\gamma)^{-1}$ by subtracting $(1-\gamma)V(x)$ from each side, and dividing each side by the resulting inequality by $\gamma$.

**Example 6.4.1** Discounted Cost for the Linear State Space (Model) with cost $c(x) = \frac{1}{2}x^2$, the solution to Poisson's equation was obtained in (6.30). Proposition 6.5 gives the bound $h_{\gamma} \leq V + \bar{\eta}(1-\gamma)^{-1}$, in which this case becomes

```
$h_{\gamma}(x) \leq \frac{1}{1-\\alpha^2}[x^2 + \frac{\sigma^2}{1-\gamma}]$. (6.36)
```

We next compute $h_{\gamma}$ to see if this bound is accurate. For this, we begin with the dynamic programming equation (6.33). We let $V(x) = A_{\gamma} + \frac{1}{2}\kappa\gamma x^2$, with $A_{\gamma}, \kappa_{\gamma}$ constants to be chosen. From (6.29), we have

```
$PV \leq \alpha^2 V + (1-\alphaalpha^2)A_{\gamma} + \frac{1}{2}\kappa_{\gamma}\sigma^2$.
```