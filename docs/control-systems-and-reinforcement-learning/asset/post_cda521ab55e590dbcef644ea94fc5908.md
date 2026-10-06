
80
Optimal Control

## 3.7 Comparing LQR in Continuous and Discrete Time
revisit Exercise 3.1, but in its original continuous setting:

```
$$\frac{d}{dt} = Ax + Bu, \quad A = \begin{bmatrix} -0.2 & 1 \\ -1 & -0.2 \end{bmatrix}, \quad B = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$$
```

Compute the function and the policy $c(x,u) = x^2 + u^2$. How does the policy compare with what was obtained in Exercise 3.1? Are the value functions related (approximately) in any way?

## 3.8 Consider the variant of 3.63 in continuous:

```
$$\frac{d}{dt} = f(x,u) = -u, \quad c(x,u) = x^p + Ru^q. \quad (3.64)$$
```

Estimate the Bellman equation:

```
$B(x) = \min_{u \ge 0} [c(x,u) + \nabla J(x) \cdot f(x,u)],$$
```

where $J(x) = Sx^*$, with $S > 0$ and $s > 1$. What are values of $s,S$ you recommend? For an answer for arbitrary $p,q,R$.

## 3.9 Optimization of the Rowing Game. We now return to Exercise 2.8, and design $(P_k, K_l, K_v)$ in (2.69) using LQR. Rather than consider the 3N-dimensional system, we pretend that the signal $\tilde{z}$ defined in (2.67) is it exogenously rather than a function of the system.

- (a) Obtain a state space model under this idealization, with augmented state $x^{ai}=(z^i, v^i, z'^i)$, and $\tilde{z}$ treated as an exogenous input:

```
$$\frac{d}{dt}x^{ai} = A^{ai}x^{ai} + B^i u^i + E^i\tilde{z} \quad A^{ai} \in \mathbb{R}^{3\times 3} \quad B^i, E^i \in \mathbb{R}^3.$$
```

For this to approximate the actual dynamics, the constant $\tilde{z}$ will depend upon the function gains that contain $u^i$.

- (b) Obtain $(K_p^*, K_l^*, K_v^*)$ using LQR based on $(A^i, B^i)$ and with quadratic cost

```
$c^i(x^a, u) = c_0^i(x^a) + Ru^{i,2}, \quad c_0^i(z^i, z'^i, v^i) = [z^i - z'^i]^2 + S_v[v^i - v^m]^2$
```

in which $S_v > 0$. Note you may calculate the gains using $v^m=0$, but by policy nonzero values:

```
$u^i = -K_p^*(z^i - \tilde{z}) - K_l^*z'^i - K_v^*(v^i - v^m). \quad (3.65)$
```

- (c) We now stop pretending: Analyze the closed-loop system in which each solver uses (3.65), with $\tilde{z} = \bar{z}$ the average position. The $N$-dimensional vector input (with component $r$)

```
$u = -K^*x + K^0\tilde{z} \quad$ with $K, K^0 \in \mathbb{R}^{3N}$.
```

Compute the value function: $J^* = \mathbb{R}^{3N} \to \mathbb{R}$ associated with your policy, and compare it to $J^*$ using full state feedback (both value functions are defined with $c(x,u) = \sum_i c^i(x^{ai}, u^i)$ Note that each value function is a quadratic function of the 3N-dimensional state, so your comparison is in terms of the respective matrices. One should be larger than the other. What is the “loss” from using limited information? You might consider

```
$Loss = \frac{1}{trace(M^*)}trace(M - M^*)$
```

with $J(x) = x^T Mx$ when $v^{rd} = 0$.

Or, propose your own definition of loss and provide justification. (d) for several values of $N$, and in each case observe the eigenvalues in closed loop for your three-dimensional model. Compare these eigenvalues for the true closed-loop system, which takes the form

```
$$\frac{d}{dt}x = (A - BK)x + Ev^{rd}, \quad B,E \in \mathbb{R}^{3N}$$
```

and $A,B$ obtained from part (a). The theory of mean-field games predicts stability and approximate optimality of (3.65) when $N$ is large [81]. Note: If $(A - BK)$ has eigenvalues in the right half plane, you may need to reconsider your choice of $R$ or $S_c$.

## 3.10 Exercises

## 3.10 Energy Control for the Inverted Pendulum [14] Return to the control system described in Exercise 2.17. We have completed parts (a) and (b), solve the following. Unnormalized kinetic and potential energy are of the state:

```
$KE(x) = \frac{1}{2}(\dot{\theta})^2, \quad PE(x) = \cos(\theta) - 1$,
```

where the potential energy is relative to $\theta = 0$, which is maximal. In the seminal part of Aström and Furuta, the control-Lyapunov function approach is using total energy:

```
$E(x) = KE(x) + s_pPE(x),$
```

with $s_p > 0$. You can look at the paper, but I suggest you discover for yourself what value will result in a stabilizing feedback law. The goal is to steer some target value $E_0$. We will take $E_0 = 0$, which corresponds to the upright position (as in the paper, we do not include friction in the model). You may pretend that $g = 1$ in your simulations.

(c) To obtain a control law $\phi(x)$ and and cost as (with $R > 0$):

```
$J(x) = \frac{1}{2}[E(x) - E_0]^2 = \frac{1}{2}x_2^2 + s_p(\cos(\theta) - 1)^2. \quad (3.66)$
```

Define a feedback law $\phi(x)$ and cost $c(x,u)$ that solves the HJB

$$\phi(x) = \arg\min_{u} \frac{1}{2}Ru^2 + f(x,u) \cdot \nabla J(x), c(x,u) = \frac{1}{2}Ru^2$$

Verify that $J$ solves the HJB equation with this $c$, and choose for $J$ in (3.66) that $c$ is non-negative, $J(x) > 0$ over $x_1 \neq \pm\pi/2$, and $E(x) \neq 0$. (d) Try out your control law. Obtain plots as a function of time (including input trajectories, and $E(t)$). Include these scenarios:

- An initial condition $x_0$ satisfying $J(x_0) = 0$ but $E(x_0)$.
- The initial condition $x_0 = (\pi, 0)$, with two or more values of $R$. In the case of large $R$, does the pendulum demand many swings to reach its target?

82 Optimal Control

## 3.11 In Exercise 3.10, you learned how to control a pendulum $E(t) \to 0$ as $t \to \infty$. You likely saw the pendulum swing around, periodically reaching $x_t \sim 0$, and then flying away from this desired position. In this exercise, you will attempt to catch the pendulum and more carefully steer it to the upright position. We consider normalized dynamics:

$0 = -\sin(\theta)+u, \quad \text{that is}, mg=\ell.$

(a) For $x=(\theta,\theta)^\top$ a Taylor expansion gives $0 \approx -\theta+u.$ Based on this linear approximation, obtain a linear state model, and from this feedback loop $u=-K^*x$ based on LQR obtain a good design.

(b) Given a threshold $\tau_E=0$, consider the following policy:

```
$u_t=\begin{cases}-K^*x_t & |x_t|\le \tau_E \\ \phi^E(x_t) & \text{else}\end{cases}$
```

where $\phi^E$ is the policy obtained in the previous assignment. Global asymptotic stability may require a weighted norm, such as $\|x\|=J^*(x)=x^\top Mx$, where $M^*$ solves the ARE (continuous time version). Conjecture under this policy succeeds in a closed-loop system that is globally stable on the restricted state space $x=\{x\in \mathbb{R}^2 : -2<E(x)<1\}$ (this includes all of the state $x=\{0,0\}$ with $|\theta|\le \pi$). (c) Simulate! Obtain a successful design, and discuss results. The definition of $u$ might not make sense unless you convert to physical units. In Matlab, use **theta = wrapTo(theta)** (so that $|\theta|\le \pi$).

## 3.12 Obtain an adaptation of Exercise 3.10 for the mountain car, which requires the following modifications:

- (i) The state space (2.56), where kinetic and potential energy are
- (ii) $E(x)=KE(x)+PE(x)$
$KE(x)=\frac{1}{2}mv^2 \quad PE(x)=U(z)-\alpha u^2, \quad x=(z,v) \in X, \quad (3.67)$

with $U$ defined in (2.57), and based on $\frac{1}{2}E(x)$, then propose a control law (perhaps based on a control-Lyapunov function) that will drive $E(x)$ to zero. For examples, use the numerical values given in Section 2.7.2.

## 3.13 Obtain an energy-based policy (with an adaptation of Exercise 3.10) for MagBall, based on the description in Section 2.7.3. Some ideas to use: The kinetic energy as a function of state is $\frac{1}{2}mv^2$, with $v=x_2$. We introduce potential energy, using the arguments to justify which tools to use in Figure 2.11. The right-hand side of (2.60b) was obtained from Newton's law, with force

```
$F(y,u)=mg-\kappa(y)^2.$
```

```
$\mathcal{U}(y)=-\int_r^r F(y,u^2)dz.$
```

This function is strictly concave, with maximum at $y=r$, where evidently $\mathcal{U}(r)=0$. The total energy is then defined by

```
$E(x) = \frac{1}{2}mx^2 + \mathcal{U}(x_1).
```

It is easily established that $\nabla E(x) = (-F(x_1, u^\circ), mx_2)^\top$.
