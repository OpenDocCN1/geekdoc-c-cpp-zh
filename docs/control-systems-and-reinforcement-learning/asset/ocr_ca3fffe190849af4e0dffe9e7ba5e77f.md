# Temporal Difference Methods

the function class (9.15) to all functions of the pair $(x,y)$, the optimal mean-square error cannot be worse. The smoothing property is then the consistency identity,

```
E[Z \mid Y] = E[Z \mid X,Y] \mid Y]. \quad (9.16)
```

Computing a conditional expectation is obviously a lofty goal, given the size of the function class $\mathcal{H}$. How do we verify the characterization in Proposition 9.3, which requires an evaluation for each $g \in \mathcal{H}$? The answer is, cannot in most cases, so we resort to the approximation techniques used in Section 5.4.1.

Approximating the $L_2$ Projection Given basis functions $\{\psi_i\}$ defines a finite-dimensional function class with linear combinations $\mathcal{H} ={\psi_i : i \in \mathbb{R}^d\}$. The estimate $\phi^*(Y)$ of $Z$, with $\phi^* \in \mathcal{H}$, is defined by the Galerkin relaxation or a restricted projection:

+   Galerkin relaxation: Define a second collection of functions $\tilde{\mathcal{G}}={\psi_i^* : i \in \mathbb{R}^d\}$, and select $\phi^* \in \mathcal{H}$ that solves

```
0 = E[(Z - \phi^*(Y))g(Y)], \quad g \in \tilde{\mathcal{G}}. \quad (9.17)
```

+   Projection onto $\mathcal{H}$: Solve the following projection problem:

```
\phi^* \in \arg min{E[(Z - \phi^*(Y))^2]}; \quad \phi \in \mathcal{H}. \quad (9.18)
```

We write then

```
E[Z \mid Y] \overset{\text{eq}}{=} \phi^*(Y). \quad (9.19)
```

Proposition 9.4 implies that the solution to (9.18) is identical to the Galerkin relaxation using $\tilde{\mathcal{G}} = \mathcal{H}$. Its proof is similar to (and simpler than) the derivation of (5:18).

# Proposition 9.4 A function $\phi^* = \sum_i \psi_i^*$ solves the minimum in (9.18) if and only if

```
0 = E[(Z - \phi^*(Y))g(Y)], \quad g \in \mathcal{H}. \quad (9.20)
```

Any solution satisfies $\phi^* = \psi^* \theta^*$,

```
R^\psi = E[\psi^* Z], \quad (9.21)
```

where $R^\psi$ is a $d \times d$ matrix and $\psi^*$ is a $d$-dimensional vector, with entries

```
R_{ij}^\psi = E[\psi_i(Y)\psi_j(Y)], \quad \psi_i^* = E[Z \mid Y(Y)]. \quad (9.22)
```

Consequently, if $R^\psi$ is full rank, then $\theta^* = [R^\psi]^{-1}\psi^*$ is the unique solution.

# 9.2.2 Linear Independence

In this chapter, we apply Galerkin relaxation techniques on $Y = \psi(n) \overset{\text{eq}}{=} \Phi(n)$ for arbitrary $n$, where $\Phi$ is the Markov chain with transition matrix (9.3a) (in Section 9.4, we briefly consider the restriction to $X$ rather than the pair process $\Phi$). For the purpose of analysis, it is assumed that $\Phi$ is stationary, which implies that the $d$-dimensional stochastic process $\{\psi(n) : n \in \mathbb{Z}_+\}$ is also stationary, its autocorrelation function is denoted