# 286
Stochastic Approximation

Applying (i), we conclude that for some integer $n(\delta)$ and all $n \geq n(\delta)$,

```
$$\|\Theta_{\mathcal{N}_{n+1}}^{(n+1)}} - \theta^*\| \leq |\Theta_{\mathcal{N}_{n+1}}^{(nn)}\| + |\Theta_{\mathcal{N}_{n+1}}^{(nn)}} - \theta^*\| \leq \varepsilon.$
```

By definition, $\theta_{\mathcal{N}_{n+1}} = \Theta_{\mathcal{N}_{n+1}}$ is the initialization for the next interval, which implies that

```
$$\|\theta^{(k)} - \theta^*\| \leq \delta \quad \text{for all } k \geq n(\delta), \tau \geq \mathcal{N}_k.$
```

From (8.19), we then obtain

```
$$\lim_{n\to\infty} |\theta_n - \theta^*\| = \lim_{t\to\infty} |\Theta_t - \theta^*\| \leq \delta.$
```

This establishes convergence, since $\delta > 0$ is arbitrary.

# Projection and Restart

The introduction of $n_0 \geq 0$ in the step-size sequence $\alpha_n = q/(n+n_0)^p$ is to avoid excessive gain when $n$ is small. Anyone who has experienced SA has seen parameter estimates explode in the first few iterations. Without understanding its asymptotic covariance, it is likely that a user will reduce the value of $g_n$, not realizing this might result in asymptotic covariance. Increasing $n_0$ can take the algorithm and has no impact on the asymptotic covariance.

Two alternatives are available, each based on a closed region $R \subset \mathbb{R}^d$ satisfying $\theta^* \in R$ (in practice, the choice of this set is much like the choice of $n_0$) through trial and error.)

# Projection

The definition requires notion of distance: $dist(w,v) \geq 0$ for any $v \in \mathbb{R}^d$ with $dist(v,v)=0$ for any $v$. It is typical to use the standard Euclidean norm or the max norm: $dist(w,v) = \|w-v\|_{\infty} = \max |\w_i - v_i\|$. For any vector $v \in \mathbb{R}^m$, the vector $\theta' = \Pi_R\v\}$ satisfies

```
$$\theta' = \arg\min dist(w,v) : w \in R.$
```

Projected aligned the basic algorithm (8.2) is defined by the following:

```
$$\theta_{n+1} = \Pi_R(\theta_n + \alpha_n f_n(\theta_n)).\quad (8.20)$
```

There are two difficulties with this approach: one is the potential computational complexity in updating the parameter estimate, and the other is complexity in an ODE analysis. How do we know that the parameter sequence doesn't become trapped on the boundary of $R?

# Restart

Whenever $\theta_{n+1} \notin R$, we reset its value to a vector within the interior of $R$. For example, with $R = \{\theta : |\theta\| \leq r\}$, you might choose the reset parameter to be $\theta'_{n+1} \in R$ by scaling the following:

```
$$\theta'_{n+1} = \frac{r}{2\|theta_{n+1}\|}\theta_{n+1}.$
```

This procedure is far simpler than projection, and analysis is simpler.