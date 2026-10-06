254

Stochastic Control

The cost function we consider balances delay with power consumption:

$c(x, u) = x + rP(u),

where $\mathcal{P}$ denotes the power consumption as a function of the service rate $u$, and $r > 0$. We are then to the AOE to obtain an optimal policy,

```
$h^*(x) + \eta^* = \min_{u \in U(x)} \{c(x, u) + P_u h^*(x)\}$
= \min_{u \in U(x)} \{x + rP(u) + E[h^*(x - u + A(k))]\}\quad (7.33)$
```

Here we will use quadratic for $u$, which is alleged to be a good approximation for computer processors.

# 7.4.1 Fluid Model

We cannot possibly solve the ACOE for the stochastic model (7.33) or even obtain any intuition in this discrete-st world. we find that optimization of the fluid model in continuous time provides a near-perfect approximation of the ACOE solution. We henceforth abandon없이 integer constraints, and focus on the scalar state space model

```
$\frac{d}{dt}x_t = -u_t + \alpha,\quad (7.34)$
```

where $\alpha$ is the expectation of $A(k)$, and the processing cost function $c : \mathcal{R}_+ \times \mathcal{R}_+ \to \mathcal{R}_+$, the associated value function is denoted

```
$J^*(x) = \inf \int_0^\infty c(x_t, u_t)dt,\quad x_0 = x \in \mathcal{R}_+$.
```

The HJB equation is then

```
$0 = \min_{u \in U(x)} \{c(x, u) + (-u + \alpha)\frac{d}{ds}J^*(x)\},\quad (7.35)$
```

This is similar to the integrator model with polynomial cost consideration in Section 3.9.44 (see (3.62)).

# 7.4.2 Computation and Solidarity

Consider the following choices for $\mathcal{P}(u)$ in the definition of $J^*$:

Case 1: $\mathcal{P}(u) = u^2$.

In this case, $c(x,u)$ never vanishes, so that the total $J^*(x)$ is never valued! This challenge is resolved by instead considering the (weighted) shortest path problem (SPP):

```
$K^*(x) = \min \int_0^{T_0} c(x_t, u_t)dt,\quad (7.36)$
```

where $x_0 = x \in \mathcal{R}_+, T_0 \overset{def}{=}\{t : x_t = 0\}$ is the first time that $x_t$ hits the origin, and the minimum is over $u$ as follows. The function $K^*$ is finite valued and solves the HJB equation (7.35).