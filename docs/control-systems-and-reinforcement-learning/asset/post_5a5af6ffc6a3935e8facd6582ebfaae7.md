
# Mathematical Background

It is interpreted as a possible realization of the stochastic process, so that $X_k(\omega) = \omega_k$. When $\Omega$ is defined in this way, the event defined in (A.2) becomes

> $E_{(x_0,\dots,x_N)} = \{\omega \in \Omega : \omega_i = x_i, \quad 0 \leq i \leq N\}. \quad (A.3)$

And in this, we typically take $F$ to be the smallest $\sigma$-field that contains all events of the (A.3), where $N$ ranges over all integers $N \geq 0$, and the $\{x_i\}$ can take on any value in $X$. This $\sigma$-field contains any event, including

> ${\omega \in \Omega : \lim_{T \to \infty} \frac{1}{T} \sum_{i=0}^{T-1} c(\omega_i) = \eta\}$

where $c: X \to \mathbb{R}$ is any function, and $\eta \in \mathbb{R}$ any constant.

# A.2.2 Markov Chain Basics

We will keep things simple and assume that the state space X for the Markov chain is finite or countably infinite. The transition matrix is denoted P. For each $\mu$ on $X$, there is a probability measure $P_{\mu}$ on $\mathcal{F}$ defined so that $\mu$ is the initial distribution for the chain. Consistent with definitions in Chapter 6,

> $P_{\mu}[X_0 = x] = \mu(x)$

> $P_{\mu}[X_k = x] = \sum_{x' \in X} \mu(x') P^k(x',x), \quad x \in X$,

> $E_{\mu}[g(X_k)] = \sum_{x} P_{\mu}\{X_k = x\}g(x) \quad$ for any $g: X \to \mathbb{R}$.

When $\mu$ is degenerate, in the case that $\mu(x)=1$ for some $x$, then we write $P_{\mu}$ and $E_x$. The *shift operators* are mappings on $\Omega$ that provide compact language for complex concepts. For each $k$, the shift operator $\theta^k$ maps an element $\omega = \{x_0, x_1, \dots, x_n, \dots\} \in \Omega$ to a new value via

> $\theta^k\omega = \{x_k, x_{k+1}, \dots, x_{n+k}, \dots\}$.

It defines a transformation on random variables $H$ by

> $(\theta^kH)(\omega) = H(\theta^k\omega)$.

Hence if the random variable $H$ is of the form $h = h(X_0, X_1, \dots)$ for a function $h$, then

> $\theta^kH = h(X_k, X_{k+1}, \dots, \dots)$.

Specializing to $H = h(X_n)$ for some $n$ and $h: X \to \mathbb{R}$ gives

> $\theta^kH = h(X_{n+k)$

and hence

> $E_{\mu}[\theta^kH | \mathcal{F}_k] = E_{\mu}[h(X_{n+k}) | \mathcal{F}_k]$

> $E_{\mu}[h(X_{n+k}) | X_k]$

> $\sum_{x'} P^n(x', x)h(x')_{x=X_k}$

by the Markov property definition of transition matrix.

# A.2 Probability and Markovian Background

This can be generalized: For any initial distribution $X_0 \sim \mu$, any bounded random variable $H$, and fixed $k, n \in \mathbb{Z}_+$.

```
$E_{\mu}[\theta^k H | \mathcal{F}_k] = E_x[H]_{x=X_k} \quad \text{a.s.}[P_{\mu}]. \quad (A.4)$
```

This describes the (time-homogeneous) *Markov* property in a succinct way. Hence, Note that we are viewing $E_x[H]$ as a real-valued function on the state space. Here we substitute the following:

```
$E_x[H] = E_x[H]_{x=X_k}.
```

# A.2.3 Strong Markov Property

The strong Markov property is described by a significant extension of the formula (A.4). The definition of this property requires these three ingredients:

- (i) A function $\tau : \Omega \to \mathbb{Z}_+ \cup\{\infty\}$ is a *stopping time* for **X** if the event $\{\tau = n\}$ lies in $\mathcal{F}_n$ for each $n \in \mathbb{Z}_+$. That is, for each $n$ there is a function $f_n$ such that $\{\tau = n\} = f_n(X_0, \dots, X_n)$.

- (ii) The associated shift operator $\theta^{\tau}$ is defined exactly as before: $\theta^{\tau} H = h(X_{\tau}, X_{\tau+1}, \dots)$.

- (iii) An associated $\sigma$-field is also defined as: $\mathcal{F}_\tau \stackrel{\text{def}}{=} \{A \in F :\{\tau = n\} \cap A \text{ for each } n \in \mathbb{Z}_+\} \quad (A.5)$

This is interpreted as the events that happen "up to time $\tau$."

Two important examples of stopping times, for any set $A \subset X$,

$\tau_A \stackrel{\text{def}}{=} \min\{n \ge 1 : X_n \in A\}$

$\sigma_A \stackrel{\text{def}}{=} \min\{n \ge 0 : X_n \in A\}$

is known as the first and hitting times into A, respectively.

**Proposition A.1** For any set $A \subset X$, the variables $\tau_A$ and $\sigma_A$ are stopping times for **X**.

*Proof* The random variables $\tau_A$ and $\sigma_A$ have this representation, for any $n \ge 1$,

```
$\{\tau_A = n\} = f_n(X_0, \dots, X_n) \stackrel{\text{def}}{=} \mathbb{1}\{X_n \in A\} \prod_{i=1}^{n-1} \mathbb{1}\{X_i \notin A\}$,
```

```
$\{\sigma_A = n\} = g_n(X_0, \dots, X_n) \stackrel{\text{def}}{=} \mathbb{1}\{X_n \in A\} \prod_{i=0}^{n-1} \mathbb{1}\{X_i \notin A\}$,
```

where $\prod_{i=1}^{0} = 1$ (handles the case $n=1$). For $n=0$, we have $\{\tau_A = 0\} = f_0(X_0) = 0$ and $\{\sigma_A = 0\} = g_0(X_0) \mathbb{1}\{X_0 \in A\}$. \square

# Mathematical Background

A finite-valued random variable $H$ that is $\mathcal{F}_t$-measurable can be expressed as an infinite sum:

```
$H = \sum_{n=0}^{\infty} h_n(X_0, \dots, X_n) \mathbb{1}\{\tau = n\}$
```

for a sequence of functions $\{h_n\}$; this is true for what property?

An example is the random variable $X_{\tau}$, defined by setting $X_{\tau} = X_n$ on the event $\{\tau = n\}$:

```
$X_{\tau} = \sum_{n=0}^{\infty} X_n \mathbb{1}\{\tau = n\}$
```

Finally, we come to key definition:

**Strong Markov Property** X has the strong Markov property if for any initial distribution $\mu$, any real-valued random variable $H$, and any stopping time $\tau$,

```
$E_{\mu}[\theta^{\tau} H | \mathcal{F}_{\tau}] = E_{X_{\tau}}[H] \quad \text{a.s.}[P_{\mu}]$, on the event $\{\tau < \infty\}$.quad (A.6)
```

**Proposition A.2** For a Markov chain **X** with discrete time parameter, the **strong Markov property** holds.

*Proof* This is a consequence of decomposing the expectations on both sides of (A.6) over the set $\{\tau = n\}$, and using the ordinary Markov property, at each of these fixed times $n$.

# Appendix B

# Markov Decision Processes

This section mirrors the optimal theory surveyed in Chapter 3. See 7.1 for the definition of an MDP and surrounding notation. Throughout the remainder of the appendix, it is assumed that the state space X and action space U are finite.

# B.1 Total Cost and Other Criteria

The definition of the total-cost value function $J^*$ defined in (3.2) is unchanged, except that we introduce an expectation and change the notation:

```
$h^*(x) = \min_{k=0}^{\infty} E_x[c(\Phi_k)],quad (B.1)
```

where $\Phi_k = (X_k, U_k)$, the minimum is over all admissible policies, and the subscript indicates $X_0 = x$.

When finite, this function solves the Bellman equation

```
$h^*(x) = \min_{u}\{c(x,u) + \sum_{x'} P_u(x,x')h^*(x')\}, \quad x \in X$.
```

This is similar to the dynamic programming equation (3.5) for $J^*$, especially when expressed in the equivalent sample path:

```
$h^*(X_k) = c(\Phi_k) + E[h^*(X_{k+1}) | \mathcal{F}_k] \quad \text{when } U_k = \phi^*(X_k).
```

Also similar to the deterministic setting, the optimal policy is any minimizer:

```
$\phi^*(x) \in \arg \min_{u}\{c(x,u) + \sum_{x'} P_u(x,x')h^*(x')\}, \quad x \in X$.
```

There is, however, a significant difference in the stochastic control formulation: In most cases, we find that $E_x[c(\Phi_k)]$ converges to a strictly positive constant, as $k \to \infty$, meaning $h^*$ is not finite. Why then should we care about (B.1)?

# B.1.1 Total Cost in Many Flavors

What follow are examples of optimization criteria for MDPs, and how they can be transformed to the total-cost criterion.

# Shortest Path Problem (SPP) Given a target set $S \subset X$ and a terminal cost $V_0: S \to \mathbb{R}$, define for each $x \in S^0$:

```
$h^*(x) = \min E_x \left[\sum_{k=0}^{\tau_S-1} c(\Phi_k) + V_0(X_{\tau_S})\right]$.
```

This is transformed to the total-cost problem by the enlargement of X to include a graveyard state denoted $\triangle$. The “graveyard property” indicates that $P_u(\triangle, \triangle) = 1$ for each $u$, and we impose $P_u(x, \triangle) = 1$, for $x \in S$ and any $u$. The cost function is also modified: $c(x, u) = V_0(x)$ for $x \in S$. Under these conventions, the value function for the SP can be represented as (B.1).

# Discounted-Cost Value Function Given a discount factor $\gamma \in [0, 1]$,

```
$h^*(x) = \min E_x \sum_{k=0}^{\infty} \gamma^k c(\Phi_k)]. (B.2)
```

Enlarge the state space for the MDP with a geometric random variable $T$ with parameter $\gamma$, and independent of everything:

```
$P[T \geq k | \Phi_0^x] = \gamma^k$.
```

Then $\Psi_k = (X_k, B_k)$ is a Markovian state, with $B_k = \mathbb{1}[T \geq k]$. Independence of **X** and **B** implies that

```
$\gamma^k E_x[c(\Phi_k)] = E_x[c(\Phi_k)B_k].
```

Consequently,

```
$h^*(x) = \min E_x \sum_{k=0}^{\infty} \widehat{c}(\Psi_k, U_k)].$
```

with $\widehat{c}(z,u) = c(x,u)b$ when $z = (x,b)$.

# Average Cost Optimal Control Denote the following for any input sequence:

```
$\eta_u(x) = \limsup_{n\to\infty} \frac{1}{n} \sumsum_{k=0}^{n-1} E_x[c(\Phi_k)]. (B.3)
```

The minimum over all admissible inputs is denoted $\eta^*(x)$.

The minimum is typically independent of $x$, and the solution is obtained via an SPP with modified cost. Consider

```
$h^*(x) = \min E_x \sum_{k=0}^{\tau_S-1} \{c(\Phi_k) - \eta^*\]. (B.4)
```
