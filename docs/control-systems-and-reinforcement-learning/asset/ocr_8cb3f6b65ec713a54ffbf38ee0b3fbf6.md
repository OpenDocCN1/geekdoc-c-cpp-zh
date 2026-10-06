# ODE Methods for Algorithm Design

Increasing $e^{L_f w}$ to $e^{L_f T}$ for the range of integration gives

```
$2 \int_0^T ||\dot{	heta}_w - \dot{	heta}_\tau|| dw \leq 2(B_f + L_f ||\dot{	heta}_\tau||)e^{L_f T} \int_0^T w dw = \langle B_f + L_f ||\dot{	heta}_\tau||\rangle T^2 e^{L_f T}$.
```

Hence

```
$$\hat{\alpha}_T^2 \leq b_0(\dot{	heta}_0)\varepsilon_0^2 + L_f(B_f + L_f ||\dot{	heta}_\tau||)T^2 e^{L_f T},
```

which completes the proof, since $0 \leq T \leq 1$ by assumption.

# 4.9.3 Criteria for Stability

The first step in establishing convergence of QSA is to show that the solutions are bounded in time. Two approaches can be borrowed from the dynamical systems literature: Lyapunov function techniques, or the ODE at $\infty$ introduced in Section 4.8.4.

# Lyapunov Criterion and (QSV1)

There exists a continuous function $V: \mathbb{R}^d \to \mathbb{R}_+$ and constants $c_0 > 0, \delta_0 > 0$ such that, for any initial condition $\theta_0$ of (4.42), and any $0 \leq T \leq 1$, the following bounds hold when $||\theta_s|| > c_0:

```
$V(\	heta_s + T) - V(\	heta_s) \leq -\delta_0 \int_0^T ||\dot{	heta}_t|| dt.$
```

The Lyapunov function is Lipschitz: There exists a constant $L_V < \infty$ such that $||V(\theta') - V(\theta)|| \leq L_V ||\theta' - \theta||$ for all $\theta, \theta'$.\n

Assumption (QSV1) ensures that $V(\theta_t)$ is strictly decreasing when $\theta_t$ escapes a ball of radius $c_0$. If $V$ is quadratic, then this assumption implies

```
$$\frac{d}{dt}V(\	heta_t) \leq -\delta_0||\dot{	heta}_t||, \quad \text{whenever} ||\dot{	heta}_t|| > c_0.$
```

The integral form is chosen since sometimes it is easier to establish a bound in this form. In particular, the proof of Proposition 4.34 is based on the construction of a solution to (QSV1).

# Verifying (QSV1) for a Linear System

Consider the ODE (4.42), in which $f(x) = Ax$ with $A$ a Hurwitz $d \times d$ matrix. There is a quadratic function $V_2(x) = x^T Mx$ with $M \in \mathbb{R}^{d \times d}$ satisfying the Lyapunov equation $MA + A^T M = -I, M > 0$. Consequently, solutions to (4.42) satisfy

```
$$\frac{d}{dt}V_2(\	heta_t) = -||\dot{	heta}_t||^2.$
```

Choose $V = \sqrt{V_2}$, also by this chain rule

```
$$\frac{d}{dt}V(\	heta_t) = -\frac{1}{2}\frac{1}{\sqrt{V_2(\theta_t)}}||\dot{	heta}_t||^2 \leq -\frac{1}{2}\sqrt{\lambda_{max}}}||\dot{	heta}_t||,$
```

where $\lambda_{max}$ is the largest eigenvalue of $M$. This $V$ is a Lipschitz function to (QSV1), for any $c_0 > 0$.