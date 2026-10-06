# Markov Chains

Proof  The simplest of the three is (i),

```
$Ph_1 = \sum_{k=0}^{\infty} P^k \hat{c}$$
```

where we used $P \cdot P^k = P^{k+1}$. The right-hand side is equal to $h_1 - \hat{c}$.

The remainder of the proof is a “roadmap.” For the full details, we see the appendix of [254].

For (ii) and (iii), recall that the invariant measure $\pi$ exists and is unique, due to Theorem 6.2. Poisson's equation with invariance of $\pi$ implies:

```
$$\pi(h) = \sum_{x} \pi(x)h(x) = \sum_{x} \sum_{y} \pi(x)P(x,y)h(y)$
$$\eta = \sum_{x} \pi(x)\{h(x)-c(x)\} = \pi(h) - \pi(c) + \eta$$
```

Hence $\eta = \pi(c)$.

The proof that $h_2$ solves Poisson's equation follows similar to Proposition 3.5. A full proof can be found in [257] or the appendix of [254]. This solution is related to $h_1\hat{c}$. We have $P^k\hat{c} = \tilde{P}^k\hat{c}$ for any $k$, where $\tilde{P} = P-1 \odot \pi$ was introduced in (6.19). Hence $h_1 = G_1,\pi\hat{c}$.

The third representation can be reduced to the second, starting with

```
$h_3(x) = \sum_{k=0}^{\infty} E_x[\mathbb{1}_{\{\tau > k}]}\hat{c}(X(k))$$
```

It can be shown that $h_2$ is in the special case $s(x) = \mathbb{1}_{\cdot}(x)$, and $v(y) = P^*(x,y).
We come to (iv): If $C+Pg = g+\beta$ and $C+Ph = h+\eta$, then let $\Delta = h-g$, giving

Using invariance of $\pi$ gives

```
$$\pi(\Delta) = \sum_{x} \pi(x)\Delta(x) = \sum_{x} \sum_{y} \pi(x)P(x,y)\Delta(y) = \sum_{x} \pi(x)\Delta(x) + \eta-\eta = \pi(\Delta)+\eta-\eta.$
```

This gives $\eta = \beta$, and also the following eigenvector equation:

```
$P\Delta = \Delta.$
```

Under the assumptions of the theorem, it follows that $\Delta(x)$ does not depend on $x$.

# 6.6 Lyapunov Functions

Much of the Lyapunov stability theory for dynamical systems can be adapted to the Markovian setting. For an irreducible Markov chain in a finite state space, where the term “stability” may not be meaningful, Lyapunov functions are useful as means to obtain performance bounds (generalizing the Comparison Theorem in Proposition 2.3).

Poisson's inequality for the Markovian model is the extension of (2.31): For a function $V: X \to \mathbb{R}_+$, a function $c: X \to \mathbb{R}_+$, and a constant $\bar{\gamma} < \infty$.

```
$E[V(X(k+1)) | X(k)=x] \leq V(x)-c(x)+\bar{\gamma}, \quad x \in X.$
```