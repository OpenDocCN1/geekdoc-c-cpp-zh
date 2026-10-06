# 9.9 Technical Proofs

353

![](bbox=[0.275, 0.073, 0.683, 0.198])

**Figure 9.6** Span norm error for Zap Zero Q-learning.

# ## Zap Zero Q-Learning

Initialize $	heta_0, \omega_0 \in \mathbb{R}^d$, Update for $n \geq 0$:

```
$$\theta_{n+1} = \theta_n + c_n\omega_n,$$
$\omega_{n+1} = \omega_n + \beta_n + \beta_{n+1}\{A_{n+1}\theta_n - b_{n+1}\}$$
```

the following two-step sequences satisfy (8.22).

The fast time-scale recursion (9.9b) is designed to obtain the approximation

```
$$\omega_{n} \approx -A(\theta_n)^{-1}\{A(\theta_n)\theta_n - b\\}$
```

The Zap Zero algorithm is not much better than Watkins's original algorithm. We have doubled the number of parameter elements since we must update $\theta_n$ and $\omega_n$ at each stage, but the updates are not all complex.

When this and Zap Q-learning are compared for the example considered in Figure 9.3 we observe that the span errors for the respective parameter estimates $\{\theta_n\}$ are very similar. Results are shown in Figure 9.6, alongside results using PJR averaging and Watkins's algorithm with gain $g = 1/(1-\gamma)$. The transient behavior of Zap Zero Q-learning is better than what is obtained using averaging, and a bit worse than Zap Q-learning.

For Zap Q-learning, any value $0.6 \leq \rho \leq 0.9$ for $\beta_n = n^{-\rho}$ in (9.96) gives similar performance.

However, for Zap Zero and PJR averaging, was found in this example that a large step-size $\rho$ is required for the time scale. These results were obtained using $\beta_n = n^{-\rho}$ with $\rho = 0.1$. Performance was terrible for Zap Zero and PJR averaging with $\rho \geq 0.5$. New theory is needed to explain these findings.

# ## 9.9 Technical Proofs*

# ### 9.9.1 Advantage Function

Proof of Proposition 9.1 The conclusion $G^*(x) = E[Q(\phi(n)) | X(n) = x] = \sum_{u} \phi(u) | x)Q(x,u) = \underline{Q}(x)$ is obtained upon recalling the definition of the conditional expectation in (9.15). Recall that $\underline{Q} = h$ is the value function (9.6a).