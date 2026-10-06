# Control Crash Course

+   (a) Obtain a linearized state model with equilibrium $(x^s, u^s)$ for each equilibrium (you will find that $x_i^s = 0$ is required). Comment on the challenge for $x_i^s = \pm t/2$.
(b) Obtain a linear feedback law that results in $x = 0$ asymptotically stable (locally). You will obtain a control solution that is globally asymptotically stable in Exercise 3.10 after you learn a few concepts from optimal control in the next chapter.
(c) Find $u^0$ such that $x^0 = (r,0)^T$ is an equilibrium: $f(x^0, u^0) = 0$. Based on the linearization (2.62), find a linear control law for (2.62), of the form

$	ilde{u} = -	ilde{K}	ilde{x} = K_1	ilde{x}_1 - K_2	ilde{x}_2$
(b) With this difficulty is that $u^d$ depends on $c/m$, which may not be known. Modify your design as follows:

$\hat{u} = -K^a	ilde{x}^a, \quad \text{where} \quad 	ilde{x}^a = (	ilde{x}_1^a, 	ilde{x}_2^a)^T, \quad z_l^a = \int_{0}^{t} \tilde{x}_1 \ dr$ \quad (2.73)

with $K = [K_1, K_2, K_3]$. This is known as proportional-integral-derivative (PID) control. Obtain a third-order linear state model, and $K_i > 0$ for the $3 	imes 3$ matrix remains Hurwitz, and the transient behavior remains "good" (or define what that means). Observe the equilibrium condition $\frac{d}{dt}x^a=0$ implies that $x_1^a = r$.
(c) Simulate in Exercise 2.16 to estimate the region of attraction (which may restrict the simulation to initial conditions with zero velocity).

2.18 Feedback Linearization for MagBall. For systems with some nonlinearities, there is a "brute-force" approach to obtain a linear model. For MagBall, you may view $v = u^2/x_1$ as an input, from which we obtain a linear system by (2.60):

```
$\frac{d}{dt}x=x2,\frac{d}{dt}v=g-\frac{\kappa}{m}$
```

+   (a) As in the previous exercise, obtain a control law $u = -K\tilde{x}$, where $K_1$ and $K_2$ are parameters chosen for stability and robust response.
(b) Obtain an expression for the equilibrium $x^s$ for the closed-loop system using the gain $\frac{d}{dt}x_i=0$ for $i=1,2$.
(c) Modify your design in (2.73): $v = -K^a\tilde{x}$. Find $K_3 > 0$ so that the transient behavior remains "good".
(d) You will need to modify your policy in (c) so that $v$ is nonnegative, say $v = \Phi(\tilde{x}^a) = \max(0, K_0\tilde{x}^a + K_3\tilde{x}^a)$. The current applied to the magnet is this

```
$u = x_1\sqrt{\Phi(\tilde{x}^a)}.$ \quad$ (2.74)
```

Simulate, and estimate the region of attraction. You may restrict the simulation to zero initial velocity.
How the region of attraction change when $k$ is divided by 2? Do not change your policy! The point is to check if your solution is robust to an inaccurate model.
Warning: Recall that it is not possible to achieve convergence from any initial condition.
Note: See [199] for a survey on feedback linearization - a topic that has far more depth than obvious from this example.