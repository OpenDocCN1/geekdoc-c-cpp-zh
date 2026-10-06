# 3.10 Exercises

be larger than the other. What is the “loss” from using limited information? You might consider

```
$Loss = \frac{1}{trace(M^*)}trace(M - M^*)$
```

with $J(x) = x^T Mx$ when $v^{rd} = 0$.

Or, propose your own definition of loss and provide justification. (d) for several values of $N$, and in each case observe the eigenvalues in closed loop for your three-dimensional model. Compare these eigenvalues for the true closed-loop system, which takes the form

```
$$\frac{d}{dt}x = (A - BK)x + Ev^{rd}, \quad B,E \in \mathbb{R}^{3N}$
```

and $A,B$ obtained from part (a). The theory of mean-field games predicts stability and approximate optimality of (3.65) when $N$ is large [81]. Note: If $(A - BK)$ has eigenvalues in the right half plane, you may need to reconsider your choice of $R$ or $S_c$.

# 3.10 Energy Control for the Inverted Pendulum [14] Return to the control system described in Exercise 2.17. We have completed parts (a) and (b), solve the following. Unnormalized kinetic and potential energy are of the state:

```
$KE(x) = \frac{1}{2}(\dot{	heta})^2, \quad PE(x) = \cos(\theta) - 1$,
```

where the potential energy is relative to $	heta = 0$, which is maximal. In the seminal part of Aström and Furuta, the control-Lyapunov function approach is using total energy:

```
$E(x) = KE(x) + s_pPE(x),$
```

with $s_p > 0$. You can look at the paper, but I suggest you discover for yourself what value will result in a stabilizing feedback law. The goal is to steer some target value $E_0$. We will take $E_0 = 0$, which corresponds to the upright position (as in the paper, we do not include friction in the model). You may pretend that $g = 1$ in your simulations.

(c) To obtain a control law $\phi(x)$ and and cost as (with $R > 0$):

```
$J(x) = \frac{1}{2}[E(x) - E_0]^2 = \frac{1}{2}x_2^2 + s_p(cos(\theta) - 1)^2. \quad (3.66)$
```

Define a feedback law $\phi(x)$ and cost $c(x,u)$ that solves the HJB

```
$$\phi(x) = \arg\min_{u} \frac{1}{2}Ru^2 + f(x,u) \cdot \nabla J(x),\\
c(x,u) = \frac{1}{2}Ru^2 - \min_{u} \ffrac{1}{2}Ru^2 + f(x,u) \cdot \nabla J(x)$
```

Verify that $J$ solves the HJB equation with this $c$, and choose for $J$ in (3.66) that $c$ is non-negative, $J(x) > 0$ over $x_1 \neq \pm\pi/2$, and $E(x) \neq 0$.

(d) Try out your control law. Obtain plots as a function of time (including input trajectories, and $E(x_t)$). Include these scenarios:

+   - An initial condition $x_0$ satisfying $J(x_0) = 0$ but $x_0 
eq 0$.
- The initial condition $x_0 = (\pi, 0)^T$, with two or more values of $R$. In the case of large $R$, does the pendulum demand many swings to reach its target?