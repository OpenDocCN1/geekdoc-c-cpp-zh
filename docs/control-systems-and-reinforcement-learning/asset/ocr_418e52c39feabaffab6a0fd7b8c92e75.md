# 9.8 GQ and Zup

# 9.8.1 GQ-Learning

This algorithm is defined exactly as in the deterministic setting of Section 5.4.4, with the same objective: solve

```
$$\min \Gamma(\theta) = \min_{\theta} \frac{1}{2} {f^0(\theta)}^T M f^0(\theta),$$
```

where once again $M^{-1} = E_{	heta[\zeta_n \zeta_n^T]$ with $\zeta_n = \psi(n)$ (recall 9.4 for notation). For the tabular case, this reduces to $M^{-1} = \Pi$, and $\Gamma(\theta) = 0$.

The ODE method based on gradient descent will provide a recursive algorithm, as in the deterministic setting considered previously (recall (5.55)). We must first inspect the ODE. The following representations are implied by (9.92b).

+   **Lemma 9.26** $\theta \in \mathbb{R}^d$ satisfies $0 \in \Theta^m$ for any $m$, then $\Gamma$ is quadratic in a neighborhood of $\theta$, with partial derivatives

```
$$\Gamma(\theta) = A(\theta)^T M f^0(\theta) = -[I - \Gamma_m]^T f^0(\theta)$,$\nabla^2(\theta) = [I - \Gamma_m]^T \Pi[I - \Gamma_m].$$
```

GQ-learning is the two-scale SA algorithm, designed to approximate $\frac{d\theta}{dt} = -\Gamma(\theta)$, with $-\Gamma(\theta) = f^0(\theta) - \Gamma_m^T f^0(\theta)$. A challenge is to interpret the product:

```
$T_m^T f^0(\theta)|_i = \sum_j f_j^0(\theta) T_m(j, i), \quad \theta \text{ in } (\Theta^m).$$
```

For the tabular case, this can be expressed

```
$T_m^T f^0(\theta)|_i = \sum_{j,k} f_j^0(\theta) T_m(j,k) \psi_k(x^k, u^k) = \sum_j f_j^0(\theta) E[|\underline{\psi}_{(n+1)}|_i | \Phi(n) = (x^j, u^j)|_i], \quad (9.93)$
```

where $\underline{\psi}_{(n+1)} = \psi(X(n+1)),Phi(X(n+1)) \text{ for } \theta \in (\Theta^m)$.\nThis representation lends itself to algorithm design. Recall from (9.74) that $\phi_n$ denotes the greedy policy associated with $H^n$.

# **GQ-Learning**

For initialization $\theta_0, \omega_0 \in \mathbb{R}^d$

```
$$\theta_{n+1} = \theta_n + \alpha_{n+1}\{\mathcal{D}_n + 1\psi(n) - \gamma\omega_{n+1}^T\underline{\psi}_{(n+1)}\},\ \quad (9.94a)$
```

```
$$\omega_{n+1} = \omega_n + \beta_{n+1}\{\mathcal{D}_n + 1\underline{\psi}_{(n)}^T\omega_n},\ \quad (9.94b)$
```

```
$where $\underline{\psi}_{(n+1)} = \psi(X(n+1)),Phi(X(n+1)),\n\mathcal{D}_{n+1} = -H^n(\Phi(n)) + c_n + \gamma H^n(X(n+1)),$$
```

where the two step-size sequences satisfy (8.22).