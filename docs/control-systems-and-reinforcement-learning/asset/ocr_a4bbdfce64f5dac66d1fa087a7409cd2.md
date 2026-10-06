# 6.8 Sensitivity and Actor-Only Methods

+   There is a solution $h_	heta$ to Poisson's equation:

```
$$c_0 + P_	heta h_	heta = h_	heta + \eta_	heta. \quad (6.50)$
```

+   The average cost $\eta_	heta$ and other functions of $	heta$ are continuously differentiable in $	heta$.

The assumption that $\eta_	heta$ and $h_	heta$ are continuously differentiable functions of $	heta$ is not strong. See Example 6.21 for hints how to obtain a representation of the gradient of $h_	heta$, subject to mild assumptions on the parameterized model. The "Notes" section contains references with full details.

The control objective is to minimize the loss function $\Gamma(\theta) = \eta_	heta$ over all $\theta \in \mathbb{R}^d$ and, in Section 4, our approach is to approximate by gradient descent: $\frac{d\Gamma}{d\theta}_t = -\Gamma'(\theta_t)$.

A formula from the 1960s provides one example for approximating the gradient, based on the so-called *score function*, for a finite state space model:

```
$$S^	heta(x,x') = \nabla_x \log(P_	heta(x,x')), \quad x,x' \in X. \quad (6.51)$
```

Lemma 6.7 is merely a restriction of that, using the chain rule for the gradient of a logarithm:

**Lemma 6.7** *For a finite state Markov chain, and any function $g: X \to \mathbb{R}$,*

```
$$\nabla_theta{\sum_x P_	heta(x,x')g(x')} = \sum_x P_	heta(x,x')S^	heta(x,x')g(x'). \quad \square$$
```

The proof of the following is at the end of this section.

**Theorem 6.8 (Sensitivity Theorem)** *Suppose that the assumptions of this section hold, and in addition $X$ is finite, $c_	heta(x)$ is continuously differentiable in $\theta$ for each, and the score function is continuous at all value of $\theta$ for $P_	heta(x,x') > 0$. Then,*

```
$$\Gamma(\theta) = E_{\pi_	heta}[c_	heta(X(k)) + S^	heta(X(k), X(k+1))h_	heta(X(k+1))], \quad (6.52)$
```

where the expectation is in state under.

The stochastic approximation of Section 8 invites the *stochastic gradient descent (SGD) algorithm*:

```
$$\theta_{n+1} = \theta_n - \alpha_{n+1}\hat{\Gamma}(X(n)), \quad (6.53)$$\n$$\hat{\Gamma}(n+1) = [\nabla_theta\Gamma(X(n)) + S^	heta(X(n), X(n+1))h_	heta(X(n+1))]|_{\theta=\theta_n$
```

where (in *early chapters*) is a step-size approach. It is likely that we have designed $P_	heta$ and $c_	heta$, so the score function is available. A challenge with this algorithm is the computational complexity of computing $h_{	heta_n}$, at each iteration $n$.

The update equation for $	heta$ is an example of the *actor* in the RL literature, and the relative value function $h_{	heta_n}$ is the critic at iteration $n$. The actor-critic methods surveyed in Section 10 provide a computationally feasible refinement of (6.53), in which the relative value function is estimated simultaneously with estimation of the parameter $	heta^*$ that minimizes $\Gamma$.