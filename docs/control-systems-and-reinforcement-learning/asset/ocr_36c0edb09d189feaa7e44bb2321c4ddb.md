# Setting the Stage, Return of the Actors

$||H||_{\alpha, \omega}^2 = \mathbb{E}[H(\Phi(n))^2 w(\Phi(n))].$ (10.9)

$H \in L_2(\alpha, w)$ if this is finite (a vacuous assumption when finite, as assumed in the theoretical development). The inner product is redefined consistently:

```
$$\langle G, H\rangle_{\alpha, \omega} = \mathbb{E}[G(\Phi(n))H(\Phi(n))w(\Phi(n))], \quad G, H \in L_2(\alpha, w).$
```

The adaptation of (6.49) to the current setting is minimization of the weighted mean-square error:

```
$||H^0 - Q||_{\alpha, \omega}^2 = \mathbb{E}[(H^0(\Phi(n)))^2 w(\Phi(n))].$ (10.10)
```

The Galerkin approach to on-policy $(\lambda$-learning) is modified as follows:

```
$0 = \mathbb{E}[-H^0(\Phi(n)) + \zeta_n + \gamma H^0(\Phi(n+1))w(\Phi(n))\zeta_n],$ (10.11)
```

with $\zeta_n = \sum_{k=0}^{\infty} \lambda^k \psi^k(\Phi(n-k))$, and with $\psi$ stationary on $\mathbb{Z}$.

The development of Section 10.1 carries over to the new vector space $L_2(\alpha, w)$, beginning with the following:

**Proposition 10.4** The following hold for any function $G \in L_2(\alpha, w)$, with the following notation:

```
$$\psi_i^G = \langle\psi_i, G\rangle_{\alpha, w} \quad 1 \le i \le d,$$$\n$$R_{i,j}^G = \langle\psi_i, \psi_j\rangle_{\alpha, w} \quad 1 \le i, j \le d.$$ (10.12)
```

+   (i) The projection $G$ exists, with $\bar{G} = \theta^{\*} \psi$, with $\theta^{\*} \in \mathbb{R}^d$ any solution to the linear equation $R\theta^{\*} = \psi^G$.

+   (ii) Suppose $\{\psi_i\}$ are linearly independent in $L_2(\alpha, w)$: $|\theta^{\*} \psi||_{\alpha, w} = 0$ only when $\theta = 0$. Then $\theta^{\*} = |R|^{-1}\psi^G$ is unique.

When applied to minimize the objective (10.10), we still have $Q = T_{\gamma}c$, and hence

```
$$\psi_i^Q = \langle\psi_i, T_{\gamma}c\rangle_{\alpha, w} \quad 1 \le i \le d.$$$
```

However, the definition of the adjoint depends on the choice of norm:

**Lemma 10.5** We have for all $g, h \in L_2(\alpha, w)$,

```
$$\langle T_{\gamma}h, g\rangle_{\alpha, w} = \sum_{k=0}^{\infty} \gamma^k \mathbb{E}[w(\Phi(0))h(\Phi(-k))g(\Phi(k))]$$\n$$= = \sum_{k=0}^{\infty} \gamma^k \mathbb{E}[w(\Phi(-k))h(\Phi(-k))g(\Phi(k))].$$
```

Consequently, the adjoint of $T_{\gamma}$ in $L_2(\alpha, w)$ admits the following representation:

```
$T_{\gamma}^T h(z) = \frac{1}{w(z)} \sum_{k=0}^{\infty} \gamma^k \mathbb{E}[w(\Phi(-k))h(\Phi(-k)) \| \Phi(0) = z], \quad z \in \mathbb{Z}.$$
```

This motivates a new algorithm and consistency result: