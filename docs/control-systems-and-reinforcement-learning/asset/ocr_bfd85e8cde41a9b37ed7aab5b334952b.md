# Temporal Difference Methods

An alternative is to abandon approximation of $Q$ and turn to the advantage function.

# 9.5.4 TD($\lambda$) for Advantage

The advantage function introduced in Section 9.1.3 admits the following equivalent forms:

**Proposition 9.14** The following representations hold for the advantage function:

```
$V(x,u) = Q(x,u) - h(x) \quad (9.65a)$
$$-h(x) + c(x,u) + \gamma E[h(X(k+1)) \mid \Phi(k) = (x,u)] \quad (9.65b)$
$$= c(x,u) - c_{\phi}^*(x) + \gamma E[h(X(k+1)) \mid \Phi(k) = (x,u)] - E[h(X(k+1)) \mid X(k) = x] \ \quad (9.65c)$
```

for each $x \in \mathbb{X}, u \in \mathbb{U}$, and with $c_{\phi}^*(x) = \sum_{u} c(x,u)\phi(u|x)$.

The motivation for the advantage function is in part the desire to reduce variance in the estimate of the function used in policy improvement. This brings a question, can we estimate V directly with reduced variance (as compared to estimating Q and h and then subtracting)? It might not be surprising that the answer is yes, but full justification will come until Section 10.2. We provide here a heuristic and an algorithm.

For the heuristic, we have $E[V(\\Phi(k))] = 0$ for each $k$, so it is reasonable to choose a policy class that holds for any approximation within this class. This is not difficult to arrange.

The following notation is introduced in Chapter 10:

```
$$\psi(x) = \sum_{u} \psi(x,u)\phi(u|x) \quad \quad \widetilde{\psi}(x,u) = \widetilde{\psi}(x,u) - \psi(x), \quad x \in \mathbb{X}, u \in \mathbb{U} (9.66)$
```

We search for an approximation within the following class:

```
$$\widetilde{\mathcal{H}} = \{H^{\theta} \in \mathcal{H} : \theta \in \mathbb{R}^d\}. \quad \quad (9.67)$
```

We have by definition $E|H(\\Phi(k)) \mid X(k)| = 0$ for any $H \in \widetilde{\mathcal{H}}$. With a bit more work, we learn in Section 10.2 that the best estimate of $V$ within $\widetilde{\mathcal{H}}$ coincides with the best estimate of $Q$ within the same function class.

Stability of any algorithm based on this requires linear independence of the $\Psi$. For a deterministic policy, we have $\psi(\\Phi(k)) = 0$ for every $k$, so we are out of luck! For a randomized policy, the covariance matrix $\Sigma^{\Psi}$ may be trimmed by writing $\Sigma^{\Psi} = C^TC$, where $C$ is an $m \times d$ matrix with rank $m < d$, and then we replace $\widetilde{\psi}$ with the $m$-dimensional basis:

```
$$\widetilde{\psi} = [CC^T]^{-1}C^T\.$
```

The covariance of $\widetilde{\psi}$ is the $m \times m$ identity matrix, and the function class is unchanged:

```
$$\widetilde{\mathcal{H}} ={\omega^T\widetilde{\psi} : \omega \in \mathbb{R}^m}\ = \widetilde{\mathcal{H}}.$
```