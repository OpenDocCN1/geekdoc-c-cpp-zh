# 290 Stochastic Approximation

eigenvalue of $GA$ satisfies Real$(\hat{\lambda}(GA)) < -\frac{1}{2}$. The covariance matrix is the solution to the Lyapunov equation:

```
$$(GA + I)\Sigma_0^G + \Sigma_0^G(GA + I)^top + G\Sigma_\Delta G^top = 0. \quad (8.29)$
```

The superscript $G$ is introduced here so we can identify the optimal choice:

**Optimizing the Asymptotic Convergence** The Lyapunov equation (8.29) has a solution $\Sigma_0^G \geq 0$ provided the eigenvalue test is satisfied: Real$(\lambda) < -\frac{1}{2}$ for each eigenvalue $\lambda$ of $GA$. The choice $G^* = -A^{-1}$ passes this test, and results in

```
$$\Sigma_0^G A^{-1}\Sigma_\Delta(A^{-1})^top. \quad (8.30)$
```

This is optimal, in the sense that the difference $\Sigma_0^G - \Sigma_0^*$ is positive semidefinite.

See Proposition 8.10 for a special case, and the "Notes" section for resources. RL literature today has an entirely different emphasis: computation of a finite-time error bound of the form

```
$P{\||\theta_n - \theta^*|| > \varepsilon\} \leq \exp(-nI(\varepsilon)), \quad n \geq 1, \quad (8.31)$
```

where $\bar{b}$ is a constant, and $I(\varepsilon) > 0$ for $\varepsilon > 0$. The bound is usually inverted: For given $\delta > 0$, denote

```
$$\pi(\varepsilon, \delta) = \frac{1}{I(\varepsilon)}[\log(\delta) + \log(\delta^{-1})]. \quad (8.32)$
```

(8.31) implies the sample complexity bound: $P{\||\theta_n - \theta^*|| > \varepsilon\}$ for all $n \geq \pi(\varepsilon, \delta)$.

The value of a finite-$n$ bound is invaluable: has assurance that the probability of error is below the desired value, provided we wait for $n \geq \pi(\varepsilon, \delta)$ iterations of the algorithm. There are also significant challenges:

+   (1) A complex bound is typically conservative. If the bound is very loose, then we will not be willing to wait for $n$ to exceed the overestimate $\tilde{n}$.
(2) The $\tilde{n}$ may not offer guidance on how to improve the algorithm.

Counterparts for the parameter estimate convergence are not a challenge:

There is a third criticism concerning any bound on the error metric $||\theta_n||$ (based on (8.31) or a bound on the error variance): it is probably not what we care about! In the context of reinforcement learning, most valuable metric would be a measure of the performance of the policies associated with the parameter estimates, in the theory of bandits surveyed in