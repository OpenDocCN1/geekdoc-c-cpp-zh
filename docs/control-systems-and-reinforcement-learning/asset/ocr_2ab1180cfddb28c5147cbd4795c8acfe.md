# Temporal Difference Methods

# 9.4.2 Nonlinear Parameterizations

Suppose $h^0: 0 \in \mathbb{R}^d$ are not linear functions of $\theta$, but are differentiable. A generalization of the foregoing are based on the definition

```
$$\psi_t(x;\theta) = \frac{\partial}{\partial\theta_s}h^{\theta}(x).$
```

The temporal difference and eligibility sequence are redefined as follows:

```
$$\mathcal{D}_{n+1} = c(X(n)) + \gamma h^{\theta}(X(n+1)) - h^{\theta}(X(n)), \quad (9.43a)\n\zeta_{n+1} = \lambda\zeta_n + \psi(X(n+1);\theta_n), \quad n \geq 0. \quad (9.43b)$
```

The TD($\lambda$) or LSTD($\lambda$) algorithms can be defined using these definitions, because their theory is lacking.

The Zap($\lambda$) algorithm is a potential alternative, which will be convergent under mild conditions. However, it is useful to go back to basics, and ask if there is good motivation for the choice of eligibility vector

If the algorithm is chosen, the limit $	heta^*$ can be solved as follows:

```
$0 = \mathbb{E}[(c(X(n)) + \gamma h^{\theta}(X(n+1)) - h^{\theta}(X(n))\zeta_n^{\theta*}], \quad (9.44)$
```

where $\zeta_n^{\theta*} = \lambda\zeta_n^{\theta*} + \psi(X(n+1);\theta^*), n \geq 0$, and the expectation in (9.44) is taken with respect to the joint stationary process $(X,\zeta^{\theta^*})$. The fixed-point equation $\Phi = \Phi(k) : k \geq 0$ is$ no longer has an interpretation as a Galerkin relation when the eligibility vector depends upon the parameter $\theta$. It may be best to modify the definition of the loss function so that the solution is more easily understood. Examples include convex Q-learning and actor-critic methods.

# 9.5 Return to the Q-Function

In this section and, it is assumed that the input is defined by a (possibly randomized) stationary process $\phi$. For the sake of analysis, it is assumed that $\Phi = \{\Phi(k) = (U(k)) : k \geq 0\\}$ is uni-chain, with unique invariant pmf given by (9.3b).

# 9.5.1 Exploration

It is time to discuss how to define $\Phi$ when our true goal is to estimate a value function for a deterministic policy $\Phi$. It is useful to construct the randomized policy that it can be regarded as an'$\varepsilon$-perturbation' of $\Phi$, where $\varepsilon$ is a small but constant.

One approach is to start with any randomized policy $\phi^{\varepsilon}$. This might be completely random, in the sense that $\phi^{\varepsilon}(u|x)$ does not depend upon $x$. The $\varepsilon$-approximation is then defined as:

```
$$\phi(u|x) = (1 - \varepsilon)\{u = \phi(x)\} + \varepsilon\phi(u|x). \quad (9.45)$
```

This is implemented using an i.i.d. Bernoulli sequence $\{I_k\}$ with parameter $\varepsilon$, so that $P\{I_k=1\} = \varepsilon$. The policy $\phi$ is applied at time $k$ if and only if $I_k=0$; otherwise the input is determined by $\phi^{\varepsilon}$.