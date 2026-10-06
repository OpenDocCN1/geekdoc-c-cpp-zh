
Suppose that the function J is convex. Jensen's inequality implies the bound

> E[J(X(k+1)) | X(k) = x, U(k) = u] \geq J(E[X(k+1) | X(k) = x, U(k) = u]) J(\bar{F}(x,u)).

It follows from (7.24b) that $\eta$ is a nonnegative function of $(x,u)$ in this special case.
Consider application of the lemma with $J = J^*$. The value function satisfies the assumptions of the lemma, the DP equation (7.22) for the fluid model implies a DP equation to the MDP model:

$J^*(x) = \min_{u} c(x,u) - \eta(x) + P_u J^*(x), \quad x \in X. (7.25)$

In many examples to we find that $\eta$ is small enough compared to $c$, so that $c^*$ approximately solves the ACOE. In fact, this will be much smaller in the span norm:

$|\eta||_{\infty} \triangleq \max_{x,u} |\eta(x,u) - g|$.

Let $q^o$ denote the minimizer and $c^*(x,u) = c(x,u) - \eta(x,u) - q^o$, (7.22) becomes

$q^o + J^*(x) = \min_{u} c^*(x,u) + P_u J^*(x)\}. (7.26)$

Hence $J^*$ solves the ACOE with this cost function, and average cost $q^o$.

# Fluid Model in Continuous Time

The value function $J^*$ for total cost in continuous time solves the HJB equation:

$0 = \min_{u} c(x,u) + f(x,u) \cdot J^*(x)\}. (7.27)$

Justification of the continuous time model requires a different application of the MVT (7.20). We take $x' = X(k+1)$ as before, but now $x = X(k)$ to obtain

$J(X(k+1)) = J(X(k)) + \nabla J(X) \cdot \{X(k+1) - X(k)\},$

$\bar{X}$ lies on the line segment with endpoints $X(k)$ and $X(k+1)$. Denote

$\eta(k+1) = \{\nabla J(X) - \nabla J(X(k)) \cdot \{X(k+1) - X(k)\}\}$.

**Lemma 7.3** Suppose that $J: X \to \mathbb{R}$ is differentiable, and its gradients satisfy the Lipschitz bound (7.21). Then the following approximation holds for each k:

$J(X(k+1)) = J(X(k)) + \nabla J(X) \cdot \{X(k+1) - X(k)\} + \eta(k+1),$
$|\eta(k+1)| \leq L ||X(k+1) - X(k)||^2. (7.28a)$

Consequently, for any $x,u$, and,

$P_u J(x) - J(x) = \nabla J(x) \cdot \tilde{f}(x,u) + \eta(x,u),$

$\eta(x,u) = E[\eta(k+1) | X(k) = x, U(k) = u]$.

![](img/0790f102da4ffa7564329bf76c7d0815_267_0.png)

# 7.3 Queues

Applying the lemma with $J = J^*$ solving (7.27), we again arrive at the representation (7.25), whenever $J^*$ satisfies the assumptions of Lemma 7.3. In practice, these lemmas are useful as motivation to initially ignore disturbances in control design. Simple applications can be found in the remainder of this chapter:

The reflected random walk, introduced in Example 6.2, is a model for the evolution of workload in the single server queue. The **controlled random walk** (CRW) queue has its form, but with an input of:

$X(k+1) = X(k) - S(k+1)U(k) + A(k+1), \quad (7.29)$

where $N(k)\overset{\text{iid}}{=}(S(k), A(k))$ is an i.i.d. sequence, and $S(k)$ has a Bernoulli distribution. It is assumed that $X_i \overset{\text{iid}}{=}\{0,1\}$ and $U \overset{\text{iid}}{=}\{0,1\}$. The input process is interpreted as the sequences of times at which the server is busy. It is subject to the constraint $U(k) \in U(X(k))$ for each $k$, where $U(x)=\{0,1\}$ for $x \ge 1$, and $U(0)=\{0\}$ (the server can't work if there is nobody in the queue).

Example 6.2.3 provides a simple example where $A$ is an i.i.d. Bernoulli process with parameter $\alpha$. Setting $S(k) = 1 - A(k)$ for each $k$, it follows that $S$ is also an i.i.d. Bernoulli process with parameter $\mu = 1 - \alpha$. The MDP in this case is the controlled M/M/1 queue:

- (i) The following is controlled transition matrix:
$P_u(x,x') = \begin{cases} \alpha & x' = x+1 \\ \mu & x' = x-1 \\ 0 & \text{else}\end{cases} \quad (7.30)$
- (ii) A standard cost function is $c(x,u) = x$ for each $x$, so that $E[c(X(k))]$ is the mean queue length at time $k$.
- (iii) A typical objective in queuing applications is average cost, which requires $\rho = \alpha/\mu < 1$. The M/M/1 queue is obtained with the idle policy, $U(k) = \phi^*(X(k))$, with $\phi^*(x) = 1$ for $x \ge 1$. This is average cost, resulting in $\eta^* = \rho/(1-\rho)$.

Stochastic Control
![](img/0790f102da4ffa7564329bf76c7d0815_269_0.png)

# 7.3.1 Fluid Models and Value Functions

To define fluid model for the CRW queue, we begin with convex relaxation, taking $X = \dots$, and $U = [0,1]$. The mean-field dynamics and mean-field vector field associated with (7.29) are $\hat{f}(x,u) = E[X(k+1) - S(k)U(k) + A(k+1) \mid X(k) = x, U(k) = u]$ $\hat{f}(x,u) = -\mu+\alpha$.

Shown on the left-hand side of Figure 7.1 is a copy of the left-side of Figure 6.1, and on the right-side is the solution of fluid model $\frac{dq}{dt} = \hat{f}(q)$, under the idle policy $u=1$ when $q > 0$, and $u = \alpha/\mu$ otherwise.

Let's compare three value functions under the respective policies, and cost function $c(x,u) = x$:

- (i) It is easy to verify that the ACOE (7.5) is given by $h^*(x) = \frac{x^2+x}{\mu-\alpha}. \quad (7.31)$
- (ii) The value function in continuous time is easily obtained: $J^*(x) = \int_0^W q_t dt = \int_0^x q_t dt = \frac{1}{2}W \times x$ (area of a triangle), where $H$ refers to the height of the triangle defined by the linear path of $q$, and $W$ the width, which is the time to reach zero. A glance at the plot on the right-side of Figure 7.1 should convince you that $H = x/(\mu-\alpha)$, so that $J^*(x) = \frac{x^2}{\mu-\alpha}$. We can compute the function $\eta(x,u)$ appearing in 7.28b: $\eta(x,u) = E[J^*(X(k+1)) - J^*(X(k)) \mid X(k) = x, U(k) = u] - \nabla J^*(x) \cdot \hat{f}(x,u) = \frac{1}{2}\frac{\mu u+\alpha}{\mu-\alpha}$. This is bounded, and independent of $x$. It follows from Lemma 7.3 that $J^*$ almost solves ACOE for the MDP model.

# 7.4 Speed Scaling

- (iii) Treatment of fluid model in discrete time is a bit more complex:
- (a) The fluid model becomes $x(k+1) = \bar{F}(x(k), u(k)) = x(k) - \mu u(k) + \alpha$.
- (b) The optimal policy is maximal, subject to the constraint $x(k) \geq 0$ for each $k$, $\Phi^*(x) = \min\{1, (x+\alpha)/\mu\}$. This results in $x(k+1) = 0$ when $x(k) \leq \mu - \alpha$.
- (c) The total cost is given by $J^*(x) = \begin{cases} x & x \leq \mu-\alpha \\ \frac{x^2}{\mu-\alpha} + \frac{1}{2}x & \text{otherwise}\end{cases}.$ This follows by direct computation, or verification that this function solves the DP equation $J^*(x) = \min_u\{c(x,u) + J^*(\bar{F}(x,u))\}$, with boundary condition $J^*(0) = 0.$

The example stability of the value functions in this process is the product of two factors: the cost function $c$ is Lipschitz continuous, and the MDP is "skip-free" in a mean-square sense: $E[|X(k+1) - X(k)|^2 \mid X(k)=x, U(k)=u] < \infty.$ The next example visits the skip-free property. However, the continuous-time fluid model approximation is accurate because $\nabla J^*$ as the states tend to infinity.

**Dynamic speed scaling** in processor uses algorithms that adjust processing speed in response to environment. While initially proposed for processor design [25], the ideas have impacted other application areas such as wireless communication.

Dynamic speed scaling is modeled as an MDP in discrete time, using a variation of the CRW queuing model. For each $k=0,1,2,...,$ $A(k)$ denote arrivals in this time slot, $X(k)$ the number of jobs in the queue awaiting service, and $U(k)$ the rate of service. The evolution of the state is

$X(k+1) = X(k) - U(k) + A(k+1), \quad k \geq 0. \quad (7.32)$

It is assumed that the arrival process $A$ is i.i.d., so that this forms the dynamic system for an MDP model. One source of complexity comes from integer constraints on the state and input: each evolve on the non-negative integers $X = U = \mathbb{Z}_+ = \{0,1,2,3...\}$, and the constraint $U(k) \leq x$ is also imposed, so that $U(x) \in \mathbb{Z}_+ : u \leq x.$

The arrival process also evolves in $\mathbb{Z}_+$. The common mean and variance of $A(k)$ are assumed, with mean denoted $\alpha$. Assume moreover that $P\{A(1) > 0\} > 0$. Under this assumption, there is a stationary policy under which $X$ becomes a Markov chain that $x^*$-irreducible with $x^* = 0$ (see 6.57 and surrounding discussion). A simple example is

$U(k) = \Phi^k(X(k)) = X(k),$

that $X(k) = A(k)$ for $k \geq 1.$
