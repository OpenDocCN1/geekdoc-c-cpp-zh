# 4.4 Optimization

![](bbox=[0.31, 0.076, 0.69, 0.203])

**Figure 4.1** Gradient flow: $\Gamma(\theta_t)$ is nonincreasing each because each sublevel set $S_{\Gamma}(r_0)$ is absorbing.

This intuition is the starting point toward finding conditions under which the gradient flow is convergent using Lyapunov functions. Two typical choices for a Lyapunov function are

```
$V(\theta)=\frac{1}{2}|\theta-\theta^*|^2\quad\text{or}\quad V(\theta)=\frac{1}{2}|\Gamma(\theta)-\Gamma^*|^2,\(4.21)$
```

where $\theta^*=\min_{\theta}\Gamma(\theta)$. The latter is most natural, based on the intuition obtained from this figure and Figure 2.6.

The Polyak–Łojaziewicz (PL) condition considered in Section 4.4.2 is one minimal criterion for convergence. When we are ready to approximate the gradient flow using an Euler approximation, it is standard to follow the $L$-smooth condition: for $L>0$, and all $\theta_0$,

```
$$\Gamma(\theta) \geq \Gamma(\theta^*)+[\theta-\	heta^*]^T\nabla\Gamma(\theta)+\frac{L}{2}|\theta-\	heta^*|^2.\(4.22)$
```

The usefulness of this bound is explained in Section 4.4.3.

Please not feel free to prove a theorem before you experiment: the algorithms we obtain are frequently successful in practice, even when our assumptions are violated. For example, the optimization problems presented here, in training neural networks do not satisfy any of the assumptions listed, but practitioners commonly apply the gradient descent algorithm described in Section 4.4.3, which is nothing but a Euler approximation of the gradient flow.

# 4.4.1 Role of Convexity

The term has come up in discussion in preceding chapters, but now requires a formal definition:

# Convexity

+   A set $S \subset \mathbb{R}^d$ is convex if it contains, all line segments with endpoints in $S$. That is, $(1-\alpha)\theta^0+\alpha\theta^1 \in S$ for $\theta^0,\theta^1 \in S$ and any $\alpha \in (0,1)$.
- A function $\Gamma: S \to \mathbb{R}$, with convex domain $S$, is called convex if the following bound holds: For any pair $\theta^0,\theta^1 \in S$ and $\rho \in (0,1)$:

```
$$\Gamma((1-\rho)\theta^0+\rho\theta^1) \leq (1-\rho)\Gamma(\theta^0)+\rho\Gamma(\theta^1).\quad(4.23)$
```

It is quasiconvex if the sublevel set $S_{\Gamma}(r)$ is convex (or empty) for any $r \in \mathbb{R}$.