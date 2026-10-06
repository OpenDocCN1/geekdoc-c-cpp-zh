# 4.5 Quasistochastic Approximation

```
$$\lambda_t = \lambda_0 + \int_0^t g(\partial_r)dr + \gamma_t,\quad (4.38)$
```

where $\lambda_0 \ge 0$ is the initial condition. The reflection process is defined by three constraints
(for each $1 \le i \le m$):

+   (1) $\gamma_0(i) = 0$.
(2) $\gamma(i)$ is nondecreasing, and the solution to (4.38) is nonnegative $(\lambda_t(i)$ is nonfor
each $i$ and $t$.
(3) It is the minimal function of time satisfying 1 and 2. This is equivalently expressed

```
$$\int_0^T \lambda_t(i)d\gamma_t = 0,\quad \text{for all } T > 0.\quad (4.39)$
```

The integral (4.39) is defined in the sense of Riemann and Stieltjes, and by combining
(1)-(3), we see that

```
$$\lambda_t(i) > 0 \implies \frac{d}{dt}\gamma_t(i) = 0.$
```

Proposition 4.11 extends easily to this primal-dual flow, and the proof is almost identical.
The property (4.39) allows us to disregard the reflection process in a crucial part of the
apunov function analysis found in Section 4.8.3.

**Proposition 4.13** Suppose that $\Gamma$ is strictly convex and coercive, and $g$ is convex,
and that $\partial\theta g(\theta^*)$ has rank $m$. Then the primal-dual flow converges to the unique solution
(\theta^*, \lambda^*)$ of the dual:

```
$$\mathcal{L}(\theta^*, \lambda^*) = \varphi^*(\lambda^*) = \Gamma.*.$
```

# Euler Approximation

A remaining question is how to translate the primal-dual flow with reflection into a discrete-
time, as (4.38) is not an ODE. A standard primal-dual algorithm is
defined by the pair of equations:

```
$$\theta_{n+1} = \theta_n - \alpha_{n+1}[\nabla\partial g(\theta_n)]^T\lambda_n],\quad (4.40a)\n$\lambda_{n+1} = [\lambda_n + \alpha_{n+1}g(\theta_n)]_+.,\quad (4.40b)$
```

where $[\cdot]$ is the componentwise maximum with zero. Hence (4.40b) can be expressed

```
$$\lambda_{n+1} = \lambda_n + \alpha_{n+1}g(\theta_n) + \Delta_n,\n\Delta_n^+ = [\lambda_n + \alpha_{n+1}g(\theta_n)]_+ - [\lambda_n + \alpha_{n+1}g(\theta_n)]_- \ge 0$
```

so that $\Delta_n^+$ may be interpreted as an increment of a reflection process.

# 4.5 Quasistochastic Approximation

We are interested in solving a root-finding problem of a special form, which requires an
adjustment of notation. Given a function $f: \mathbb{R}^d \times \Omega \to \mathbb{R}^d$, and a random vector $\Phi$ taking