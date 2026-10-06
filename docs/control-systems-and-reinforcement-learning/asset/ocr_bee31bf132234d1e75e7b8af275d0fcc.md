# 82 Optimal Control

3.11 In Exercise 3.10, you learned how to control a pendulum $E(x_t) 	o 0$ as $t 	o \infty$. You likely saw the pendulum swing around, periodically reaching $x_t \sim 0$, and then flying away from this desired position.

In this exercise, you will attempt to catch the pendulum and more carefully steer it to the upright position. We consider the normalized dynamics:

```
$0 = \hat{	heta}-\sin(\hat{	heta})+u\cos(\hat{	heta}), \quad \text{that is}, m=g=\ell \text{(for convenience).}$
```

(a) For $x=(	heta,\theta)^\top$ a Taylor series expansion gives

```
$0 \approx \hat{	heta}-\theta+u.$
```

Based on this linear approximation, obtain a linear state space model, and from this feedback loop $u=-K^*x$ based on LQR with cost $c(x,u)=\|x\|^2+ru^2$ (you may need to experiment with $r$ to obtain a good design).

(b) Given a threshold $	au_E=0$, consider the following policy:

```
$u_t=\begin{cases}-K^*x_t & ||x_t|\le \tau_E \ \phi^E(x_t) & \text{else} \end{cases}$
```

where $\phi^E$ is the policy obtained in the previous assignment. Global asymptotic stability may require a weighted norm, such as

$||x||=J^*(x)=x^\top Mx, \quad$ where $M^*$ solves the ARE (continuous time version).

Conjecture under which this policy succeeds in a closed-loop system that is globally stable on the restricted state space $x=\{x\in \mathbb{R}^2 : -2<E(x)<1\}$ (this includes all of the state $x=\{0,0\\}$ with $|\theta|\le \pi$).

(c) Simulate! Obtain a successful control design, and discuss results.

That the definition of $u$ might not make sense unless you convert to physical units. In Matlab, use **theta = wrapToPI(theta)** (so that $|\theta|\le \pi$).

3.12 Obtain an adaptation of Exercise 3.10 for the mountain car, which requires the following modifications:

+   (i) The state space (2.56), where kinetic and potential energy are

+   (ii) $E(x)=KE(x)+PE(x)$
$KE(x)=\frac{1}{2}mv^2 \quad PE(x)=U(z)-\alpha(u^2), \quad x=(z,v) \in \ X, \quad (3.67)$

with $U$ defined in (2.57), and based on $\frac{1}{2}E(x)$, then propose a control law (perhaps based on a control-Lyapunov function) that will drive $E(x)$ to zero. For examples, use the numerical values given in Section 2.7.2.

3.13 Obtain an energy-based policy (with an adaptation of Exercise 3.10) for MagBall, based on the description in Section 2.7.3.

Some ideas to use: The kinetic energy as a function of state is $\frac{1}{2}mv^2$, with $v=x_2$. We introduce potential energy, using the arguments to justify which tools to use in Figure 2.11. The right-hand side of (2.60b) was obtained from Newton's law, with force

```
$F(y,u)=mg-\kappa(y)^2.$
```

```
$\mathcal{U}(y)=-\int_r^r F(y,u^2)dz.$
```