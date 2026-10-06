# Optimal Control

**Proposition 3.9** Suppose that the value function $J^\star$ is finite valued, and the optimal policy $\phi^*(k)$ is stabilizing, in the sense that $x^*(k) 	o x^\star$ as $k 	o \infty$ for any initial condition.

Suppose that $J: X 	o \mathbb{R}$, is continuous, vanishes at $x^\star$, and solves

```
$J(x) \le \min \{c(x
```

$J = J^\star$.

*Proof* Adopt the same notation in inverse dynamic programming: $\phi^j(x)$ is defined as a minimizer in (3.35) for each $x$, and $J^j$ the associated value function (3.34). We have the bound $J^{N} \le J$ by the Comparison Theorem, Proposition 2.3. We can also establish the following by induction on $N$ (starting with (3.35)):

```
$J(x) \le \min_{u[0,N-1]} \{\sum_{k=0}^{N-1} c(x,u(k)) + J(x(N))\}\N^{N-1} \le \sum_{k=0}^{N-1} c^*(x,u^*(k)) + J(x^*(N)), \quad x(0)=x, u^*(k)=\phi^*(x^*(k))$ for all $k$,
```

with the second inequality obtained because we replaced the minimum with a specific policy. We have $J^*(N) \to 0$ as $N \to \infty$ by the assumptions on $J$ and $\phi^*$, and hence $J \le J^\star$.

Putting these bounds together gives for all $x$,

```
$J^*(x) \le J^{\star} \le J(x) \le J^*(x)$,
```

which implies these functions coincide, and in particular $J = J^\star$.

*Proof of 3.8* The assumptions on $J$ and $c^j$ are imposed so that we may apply Proposition 2.3 for the state space model subject to $u(k) = \phi^j(k)$. (Part) implies that $J^{jx}(x) \le J(x)$ for all $x$, and (iii) tells that $x^\star$ is globally stable under this policy. We can then apply Proposition 3.9 to establish equality:

```
$J(x) = J^{\star}(x) = \min_{u} \sum_{k=0}^{\infty} c^j(x^*(k),u(k))$.
```

In the proof of Proposition 3.9, the right-hand side can only be replaced by replacing the minimum with the optimal policy: $x(0) = x$,

```
$J^{\star}(x) = \sum_{k=0}^{\infty} c^j(x^*(k),u^*(k)) \le (1+j)J^*(x)$,
```

with the second inequality $c^j \le (1+j)c$.

# 3.5 Bellman Equation Is a Linear Program

One approach to control design is to introduce a family of value function approximations $\{J^	heta : \theta \in \mathbb{R}^d\}$, and compute the parameter $	heta^\star$ that minimizes the Bellman error, such as using the mean-square criterion (2.53). A significant challenge is that the loss function $\Gamma^	heta(J^	heta)$ is not convex, even when $J^	heta$ depends linearly on $	heta$.