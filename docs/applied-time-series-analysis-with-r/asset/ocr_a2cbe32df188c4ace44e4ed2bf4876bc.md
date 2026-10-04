# 3.1.1 MA(1) Model

Let $X_i$, be the MA(1) process defined by

```
$X_i - \mu = a_i - \theta_1 a_{i-1}\n= (1 - \theta_1 B)a_i. \quad (3.9)$
```

From Equations 3.2 and 3.3, we obtain

```
$$\gamma_0 = \sigma_a^2[1 + \theta_1^2] = \sigma_X^2\n\gamma_1 = \sigma_a^2[-\theta_1]\n\gamma_j = 0, \quad j > 1. \quad (3.10)$
```

Thus, for an MA(1) process,

```
$$\rho_0 = 1\n\rho_1 = \frac{-\theta_1}{1 + \theta_1^2}\n\rho_j = 0, \quad j > 1. \quad (3.11)$
```

It is easily shown that the function $f(u) = |u|/(1 + u^2)$ has a maximum of 0.5 at $u = \pm1$, from which it follows that for an MA(1) process, $|\rho_1| = 0.5$. In particular, $\rho_1 = 0.5$ when $\theta_1 = -1$ and $\rho_0 = -0.5$ when $\theta_1 = 1$. From Equation 3.66, the spectral density of an MA(1) is given, for $|f| \leq 0.5$, by

```
$S_X(f) = \frac{|1 - \sum_{j=1}^q \theta_j e^{-2j\pi f}|^2}{1 + \sum_{j=1}^q \theta_j^2}\n= \frac{|1 - \theta_1 e^{-2\pi f}|^2}{1 + \theta_1^2}\n= \frac{1}{1 + \theta_1^2}[1 - \theta_1 e^{-2\pi f}][1 - \theta_1 e^{2\pi f}]\n= \frac{1}{1 + \theta_1^2}[1 - 2\theta_1 \cos 2\pi f]\n= 1 - \frac{2\theta_1 \cos 2\pi f}{1 + \theta_1^2}. \quad (3.12)$
```

As noted in Chapter 1, the spectral density provides information concerning the periodicities in the data. From Equation 3.12, $S_X(f)$ for an MA(1)