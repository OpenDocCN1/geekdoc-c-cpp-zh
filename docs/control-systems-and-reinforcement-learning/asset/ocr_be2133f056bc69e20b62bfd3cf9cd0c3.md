# 3.2 Bellman Equation

Optimal trajectory starting from $x$ at time $t = 0$
Optimal trajectory starting from $x_m$ at time $k_m$

![](bbox=[0.397, 0.098, 0.702, 0.155])

**Figure 3.1** Principle of optimality: if a better control existed on $[k_m, \infty)$, we would have chosen it.

```
$J^*(x) = \min_{u_{k_m-1}} \sum c(x(k),u(k)) + J^*(x(k_m))$. (3.4)
```

As a consequence, the optimal control over the interval has the property illustrated in Figure 3.1: If the optimal trajectory follows the state $x_m$ at time $x(k_m)$ using the control $u^*=u_{(0, \infty)}$, then the control $u^*_{k_m}$ must be optimal for the system starting at $x_m$ at time $k_m$. If a better $u^*$ existed on $[k_m, \infty)$, we would have chosen it. This concept is called the *principle of optimality*.
Analysis in continuous time proceeds by letting $k_m \downarrow 0$ to obtain a partial differential equation. The theory is far simpler in discrete time: Set $k_m=1$ to obtain the following celebrated result.

**Theorem 3.1** Suppose that the value function $J^*$ is finite valued, and an optimal input $u^*$ solving (3.2) exists. Then the value function satisfies

```
$J^*(x) = \min \{c(x,u) + J^*(F(x,u))\}$. (3.5)
```

Suppose that the minimum in (3.5) is unique for each $x$, and let $\phi^*(x)$ denote the minimum. The optimal input is expressed as state feedback.

```
$u^*(k) = \phi^*(x^*(k))$. (3.6)
```

[]

Equation (3.5) is often interpreted as a *fixed point equation* in the unknown "variable" $J^*$. It goes by the name *Bellman equation* or dynamic programming (DP) equation: the terms are used interchangeably in this book.

**Q-Function.** The function of two variables within the minimum in (3.5) is the *Q-function* of reinforcement learning:
$Q^*(x,u) \overset{\text{def}}{=} c(x,u) + J^*(F(x,u))$. (3.7a)
The Bellman equation is expressed
$J^*(x) = \min_u Q^*(x,u)$ (3.7b)
and the optimal feedback law any minimizes expressed as follows:
$\Phi^*(x) \in \arg \min_u Q^*(x,u), \quad x \in X$. (3.7c)