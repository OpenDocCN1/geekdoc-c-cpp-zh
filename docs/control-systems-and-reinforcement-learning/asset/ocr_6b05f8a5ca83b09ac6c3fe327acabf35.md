# Stochastic Approximation

and $\alpha_n = 1/n$. A similar recursion for arbitrary $N_0 < N$, the recursion begins at $n = N_0$ with $	heta_{N_0}^0 = 0$. This is equivalently expressed (8.10c)

```
$$\lim_{n\to\infty} \beta_n = \infty. \quad (8.22)$
```

This means that the estimates $\{	heta_n^*\}$ defined in (8.10a) evolve much more rapidly than $\{	heta_n^m\}$. The general two-time scale algorithm is described as:

```
$$\theta_{n+1} = \theta_n + \beta_n + f_1(\theta_n, \omega_n), \quad (8.23a)\n\omega_{n+1} = \omega_n + \alpha_n + g_1(\theta_n, \omega_n). \quad (8.23b)$
```

where $\{\theta_n\}$ evolves in $\mathbb{R}^d$ and $\{\omega_n\}$ evolves in $\mathbb{R}^m$. The assumption (8.22) is maintained, which is what makes this a two-time-scale.

The ODE approximation for these recursions will not be covered in any generality here, but the main message is something every user of SA should understand.

As always, we recall the mean vector fields $f(\	heta, \omega) = \mathbb{E}[f_1(\	heta, \omega)]$ and $\tilde{g}(\theta, \omega) = \mathbb{E}[g_1(\	heta, \omega)]$ (steady-state effects). For each $\omega \in \mathbb{R}^m$, assume there is a unique vector $\theta^*(\omega)$ solving $\tilde{g}(\theta, \omega) = 0$. Because of the second parameter sequence is so slow compared to the first, it is possible to prove under general conditions that $\theta_n \approx \theta^*(\omega_n)$ for large $n$. This leads to the following ODE approximation for the second recursion:

```
$$\frac{d}{dt} = \tilde{g}(\theta^*(w), w). \quad (8.24)$
```

See Theorem 8.3 for example of convergence theory based on these concepts. The insight is valuable in algorithm design:

+   (i) It is critical in constrained optimization, where $\omega_n$ is an approximation of a dual variable (say, in the setting of Proposition 4.12).
(ii) The approximation (8.24) is essential for recursive algorithms that approximate the Newton-Raphson flow, as we have already seen in the QSA section of Section 4.5.6.
(iii) The elegant design of actor-critic methods is possible through versions of the ODE approximation (8.24).

Stability for there two-time scale SA can be found in other sources, such as [66], where the proof of the following companion to Theorem 8.1 can be found:

**Theorem 8.3** Consider the two-time scale algorithm (8.23) subject to the following assumptions:
$f$ and $\tilde{g}$ are Lipschitz continuous, and the function $g(\	heta^*(w), w)$ is also Lipschitz in $w$.

+   ► The parameter sequences $\{\theta_n, \omega_n : n \geq 0\}$ are bounded a.s.
► The cumulative disturbances are bounded, in the sense that the sum exists and are everywhere finite with probability one:

```
$$\sum_{n=0}^{\infty} \beta_{n+1}\{f_1(\	heta_n, \omega_n) - \tilde{f}(\theta_n, \omega_n)\}, \quad \sum_{n=0}^{\infty} \alpha_{n+1}\{g_1(\	heta_n, \omega_n) - \tilde{g}(\theta_n, \omega_n)\}. \quad (8.25)$
```