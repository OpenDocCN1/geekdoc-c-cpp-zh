
(4) If step (2) is skipped (no modification is needed), and step (3) is answered in the affirmative, then we arrive at the SA algorithm:

$$\theta_{n+1} = \theta_n + \alpha_n\{-H^{\theta_n}(\Phi(n)) + c(\Phi(n)) + \gamma H^{\theta_n}(X(n+1))}\zeta_n. \quad (9.72)$$

**Q(0)-Learning** The recursion (0.972) using $\zeta_n = \nabla H^{\theta_n}(\Phi(n))$$
For a linear parametrization $\theta^0 = \psi(n)$, this gives $\zeta_n = \psi(n)$.

In general, the ODE method fails at step (3) when the state is not finite. An example of the LQG problem in $\{\theta^0 \in \mathbb{R}^d\}$ is a linearly parameterized family of quadratic functions on $X \times U$. In $H$ is rarely Lipschitz continuous as a function of $\theta$ – see Exercise 9.4 for an example.

In the finite state setting, we can expect Lipschitz continuity, but conditions ensuring stability of the ODE are not easily verified.

## 9.2 Watkins’s Algorithms

One great success story is in the special case tabular Q-learning, with the basis previously defined in (5.10): $\psi_i(x,u) = \mathbb{1}(x,u)=(x^i,u)$ for each $i$, with $X \times \{x^i,u^i\} : 1 \le i \le d\}$, but in the tabular setting we write $\theta^0 \in \mathbb{R}^d$, where $d=|X| \times |U|$, and the function class spans all possible functions on $X \times U$. For this architecture, the stability of TD learning admits extension to the nonlinear SA algorithm (9.72).

A simple stochastic-path problem we use to illustrate the state space $X=\{1,...,6\}$ coincides with the six nodes on the undirected graph shown on the left-hand side of Figure 9.1. The input space coincides with the edges shown: $U = \{e_{x,x'} : x,x' \in X\}$. The controlled transition matrix is defined as: If $X(n)=x \in X$, $U(n)=e_{x,x'} \in U$, then $X(n+1)=x'$ with probability 0.8, and with probability 0.2, next state is randomly chosen between the other neighboring nodes. The goal is to reach the state $x'=6$ and maximize the time spent there. The cost function is designed with this goal in mind, and also a cost for any node:

```
$c(x,u) = \begin{cases} 0 & u=e_{x,x}, & x \neq 6, \ 5 & u=e_{x',x'}, & x' \neq 6,x \neq x', \ -100 & u=e_{x,6}. \end{cases}$
```

![](img/0790f102da4ffa7564329bf76c7d0815_355_0.png)

Figure 9.1 Six-state directed graph for a finite state MDP example.

## 9.6 Watkins’s Q-Learning

In the tabular setting, it is common to write $H^n$ rather than $H^{\theta_n}$ (identifying the function approximation with the parameter). This is justified by the following representation: For $i$ and $\theta$,

```
$H^0(x^i, u^i) = \sum_{j=1}^d \theta(j)\psi_j(x^i, u^i) = \theta(i), \quad (9.73)$
```

where the final equality holds because of the tabular basis. Two versions of tabular Q-learning are distinguished by the way in which samples of $\Phi=(X,U)$ are obtained.

Either of the following algorithms is commonly known as Watkins’ Q-learning.

- (i) Asynchronous: access to a single sample path of $\Phi$. $H^{n+1}(x,u) = H^n(x,u)$ if $\Phi(n) \neq (x,u)$, and otherwise $H^{n+1}(x,u) = H^n(x,u) + \alpha_{n+1}[-H^n(x,u) + \gamma H^n(X(n+1))]$. Asynchronous Q-learning can be implemented with a simulator to approximate $Q^*$ based on observations of the system.

- (ii) Synchronous: access to a simulator to generate the generic distribution $P_u(x,\cdot)$ via i.i.d. sample $\Xi$ on $X^n$, with $\Xi_n \sim P_u(x)$. At iteration $n+1$ each entry of $H^{n+1}$ is updated for $i=1, \dots, d$, $H^{n+1}(x^i,u^i) = H^n(x^i,u^i) + \alpha_{n+1}[-H^n(x^i,u^i) + \gamma H^n(\Xi^i)]$.

In either case, given the estimate of the Q-function at iteration $n$, we obtain the $H^n$-greedy policy as solution to

```
$\phi_n(x) = \arg \max_{u} H^n(x,u), \quad x \in X. \quad (9.74)$
```

This section restricts itself to the asynchronous case (to avoid repetition of equations and concepts in the theoretical development). Given the definition of basis, asynchronous Q-learning is expressed as Q(0)-learning:

```
$\theta_{n+1} = \theta_n + \alpha_{n+1}\mathcal{D}_n,$
$\mathcal{D}_{n+1} = -H^n(\Phi(n)) + c_n + \gamma H^n(X(n+1)),$
$\zeta_n = \nabla_{\theta}H^n(\Phi(n))|_{\theta_n} = \psi(n). \quad (9.75)$
```

The recursion (9.75) for the Q-learning algorithm can be written in a form similar to linear recursion (8.53). By denoting $\zeta_{n+1} = \psi(X(n+1))\phi_n(X(n+1))$, with $\phi_n$ $H^n$-greedy policy,

```
$\theta_{n+1} = \theta_n + \alpha_{n+1}[A_{n+1}\theta_n - b_{n+1}],$
$\text{with } A_{n+1} = \psi(n)\psi(n)^\top, b_{n+1} = -c_n\psi(n). \quad (9.76)$
```

This is not a linear SA algorithm since the policy $\phi_n$ depends on $\theta_n$.

## Temporal Difference Methods

It should be noted that the algorithm (9.76) can be implemented with an arbitrary basis. The restriction to the tabular setting is made in this section only because there is no complete and accessible stability theory for Watkins' algorithms and refinements to come.

### 9.6.3 Exploration

It is common to employ the Gibbs policy (9.46a) using $G = H^n$;

```
$P(U(n) = u \mid X(n) = x) = \frac{1}{\kappa^n(x)}\exp(-H^n(x,u)/\varepsilon), \quad (9.77)$
```

where $\kappa^n$ is a normalizing constant, and $\varepsilon > 0$ is typically constant (it may depend too much upon $n$, possibly vanishing as $n \to \infty$). This is often highly, but avoided in the theoretical development of this chapter. While SA theory has now matured to the point where it can be applied to establish stability of Q-learning with a time-varying policy as this, there is no space in this book for a proper treatment.

We assume that $U$ is defined using a random Markov process $\phi$, so that $\Phi = \{\Phi(k) \overset{def}{}= X(k), U(k) : k \ge 0\}$ is a Markov chain. Recall from (9.3b) that its invariant pmf can be expressed as $\varrho(x,u) = \pi(x)\phi(u)$, where $\pi$ is invariant pmf of Markov chain $X$. It is assumed throughout that $X$ is irreducible, so $\pi$ is unique.

Linear independence of the basis is defined by the rank condition $R^\varrho > 0$, with matrix $R^\varrho$ defined in (9.24). For the tabular setting, this reduces to the diagonal matrix, (9.25):

```
$R^\varrho(i,i) = \varrho(x^i,u^i), \quad 1 \le i \le d. \quad (9.78)$
```

It follows that the tabular basis is full rank only if $\varrho(x^i,u^i)$ is nonzero for each $i$.

Watkins' algorithm (9.75) admits a simple ODE approximation.

## 9.6.4 ODE Analysis

**Proposition 9.15** The ODE approximation for the Q-learning algorithm (9.75) takes the form $\frac{d}{dt}\theta_i = f^0(\theta_i)$, with vector field

```
$f^0(\theta) = \varrho(x^i,u^i) [-H^0(x^i) + c(x^i) + \gamma \sum_{x'} P_a(x^i,x')]$.
```

Concavity of $f^0_i$ for each $i$ follows because $f^0(\theta)$ is concave in $\theta$, as it is minimum of linear functions. This fact is useful when we want Q-learning to converge. Proposition 9.15 raises concerns: the premultiplication by $\varrho(x^i,u^i)$ in vector field $f^0$ introduces "low gain" for state-input pairs that are rarely visited, and "the curse of dimensionality" will be severe if $\varrho$ is far from the invariant pmf (see Section 8.1). The path-finding problem provides an example of this curse. The eigenvalues of $A=-\nabla f^0(\theta)$ are real and negative in this example. The right-hand side of Figure 9.1 shows $\{-\lambda_i\}$ on log scale for values of $\gamma$. As $A$ is Hurwitz, using the step-size $\alpha_n = 1/n$, the asymptotic covariance of the resulting algorithm is obtained as solution to the Lyapunov function (8.28), provided each eigenvalue of $A$ is strictly less than $-1/2$. This translates to bound $g > 1/2$ for $\gamma=0.8$, and $g > 0$ for $\gamma=0.9$.

## 9.6 Watkins's Q-Learning

Observations inherit the state-dependent step-size rule: $\alpha_n(x,u) = 0$ for any $i$ satisfying $\Phi(k) \neq (x,u)$ for $k \leq n$, otherwise $\alpha_n(x,u) = [\text{number of times } (x,u) \text{ has been visited up } n]^{-1}$.

**Proposition 9.16** The following holds for Watkins' Q-learning with step-size rule (9.79), under the assumption that $\Phi$ is everywhere:

- (i) It is equivalent as the Q(0)-learning algorithm (9.75) with $\alpha_n = 1/n$, and modified using a diagonal matrix gain:

```
$\theta_{n+1} = \theta_n + \frac{1}{n+1}G_{n+1}\zeta_n, \quad G_n = \frac{1}{n}\sum_{k=0}^n \zeta_k\zeta_k^\top$.
```
with $G_n^{(i,i)} = 0$ if $\Phi(k) \neq (x^k, u^k)$ for $k \leq n$.

- (ii) Our ODE approximation vector field with components

```
$f_i(\theta_n) = -H^0(x^n, u^n) + c(x^n, u^n) + \gamma\sum_{x'} P_a(x^i,x')H^0(x')$.
```

- (iii) The recursion rule in (9.80) admits the representation

```
$\theta_{n+1} = \theta_n + \alpha_{n+1}\{G_n\zeta_n^\top f(\theta_n) + \Delta_{n+1}\}$,
```

where $\{\Delta_n : n \geq 1\}$ is a martingale difference sequence.

The sequence $\{\Delta_n^o\}$ of the form $\Delta_{n+1} = \Delta_{n+1}G_n\zeta_n$ in $\{\Delta_n^o\}$ is a scalar martingale difference sequence satisfying

```
$E[\Delta_{n+1} | \mathcal{F}_n] = 0$.
```

where $\mathcal{F}_n$ represents $\Phi(0), \dots, \Phi(n)$. The martingale difference property for

```
$E[\Delta_{n+1} | \mathcal{F}_n] = E[\Delta_{n+1} | \mathcal{F}_n]G_n\zeta_n$.
```

Let $i_n$ be the unique index for which $\zeta_n(i_n) = 1$ (that is, $\Phi(n) = X(n), U(n) = (x^n, u^n)$ with $i = i_n$), and denote

```
$\Delta_{n+1}^o \overset{\text{def}}{}=-H^0(x^n, u^n) + c(x^n, u^n) + \gamma\Pi^0(X(n+1)) - \hat{f}_n(\theta_n)$
```

```
$= \gamma\Pi^0(X(n+1)) - \sum_{i=1}^d P_a(x^i, u^i)H^0(x^i)|_{i=i_n},
```

where the final equation follows from (9.81). The contraction $E[\Delta_{n+1}^o | \mathcal{F}_n] = 0$ follows from the interpretation of the controlled transition matrix as a conditional expectation:

```
$\Delta_{n+1}^o = \gamma\Pi^0(X(n+1)) - E[\gamma\Pi^0(X(n+1)) | \mathcal{F}_n]$.
```
