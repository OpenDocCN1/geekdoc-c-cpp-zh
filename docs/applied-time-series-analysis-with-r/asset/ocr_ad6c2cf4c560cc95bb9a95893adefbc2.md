# 182 Applied Time Series Analysis with R

![](bbox=[0.147, 0.125, 0.477, 0.283])

![](bbox=[0.523, 0.125, 0.853, 0.283])

![](bbox=[0.147, 0.303, 0.477, 0.461])

![](bbox=[0.523, 0.303, 0.853, 0.461])

**FIGURE 4.1** Realizations from AR(2) and signal-plus-noise models. (a) $X_t - 1.55X_{t-1} + 0.8X_{t-2} = a_t$; (b) $Y_t = 4.4 \cos(2\pi/12 + U) + N_t$; (c) $X_t - 1.72X_{t-1} + 0.99X_{t-2} = a_t$; (d) $Y_t = 20 \cos(2\pi/12 + U) + N_t$.

the same, the variances of $X_t$ and $Y_t$ are the same, and the ratio of the process variance to noise variance is 10.7. That is, $\sigma_X^2/\sigma_N^2 = \sigma_Y^2/\sigma_N^2 = 10.7$. Also, both processes have a natural frequency of $f = 1/12$. To see this, that the system frequency associated with the AR(2) model of Equation 4.1 given by Equation 3.63 with $\phi_1 = 1.55$ and $\phi_2 = -0.8$ is $f_0 = 12$. In order to further compare these two types of models, Figure 4.1c and d shows realizations from

and

```
$$(1 - 1.72B + 0.99B^2)X_t = a_t,$$
```

```
$$Y_t = 20 \cos\left(\\frac{2\pi t}{12} + U\right) + N_t.$
```

These are analogous to Equations 4.1 and 4.2, but, in realizations, the noise plays a much smaller role. This can be seen by noting that for the models in Equations 4.3 and 4.4, $\sigma_X^2/\sigma_N^2 = 201$, so realizations from these