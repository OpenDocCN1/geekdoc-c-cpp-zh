
Stochastic Control

The cost function we consider balances delay with power consumption:

$c(x, u) = x + rP(u),$

where $\mathcal{P}$ denotes the power consumption as a function of the service rate $u$, and $r > 0$. We are then to the ACOE to obtain an optimal policy,

```
$h^*(x) + \eta^* = \min_{u \in U(x)} \{c(x, u) + P_u h^*(x)\}$
= \min_{u \in U(x)} \{x + rP(u) + E[h^*(x - u + A(k))]\}\quad (7.33)$
```

Here we will use quadratic for $u$, which is alleged to be a good approximation for computer processors.

## 7.4.1 Fluid Model

We cannot possibly solve the ACOE for the stochastic model (7.33) or even obtain any intuition in this discrete-state world. We find that optimization of the fluid model in continuous time provides a near-perfect approximation of the ACOE solution. We henceforth abandon integer constraints, and focus on the scalar state space model

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

This is similar to the integrator model with polynomial cost consideration in Section 3.9.4 (see (3.62)).

## 7.4.2 Computation and Solidarity

Consider the following choices for $\mathcal{P}(u)$ in the definition of $J^*$:

Case 1: $\mathcal{P}(u) = u^2$.

In this case, $c(x,u)$ never vanishes, so that the total $J^*(x)$ is never valued! This challenge is resolved by instead considering the (weighted) shortest path problem (SPP):

```
$K^*(x) = \min \int_0^{T_0} c(x_t, u_t)dt,\quad (7.36)$
```

where $x_0 = x \in \mathcal{R}_+, T_0 \overset{def}{=}\{t : x_t = 0\}$ is the first time that $x_t$ hits the origin, and the minimum is over $u$ as follows. The function $K^*$ is finite valued and solves the HJB equation (7.35).

## 7.4 Speed Scaling

We next obtain bounds on $K^*$ by considering simple policies. For example, if we take $u_t = \mu$ when $x_t > 0$, (7.34) turns into the fluid model for the CRW queue. Assuming that $\mu > \alpha$, this policy is optimal, by solving the following equation:

```
$x_t = x_0 - (\mu - \alpha)t, \quad 0 \le t \le T_0,$
```

where $T_0 = (\mu - \alpha)^{-1}x_0$. Integrating gives us the following:

```
$K(x;\mu) = \int_0^{T_0} (x_t + ru^2) dt = \frac{x^2}{\mu - \alpha} + r\mu^2\frac{x}{\mu - \alpha}, \quad x_0 = x.$
```

This implies that $K^*(x)$ can grow faster than a quadratic. We can obtain a binding bound by improving the control law $u_t = \mu^*(x)$ for $x_t > 0$ with $x_0 = x$, where $\mu^*(x)$ is the minimum of the $K(x; \mu)$ over $\mu > \alpha$. The first-order condition for optimality gives

```
$0 = \frac{d}{d\mu}\left[\frac{x^2}{\mu - \alpha} + r\mu^2\frac{x}{\mu - \alpha}\right]|\mu=\mu^*} = -(x^2 + rx|\mu^*|^2)\frac{1}{(\mu^* - \alpha)^2} + 2r\mu^*\frac{x}{\mu^* - \alpha},
```

where $\mu^* = \mu^*(x)$ in each appearance. A quadratic equation in $\mu$ multiplying both sides by $(\mu^* - \alpha)^2$, can be solved to

```
$\mu^*(x) = \alpha + \sqrt{x^2 + rx/r}, \quad K(x;\mu^*(x)) = \frac{1}{\sqrt{x^2 + rx/r}}(x^2 + rx|\mu^*|^2).
```

We have $K^*(x) \le K(x; \mu^*(x))$, which implies that the growth rate of $K^*$ is no faster than $x^{3/2}$. This bound is tight, as we see by solving the HJB equation (7.35): For $x > 0$,

```
$0 = \min_{u \in U(x)} \{x + \frac{1}{2}u^2 + (-u + \alpha)\frac{d}{dx}K^*(x)\}.\quad (7.37)$
```

This is a first-order ODE with boundary condition $K^*(0) = 0$. Its solution with $r = \frac{1}{2}$ is,

```
$K^*(x) = \alpha + \frac{1}{2}(2x + \alpha)^{3/2} - \alpha.\quad (7.38)$
```

Assuming that $u^* \neq 0$ in (7.37), the first-order optimality conditions give the optimal policy:

```
$0 = \frac{d}{du}(x + \frac{1}{2}u^2 + (-u + \alpha)\frac{d}{dx}K^*(x)).
```

$u^* = \Phi^*(x) = \frac{d}{dx}K^*(x)$ is the policy for $x > 0$, the derivative is nonnegative for all $x$.

Case 2: $P(u) = (u - \alpha)^2$

This modification of the cost function leads to a simpler expression for SPP, which coincides with total cost: $c(x^e, u^e) = 0$, where $x^e = 0$ and $u^e = \alpha$. For simplicity, we maintain $r = \frac{1}{2}$. The HJB equation (7.35) is similar to (7.37):

```
$0 = \min_{u \in U(x)}\x + \frac{1}{2}(u - \alpha)^2 + (-u + \alpha)\frac{d}{dx}J^*(x)\}.\quad (7.39)
```

Assuming $u^* \neq 0$, we apply the first-optimality conditions as before to obtain

```
$0 = \frac{d}{du}(x+\frac{1}{2}(u-\alpha)^2+(-u+\alpha)\frac{d}{dx}J^*(x)) \Rightarrow u^* = \alpha+\frac{d}{dx}J^*(x).
```

The closed-loop dynamics can be expressed as gradient descent:

```
$\frac{d}{dt}x_t = -u^*+\alpha=-\frac{d}{dx}J^*(x_t).
```

Computation of $J^*$ proceeds by solving (7.39), subject to the boundary condition $J^*(0)=0$. Let's guess the solution as $J^*(x)=bx^{p-1}$ for some $p\geq 1$ and $b>0$. We obtain the following:

- (i) The minimizer in HJB equation (7.39) gives the policy for fluid model:

```
$\Phi^*(x)=\alpha+\frac{d}{dx}J^*(x)=\alpha+bx^{p-2}.
```

- (ii) Substitution of $u^*=\Phi^*(x)$ into (7.39) gives the following:

```
$0=(x+\frac{1}{2}(bx^{p-2})^2)=b^2x^{2(p-1)}.
```

This is only possible for $b=\sqrt{2}$ and $p=3/2$ (consistent with (7.38)).

- (iii) For $r>0$, the value function and optimal policy for fluid model given by

```
$J^*(x)=\alpha r^{1/2}x^{3/2}\quad\and\quad\Phi^*(x)=\alpha+\sqrt{r}x.\quad(7.40)
```

Note that $x$ and $|\Phi^*(x)-\alpha|$ are linear in $x$. This reflects the balance between state and control cost.

## 7.4.3 Solidarity

A numerical example illustrates the strong solidarity between the MDP model and its fluid model approximation.

Take $r=1/2$, and choose the marginal distribution of the arrival process to be a scaled geometric distribution:

```
$A(k)=\Delta_A G(k),\quad k\geq 1,\quad(7.41)$
```

where $\Delta_A>0$ and $G$ is geometrically distributed on $\{0,1,\dots\}$ with parameter $p_A$. The mean and variance of $A(k)$ are given by, respectively,

```
$m_A=\Delta_A\frac{p_A}{1-p_A},\quad\sigma_A^2=\frac{p_A}{(1-p_A)^2}\Delta_A^2,\quad(7.42)$
```

with $p_A=0.96$ and $\Delta_A=1/24$ chosen so that the mean $m_A$ is equal to unity:

```
$1=m_A=\Delta_A\frac{p_A}{1-p_A},\quad(7.43)$
```

You can read about the value iteration algorithm (VIA) in Appendix B.2, which is nearly identical to the definition for deterministic control systems in (3.8). In particular, the algorithm generates a sequence of functions $\{V_n\}$, each of which can be interpreted as a value function for a finite horizon optimal control problem:

## 7.5 LQG

![](img/0790f102da4ffa7564329bf76c7d0815_274_0.png)

**Figure 7.2** Convergence of optimal policies for the fluid and MDP points.

![](img/0790f102da4ffa7564329bf76c7d0815_274_1.png)

**Figure 7.3** The convergence of value iteration for quadratic cost function.

```
$V_n(x) = \min_{U} \mathbb{E} \sum_{k=0}^{n-1} c(X(k),U(k)) + V_0(X(n)) \mid X(0) = x]. \quad (7.44)$
```

Shown in Figure 7.2 is a comparison of the optimal policy, computed numerically using value iteration, and the optimal policy for the fluid model. Recall that the constraint $U(k) \le X(k)$ is imposed in the stochastic model. This constraint is imposed in the policy in the figure, so that

```
$\Phi^*(x) = \min(x, \Phi^*(x)).
```

For MDP models, the sequence of differences $\{h_n(x) = V_n(x) - V_n(x^*)\}$ consists of approximations of the relative value function. The convergence of $\{h_n\}$ to $h^*$ is illustrated in Figure 7.3 using $x^* = 0$.

The discrete-time system equations are defined by the linear state space model of Section 2.3.3, with the introduction of disturbance process $N$ and observation noise $W$:

```
$X(k+1) = FX(k) + GU(k) + N(k+1),\nY(k) = HX(k) + W(k).\quad (7.45)
```

The joint process $\{N(k),W(k) : k \ge 0\}$ is assumed to be independent and identically distributed. The process process $N$ represents a system disturbance, in the sense that it is uncontrolled and impacts the state (whose entries represent physical quantities). The variable
