298

Stochastic Approximation

![](bbox=[0.318, 0.076, 0.683, 0.269])

The value $g=1/4$ may lead to very slow transient performance, even if the mean-square error converges to zero at its optimal rate. This is illustrated in Figure 8.5. Before discussing the figure, we revisit the topic of asymptotic variance.

# 8.4.2 Variance Formulae

What can we expect if we increase the gain in the step-size rule $\alpha_n = g/n$? A variance formula for $g > g^*/2$ follows from (8.28a), and appears similar to the variance formula for Monte Carlo:

$$\sigma_{\Delta}^2 = \left(\frac{g^2}{g/g^*}\right)\sigma_{\Delta}^2$. (8.47)

The value $g=1/0.34$ is 12 times larger than the value $g^*=1/4$ derived using asymptotic theory. The formula (8.47) can be applied to establish that $\sigma_{\Delta}^2$ is increased by more than six fold with the larger gain.

If we instead opt for $\alpha_n = g/n^2$, then (8.6) results in

$$\sigma_{\Delta}^2 = \lim_{n\to\infty} n\mathbb{E}[(\theta_n - g^*)^2]$. (8.48)

The formula is simpler in this case, and is valid for any $g>0$, and any $\rho \in (0.5,1)$

$$\sigma_{\Delta}^2 = gg^*\sigma_{\Delta}^2$. (8.49)

See Section 8.7.2 for details.

# 8.4.3 Simulations

Up until now, we have said nothing about the disturbance $\Phi$, which has zero mean. The plots that follow an i.i.d. Gaussian process with $\Phi_n \sim N(0,1)$. For i.i.d. disturbance, the variance term appearing on the right-hand side of (8.47) is defined by

$$\sigma_{\Delta}^2 = \mathbb{E}[(f'(\theta^*),\Phi_n)^2] = \mathbb{E}[{10\cos(\theta^*))\Phi_n]^2] = 100$.

With step-size $\alpha_n = g/n$, the formula (8.47) gives

$$\sigma_{\Delta}^2 = (5/2)^2,\quad g=g^*=1/4,\n\left(\frac{g^2}{4g-g}\right)^2\sigma_{\Delta}^2 \approx 6\times(5/2)^2,\quad g=1/0.34$.