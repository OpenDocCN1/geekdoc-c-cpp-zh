# 124 ODE Methods for Algorithm Design

where $\delta_t \geq 0$ for each $t$. Define $\gamma_t = \alpha_t - \delta_t$ and obtain, with $u_t = eta_t\gamma_t$ as before,

```
$x_t = \int_0^t u_s \exp(\\int_0^s \beta_r \ dr) ds \leq \int_0^t \beta_s\alpha_s \exp(\\int_0^s \beta_r \ dr) ds.$
```

Using $z_t = x_t + \gamma_t \leq x_t + \alpha_t$ then gives (i).

We establish (ii): If the function is nondecreasing, then from part (i) and the assumption that $\beta$ is nondecreasing,

```
$z_t = \alpha_t + \alpha_t \exp(\\int_0^t \beta_r \ dr) ds, \quad 0 \leq t \leq T.$
```

This bound implies (ii) by substituting

```
$\beta_s \exp(\\int_0^t \beta_r \ dr) ds = \exp(\\int_0^t \beta_r \ dr) - 1.$
```

Grönwall's Inequality provides a crude bound that is needed in approximations:

**Proposition 4.19** Consider the ODE (4.2), subject to the Lipschitz condition (4.5). Then,

+   (i) There is a constant $B_f$ depending only on $t$ such that

```
$|\partial_t|| \leq (B_f + ||\theta_0||)e^{Lt} - B_f, \quad (4.108a)
```

```
$|\partial_t - \theta_0|| \leq (B_f + ||\theta_0||)e^{Lt}, \quad t \geq 0. \quad (4.108b)
```

+   (ii) If there is an equilibrium $\theta^*$, then for each condition,

```
$|\partial_t - \theta^*|| \leq ||\theta_0 - \theta^*||e^{Lt}, \quad t \geq 0.$
```

*Proof* We present a complete proof of (ii) and 4.108a (the proof of (4.108b) is similar).

If there is an equilibrium $\theta^*$, this means that $f(\theta^*) = 0$. The proof of (4.108b) begins with (4.3), in the form

```
$\partial_t - \theta^* = \theta_0 - \theta^* + \int_0^t f(\partial_\tau) d\tau, \quad 0 \leq t \leq T.$
```

Under the equilibrium condition and the Lipschitz assumption,

```
$|f(\partial_t)|| \leq ||f(\partial_t) - f(\theta^*)|| \leq L|\partial_t - \theta^*||.$
```

Writing $z_t = ||\partial_t - \theta^*||$, combined with (4.3) gives

```
$z_t \leq z_0 + L \int_0^t z_\tau d\tau, \quad 0 \leq t \leq T.$
```

Grönwall's Inequality gives us (ii): Apply Proposition 4.2 (ii) using $\beta_t = L$ and $\alpha_t = z_0$.

To establish, take any $\theta^* \in \mathbb{R}^d$ and use the Lipschitz condition to obtain

```
$|f(\theta)|| \leq ||f(\theta) - f(\theta^*)||| + ||f(\theta^*)|| \n\leq L|\theta - \theta^*|| + ||f(\theta^*)|| \n\leq L|\theta|| + L|\theta^*|| + ||f(\theta^*)|||.$
```