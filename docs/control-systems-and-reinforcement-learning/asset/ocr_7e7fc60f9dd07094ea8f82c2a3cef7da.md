# 7.1 MDPs: A Quick Introduction

# Notation and Conventions

The standard MDP terminology uses “Markov” in the definition of a stationary policy:

+   - Markov policy: $U(k) = \phi_k(X(k))$ for a sequence of maps $\phi_k: X 	o U, k \ge 0$.
- Stationary Markov policy: $U(k) = \Phi(X(k))$.

We usually opt for simply “stationary policy” or even “policy” for $\phi$, which is also synonymous with the term feedback law introduced in Chapter 2.

These definitions extend to randomized policies by substituting $X'$ for $X$. However, it is cumbersome to introduce & whenever we require randomization. We instead let $\phi$ denote a randomized policy, which is defined as a conditional probability: For each $u$ and $x$,
nP\{U(k) = u \mid X(0), \dots, X(k-1), U(0), \dots, X(k-1)\} = \phi(u \mid x)\}$. (7.11)

Proposition 7.1 then follows from these definitions:

**Proposition 7.1** *When the input sequence U is defined by a stationary (possibly randomized) policy $\phi$, it follows that the state process $X$ is a Markov chain, with transition matrix*
P_\phi(x,x') = \sum_u \phi(u \mid x)P_u(x,x'), \quad x,x' \in X$. (7.12)

For a function $h: X \to \mathbb{R}$, we use the following compact notation for expectations:

$P_u h(x) = \sum_{x'} \phi(u \mid x)P_u(x,x')h(x') = E[h(X(k+1)) \mid X(k) = x, U(k) = u],
P_u h(x) = \sum_{x'} \phi(u \mid x)P_u(x,x')h(x') = E[h(X(k+1)) \mid X(k) = x],$ (7.13)

where $X$ is controlled by using policy in the second decision.

*For Those of You Who Know About Stochastic Processes*
The expression (7.9) is an example of an equation that is begging for streamlined notation. It is common to introduce a nondecreasing sequence of $\sigma$-algebras (a *filtration*) as a way to model the history appearing in this equation:

```
$\mathcal{F}_k = \sigma\{X(0), \dots, X(k), U(0), \dots, U(k)\}$. (7.14)
```

If “$\sigma$” looks foreign to you, then simply take $\mathcal{F}_k$ as a notational convention. We have under no admissible input

```
$P\{X(k+1) = x' \mid \mathcal{F}_k; X(k) = x, U(k) = u\} = P_u(x,x')$ (7.15a)
```

and for any function $h: X \to \mathbb{R}$,

```
$E[h(X(k+1)) \mid \mathcal{F}_k; X(k) = x] = \sum_{x'} P_u(x,x')h(x'),$ (7.15b)
```