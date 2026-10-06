(4) If step (2) is skipped (no modification is needed), and step (3) is answered in the
airmative, then we arrive at the SA algorithm:

$$\theta_{n+1} = \theta_n + \alpha_n\{-H^{\theta_n}(\Phi(n)) + c(\Phi(n)) + \gamma H^{\theta_n}(X(n+1))}\zeta_n. \quad (9.72)$

**Q(0)-Learning** The recursion (0.972) using $\zeta_n = \nabla H^{\theta_n}(\Phi(n))$$
For a linear parametrization $\theta^0 = \psi(n)$, this gives $\zeta_n = \psi(n).$.

In general, the ODE method fails at step (3) when the state is not finite. An example
of the LQG problem in $\{\theta^0 \in \mathbb{R}^d\}$ is a linearly parameterized family of quadratic
functions on $X \times U$. In $H$ is rarely Lipschitz continuous as a function of $\theta$ – see
Exercise 9.4 for an example.

In the finite state setting, we can expect Lipschitz continuity, but conditions ensuring
stability of the ODE are not easily verified.

# 9.2 Watkins’s Algorithms

One great success story is in the special case tabular Q-learning, with the basis
previously defined in (5.10): $\psi_i(x,u) = \mathbb{1}(x,u)=(x^i,u)$ for each $i$, with $X \times$
$\{x^i,u^i\} : 1 \le i \le d\}$, but in the tabular setting we write $\theta^0 \in \mathbb{R}^d$, where $d=|X| \times |U|$,$
and the function class spans all possible functions on $X \times U$. For this architecture, the stability
of TD learning admits extension to the nonlinear SA algorithm (9.72).
A simple stochastic-path problem we use to illustrate the state space $X=\{1,...,6\}$ coincides with the six nodes on the un-directed graph shown
on the left-hand side of Figure 9.1. The input space coincides with the edges shown: $U =$
$\{e_{x,x'} : x,x' \in X\}$. The controlled transition matrix is defined as: If $X(n)=x \in X$,

$$c(x,u) =$
$U(n)=e_{x,x'} \in U$, then $X(n+1)=x'$ with probability 0.8, and with probability 0.2,
next state is randomly chosen between the other neighboring nodes. The goal is to
reach the state $x'=6$ and maximize the time spent there. The cost function is designed with this
goal in mind, and also a cost for any node:

```
$c(x,u) = \begin{cases} 0 & u=e_{x,x}, & x \neq 6, \ 5 & u=e_{x',x'}, & x' \neq 6,x \neq x', \ -100 & u=e_{x,6}. \end{cases}$
```

![](bbox=[0.115, 0.762, 0.884, 0.893])

Figure 9.1 Six-state directed graph for a finite state MDP example.