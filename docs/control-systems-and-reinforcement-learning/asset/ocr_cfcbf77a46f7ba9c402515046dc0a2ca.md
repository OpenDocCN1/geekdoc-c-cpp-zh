# ODE Methods for Algorithm Design

![](bbox=[0.168, 0.075, 0.831, 0.203])

**Figure 4.7** Evolution of $Z_t = (1+t)\hat{\Theta}_t$ using quasi Monte Carlo estimates for range of gains.

Details of this theory are postponed to Section 4.9. Here we simply illustrate the conclusion with a simple example. Consider the linear QSA ODE of the vector field

```
$f(\theta
```

In this special case, (4.85) is independent of $	heta$:

```
$$\bar{\Xi}_t(0) = \bar{\Xi}_t = B \int_0^t \xi_r \ dr.$
```

The coupling result (4.85) is illustrated using the simple Monte Carlo example, where plots are shown in Figure 4.3. The representation (4.53) is easily modified to take the form (4.86). First, by letting $\xi_t^0$ a periodic function of time whose sample paths define the uniform distribution on $[0,1]$; For any continuous function $c$,

```
$$\lim_{T\to\infty} \frac{1}{T} \int_0^T c(\xi_t^0) \ dt = \int_0^1 c(x)dx.$
```

We previously used the sawtooth function, $\xi_t^0 = t (\text{mod 1})$. Introduce a gain $g > 0$, and consider

```
$$\frac{d}{dt}\Theta_t = \frac{g}{1+t}[y(\xi_t^0) - \Theta_t].\quad\ (4.87)$
```

This is of the result from (4.86) with $A = -1$, and $\xi_t = [y(\xi_t^0) - \theta^*]$. Theorem 4.24 implies the coupling result (4.85) only for $g > 1$. Figures 4.3 and 4.4 illustrate the qualitative conclusion of Theorem 4.24. Coupling is illustrated in Figure 4.7. The scaled error $g^{-1}Z_t$ is constant since $\xi_t$ grows linearly with $g$. We expect $g^{-1}Z_t \approx \int_0^t y(\xi_r^0) - O(dr)$ for large $t$.

The figure compares results using 10 gains, approximately spaced on a logarithmic scale. The smallest gain is $g=1.5$, and all other gains satisfy $g \ge 2$. Theorem 4.24 asserts that $|Z_t - |\xi|] = O([1+t]^{-\delta_s})$, where $\delta_s < 0.5$ for $g=1.5$, and $\delta_s = 1$ for $g \ge 2$. The initial condition was set to $\Theta_0 = 10$ in each experiment. The scaled results $\{g^{-1}Z_t : 95 \le t \le 100\}$ are nearly indistinguishable when $g \ge 2$.

# 4.5.5 Constant Gain Algorithm

The choice $a_t = \alpha$ (independent of time) is often favored in practice. For the linear model (4.86), this is not unreasonable, as we will see in the following. The highlight is Corollary 4.17, establishing the optimal rate of convergence when PJR averaging.