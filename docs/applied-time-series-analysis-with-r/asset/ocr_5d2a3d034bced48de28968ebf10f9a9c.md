# ARMA Time Series Models

```
$f_0 = \frac{1}{2\pi} \cos^{-1} \left(\frac{1.6}{2\sqrt{-\phi_2}}\right) \quad (3.71)$
```

Therefore, if $\phi_2 = -1$, the associated frequency is $f_0 = 0.1024$.
Notice that changing $\phi_1$ in Equation 3.71 while keeping $\phi_2 = 1.6$ fixed, changes the associated system frequency. For the AR(2) models in Equation 3.70, we obtain $f_0 = 0.05, 0.09$, and $0.10$ for $\phi_0 = -0.7, -0.9$, and $-0.98$. The strong periodic nature of the autocorrelations is clear when $\phi_2$ is close to $-1$, and in this example, it diminishes as $\phi_2 \to -0.7$. Realizations of length $n = 200$ from Equation 3.70 are shown in Figure 3.13, where the effects of the differing autocorrelation structures can be seen. Specifically, as $\phi_2 \to -1$ the periodicity becomes more apparent in the realizations, the period becomes shorter, and the process variance increases. In Figure 3.14, the corresponding spectral densities are displayed where it is seen as $\phi_2 \to -1$, the peak of the spectral density becomes sharper.

As discussed previously, the AR(2) process $(1 - \phi_1 B - \phi_2 B^2)X_t = a$, has complex roots if only $\phi_1^2 + 4\phi_2 < 0$. Therefore, it is necessary that

![](bbox=[0.285, 0.497, 0.693, 0.668])

![](bbox=[0.133, 0.693, 0.856, 0.883])

FIGURE 3.13
Realizations from the AR(2) models $X_t - 1.6X_{t-1} - \phi_2 X_{t-2} = a_t$, (a-c) $\phi_2 = -0.7, -0.9, -0.98$.