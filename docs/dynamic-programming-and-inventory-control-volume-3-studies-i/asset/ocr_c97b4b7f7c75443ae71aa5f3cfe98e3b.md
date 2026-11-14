# 7.1.2. DYNAMIC PROGRAMMING EQUATION.

The functional equation giving the value function of the preceding problem is defined by

(7.1.4) $$u(x) = \min \{ \psi(x), \inf_{v \in U} [l(x, v) + \alpha \Phi^v u(x)] \}, \forall x.$$

This functional equation combines the nonlinear operator studied in Chapter 4, with the function $\psi(x)$. We call this function, the obstacle. This refers to the fact that the solution $u(x)$ must remain below the obstacle. As we see in equation (7.1.4), it represents in the cost functional the payoff received at the decision time $\tau$.

We shall consider the ceiling function $w_0(x)$, defined in equation (4.3.4).

We state the main result

# Theorem 7.1. Under the assumptions (7.1.1), (7.1.2) (4.3.1), (4.3.2) and (4.3.6) then the set of solutions of the functional equation (7.1.4) satisfying

```
$$0 \le u(x) \le w_0(x) \quad \forall x,$$
```

is not empty and has a minimum and a maximum solution, denoted respectively $\underline{u}(x)$ and $\overline{u}(x)$. The minimum solution is l.s.c. and the maximum solution is u.s.c. if the functions $[l(x, v)$ and $\psi$ are continuous.

PROOF. Let $z$ be l.s.c. and positive. Define

```
$$Tz(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v z(x)].$$
```

We know from Chapter 4 that $Tz$ is also l.s.c. and positive. Set

```
$$Sz(x) = \min[\psi(x), Tz(x)].$$
```

We use the following exercise to claim that $S(z)$ is also l.s.c. and positive.

# Exercise 7.1. If $f$ and $g$ are l.s.i and bounded below then $\min(f, g)$ is also l.s.c. and bounded below.

The function $u$ solution of equation (7.1.4) is a fixed point of the map $S$. The map $S$ is increasing, i.e. if $z_1 \le z_2$ then $Sz_1 \le Sz_2$. If $z \ge 0$ then $Sz \ge 0$. Suppose $z \le \tilde{w}$ then

```
$$Sz(x) \le l(x, v) + \alpha \Phi^{w_0} w_0(x) = w_0(x).$$
```

We have checked that $S$ maps the interval $[0, w_0]$ into itself. Consider next the decreasing scheme

```
$$u^{n+1} = Su^n, \quad u^0 = w_0.$$
```

Clearly

```
$$u^0 \ge u^1 \ge \dots \ge u^n \dots \ge 0.$$
```

We can state that $u^n \downarrow u$ where $u$ is a positive Borel function. Clearly $u^{n+1} \ge Su$, hence also $u \ge Su$. Also

```
$$\begin{aligned} u^{n+1}(x) &\le \psi(x) \\ u^{n+1}(x) &\le l(x, v) + \alpha \Phi^v u^n(x), \quad \forall v \end{aligned}$$
```

Letting $n$ tend to $+\infty$ yields

```
$$\begin{aligned} u(x) &\le \psi(x) \\ u(x) &\le l(x, v) + \alpha \Phi^v u(x), \quad \forall v \end{aligned}$$
```

Therefore $u \le Su$. So the limit $u$ is a fixed point of $S$. Moreover it is the maximum solution in the interval $[0, w_0]$. It is u.s.c. as decreasing limit of a sequence of continuous functions.