# 8.6 Buyer Beware

Stochastic approximation can be difficult to apply because of exotic nonlinear dynamics. This is often resolved using Zap SA, while PJR averaging might fail. Two other potential curves are described here: condition number, and disturbances with long memory.

# 8.6.1 Curse of Condition Number

The condition number of the linearization matrix A = $\partial f(	heta^*)$ is the ratio of maximal and minimal singular values:

```
$$\kappa(A) = \frac{\sigma_{\max}(A)}{\sigma_{\min}(A)}$ (8.55)
```

where the singular values $\sigma_i(A)$ are obtained by taking the square root of the eigenvalues of AAᵀ. If the condition number is large, then the benefit of Polyak-Ruppert averaging may not be observed until a very long run.
The example and discussion is early warning of what might go wrong in reinforcement learning. The standard Q-learning algorithm of Watkinsにつき has a linearization matrix A with a massive condition number, and examples in Section 9.6 reveal PJR averaging may provide no benefit for time horizons less than 10 million.
The point is illustrated using the line SA recursion

```
$$\theta_{n+1} = \theta_n + n^{-1}[A\theta_n + \Delta_n + 1]$ (8.56)
```

in which $\Delta$ is Gaussian and i.i.d., with marginal N(0,1). The matrix is to be a simple form

$A = -I + (\kappa-1)vv^T$,$
in which $||v|| = \kappa$ and $\kappa > 1$. The matrix $-A$ has one eigenvalue at $\kappa$ (eigenvector), and the remaining eigenvalues are unity. The condition number of $A$ is $\kappa$.
Let's consider two algorithms with optimal asymptotic convergence:

+   (i) Stochastic Newton-aphson:
$$\theta_{n+1}^{\theta} = \theta_n^{\theta} + n^{-1}(A^{\theta_n})^{-1}(\Delta_n + 1)$ (8.57)

+   (ii) PJR estimates with carefully selected step-size. One challenge with a large condition number is that the step-size needs to be reduced to avoid explosion of the parameter estimates. This is required even if there is no noise, so that $\hat{f} = f_n$. This motivates the modification

$$\alpha_n = \min(\alpha_0, n^{-\rho})$ (8.58)

The value $\alpha_0 = 1/\kappa$ was reliable in experiments, with $\rho \in (1/2,1).
Either algorithm achieves the optimal asymptotic variance for each component of the parameter:

```
$$\Sigma_{\theta} = G\Sigma_A G^T = (A^2)(I + rvv^T)^{-1} = I - \frac{r}{1+r}vv^T$,nwith $r = \kappa^2-1$. In particular, each approach reaches the optimal asymptotic variance for
```

```
$$\lim_{n\to\infty} E[\theta_n^{\theta}(i)^2] = \lim_{n\to\infty} E[\theta^*^{\theta}(i)^2] = \Sigma_{	heta^*}(i)$.
```