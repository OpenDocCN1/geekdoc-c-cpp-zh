# 5.7 Duality

We arrive at a generalization of (5.66) to choose $	heta^*$:

# Convex Q-Learning

Choose a pmf $\mu$ on $X 	imes U$, a finite horizon $[T_0, T]$, a convex regularizer $\mathcal{R}(	heta)$, tolerance Tol $\ge 0$, and solve

```
$$\theta^* = \arg \min_{\theta} -\langle\mu, H^theta\rangle + \mathcal{R}(	heta) \quad (5.78a)$
```

```
$$\text{s.t.} \quad \int_{T_0}^T \{D_t(\theta)\} - dt \le \text{Tol.} \quad (5.78b)$
```

Consider next batch setting based on independent trials (as in the mountain car, in which we reach the goal at time $T_n$, and then reinitialize to a state $x_{T_n}$). For simplicity, we simply state a translation of DQN, in which one appearance of the parameter is fixed at value $\theta_n$. Define the following for $t \ge T_n$:

```
$$\mathcal{D}'_t(\theta) = H^{	heta_n}(x_t) - e^{-\alpha(t-T_n)}H^{	heta_n}(x_{T_n}) - \sigma \int_{T_n}^t e^{-\alpha(t-\tau)}[H^{	heta_n}(x_r,u_r)-c(x_r,u_r)]d\tau. \quad (5.79)$
```

This is used to obtain a loss function $\Gamma_n^c$ analogous to (5.58b).

# DQN

With $\theta_0 \in \mathbb{R}^d$ given, along with a sequence of positive scalars $\{\alpha_n\}$, define the following recursively:

```
$$\theta_{n+1} = \arg \min_{\theta} \{\Gamma_n^c(\theta) + \frac{1}{\alpha_n+1}\|\theta - \theta_n\|^2\} \quad (5.80a)$
```

where each $n$,

```
$$\Gamma_n^c(\theta) = \frac{1}{2}\int_{T_n}^{T_{n+1}}[D_t(\theta)]^2 dt, \quad \text{with } r_n = T_{n+1}-T_n. \quad (5.80b)$
```

These algorithms are especially practical for a linear parametrization $H^theta = \theta^T\psi$, since, for example, $\mathcal{H}_t^c = \theta^T\psi_t$, where $\Psi_t$ is obtained by filtering:

```
$$\Psi_t \triangleq \frac{\alpha}{t}\int_0^t e^{-\alpha(t-\tau)}\psi(x_\tau,u_tau)d\tau$
```

# 5.7 Duality*

The ideas introduced here are based on an entirely different view of basic dynamic programming from Section 3.1. The main conclusion is an interesting dual for the DPLP (3.36).