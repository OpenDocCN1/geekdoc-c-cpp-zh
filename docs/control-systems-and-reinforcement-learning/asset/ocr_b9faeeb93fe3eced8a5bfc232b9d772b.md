# 10.4 Average Cost and Every Other Criterion

# Finite-Horizon

Let $N \ge 1$ and $z^* \in \mathbb{Z}$ be given, consider the finite horizon criterion

> $$\Gamma = E\left[ \sum_{k=0}^{\mathcal{N}^\star_{\mathcal{N}}} \gamma^k c(\Phi(k)) \right], \quad \Phi(0) \sim \mu,$ (10.27)$

$$\mathcal{N}^\star = \min\{k \ge 1 : \Phi(k) = z^*\}; \mathcal{N}^\star_{\mathcal{N}} = \min(N, \mathcal{N}^\star),$ and $\gamma > 0$ is arbitrary. This is the shortest shortest problem with $\mathcal{N} = \infty$ and $\gamma = 1$.

To construct a Markov chain $\Psi$ for which (10.27) is proportional to average cost we require a different construction. We define $\Psi$ as a pair process $\Psi(k) = (\Phi(k), k)$, where the setting $t$ is defined to be deterministic and periodic: $t = k \pmod N$. The regeneration times are also deterministic: $\mathcal{N}_n = nN$ for $n \ge 1$, and the construction is defined such that the sequence $(\Phi(\mathcal{N}_n) : n \ge 1)$ is i.i.d. with marginal $\mu$.

We borrow from the discounted cost setting with $\Psi$: The state space $Z$ is enlarged to include a graveyard state denoted $\blacktriangle$. Here the state space for $\Psi$ is $[Z \cup \blacktriangle] \times \{0, \dots, N-1\}$. The dynamics on each interval $\mathcal{N}_n < k < \mathcal{N}_{n+1}$ are defined as follows:

+   (i) $\Phi(k) = \blacktriangle \ |\Phi(k-1) = z^*|$; $\Phi(k) = \blacktriangle \ |\Phi(k-1) = \blacktriangle| = 1$.
(ii) $\Phi(k) = z' \ |\Phi(k-1) = z| = T(z, z')$ for $z, z' \in \mathbb{Z}$, where $z \neq z^*$.

As in the discounted case, there is a simple interpretation that leads to simulation or experimental design: for $n$, initialize $\Phi(\mathcal{N}_n) \sim \mu$, independent of samples of the state process according to the natural dynamics of $\Phi(k) : k < \mathcal{N}_{n+1}$ for $\mathcal{N}_n < k < \mathcal{N}_{n+1}$, stopping the experiment if $z^*$ is reached during this interval.

The cost function is defined by $c(\blacktriangle) \doteq 0$, and $c(z) \doteq \gamma^t c(z)$ for $z \in \mathbb{Z}$ and $t \in \{0, \dots, N-1\}$.

An analog of Proposition 10.12 is obtained through this construction:

**Proposition 10.13** The partial sums $\{S_n\}$ in (10.24) are i.i.d. with common mean $\Gamma$, now defined in (10.27). Consequently, the average cost is given by

> $$\lim_{N \to \infty} \frac{1}{N} E\left[ \sum_{k=1}^N c(\Phi(k)) \right] = \Gamma.$

Proposition 10.13 also applies to the truncated discounted-cost criterion:

> $$\Gamma = E\left[ \sum_{k=1}^{\mathcal{N}^\star} \gamma^k c(\Phi(k)) \right], \quad \Phi(0) \sim \mu.$

This may be preferred to the infinite horizon objective (10.25), since the use of deterministic regeneration cycles will lead to lower variance.

Both regeneration and relative DP equations are used next to construct algorithms designed to estimate the solution of Poisson’s equation (9.56). Regeneration motivates the representation $H_3$ given in (10.17), which is the unique solution $H_3(z^*) = 0$.

# 10.4.2 Average-Cost Algorithms