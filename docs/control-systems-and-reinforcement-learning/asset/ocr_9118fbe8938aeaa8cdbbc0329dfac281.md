# 4.6 Gradient-Free Optimization

![](bbox=[0.115, 0.073, 0.883, 0.243])

(a) PGR estimate: nearly optimal

**Figure 4.10** Minimizing a loss function with multiple local minima: While $\Gamma(\Theta_t)$ is highly oscillatory, the estimate $\hat{\Theta}_T^\Gamma$ is nearly optimal (obtained by averaging the final 20% of estimates).

These metparameters were obtained by trial and error: If $ar{a}$ or $\varepsilon$ is too small, then we are sometimes trapped in a local minima.

The ODE was approximated using a standard Euler scheme with 1 sampling: The crude ODE approximation leads to the requirement that $\omega_1/\omega_2$ is irrational. The two plots on the right-hand side of Figure 4.10 show the evolution of $\Theta_t$ in $\mathbb{R}^2$ with $0 \leq t \leq 5 	imes 10^4$, with $\Theta_0 = (-2, 2)$. The plots indicate that the estimates exhibit significant variation throughout the run, but in plot (c) it is clear that they are trapped within the region of attraction of the global minimum.

What's more, averaging is highly successful: The estimate $\hat{\Theta}_T^\Gamma$ was obtained as the average of $\Theta_t$, over the final 20% of the run. It is found that $\Gamma(\hat{\Theta}_T^\Gamma)$ is only a small fraction of 1% greater than $\Gamma(	heta^0)$.

# 4.6.2 A Menu of Algorithms

In each of the algorithms defined, it is assumed that the process $\Psi$ is the sum of two terms: $\Psi_t = \Theta_0 + \varepsilon\Xi_t, t \geq 0$, where $\varepsilon > 0$, and $\Xi_t$ is a $d$-dimensional probing signal. For simplicity, we impose the normalization conditions unless otherwise stated:

```
$$\lim_{T\to\infty} \frac{1}{T} \int_{t=0}^T \Xi_t \ dt = 0, \quad \frac{1}{T} \int_{t=0}^T \Xi_t\Xi_t^T \ dt = I. \quad (4.95)$
```

This is easily arranged using a mixture of sinusoids.
The first is the simplest:

**SGD #1**

For a given $d \times d$ positive definite matrix $G$, and $\Theta_0 \in \mathbb{R}^d$,

```
$$\dot{\Theta}_t = -a_t - \frac{1}{\varepsilon}G\Gamma(\Theta_t), \quad (4.96a)$
```

```
$$\Psi_t = \Theta_t + \varepsilon\Xi_t. \quad (4.96b)$
```