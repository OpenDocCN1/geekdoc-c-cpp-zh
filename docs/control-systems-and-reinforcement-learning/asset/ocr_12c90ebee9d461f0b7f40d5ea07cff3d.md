# 6.6 Lyapunov Functions

In the more compact operator-theoretic notation, this becomes

```
$$PV \leq V - c + \bar{\eta}. \quad (6.27)$
```

As in the deterministic case, the function $c$ is usually interpreted as a cost function on the state space. It is frequently assumed that $c(x)$ is large for "large" $x$ (recall the definition of *coercive* from Section 2.4). In this case, the Poisson inequality implies that $V(X(k))$ decreases on whenever $X(k)$ is large. This is illustrated for a deterministic system in Figure 2.5, which the set referred to in the caption is $S=\{x : c(x) \leq \bar{\eta}\}.

# 6.6.1 Average Cost

Let $\eta(x)$ denote the average cost:

```
$$\eta(x) = \lim_{n \to \infty} \frac{1}{n} \sum_{k=0}^{n-1} E[c(X(k)) \mid X(0) = x].$$
```

Using the operator-theoretic notation (6.9b) gives

```
$$\eta(x) = \lim_{n \to \infty} \frac{1}{n} \sum_{k=0}^{n-1} P^k c(x).$$
```

The dependency on $x$ and the use of "limit supremum" rather than limit in the definition of $\eta(x)$ are both required because we are not imposing any particular structure on $X$. The average cost admits a stable bound under Poisson's inequality (6.27). This is an extension of Proposition 2.3 to the Markovian setting.

**Proposition 6.4** *Suppose that (6.27) holds with $V \geq 0$ everywhere. Then the following transient bounds hold for each $n \geq 1$ and each $x \in X$:*

```
$$\frac{1}{n} \sum_{k=0}^{n-1} P^k c(x) \leq \bar{\eta} + \frac{1}{n}V(x).$$
```

Consequently, the average cost admits the bound $\eta(x) \leq \bar{\eta}$.

*Proof* Applying $P$ to both sides gives $P^2V \leq PV - Pc + P\bar{\eta}$, and since $\eta$ is constant,

```
$$P^2V \leq PV - Pc + \bar{\eta} \leq V - Pc + 2\bar{\eta}.$$
```

By repeated multiplication by $P$, we conclude that, for each $n$,

```
$$$P^nV \leq V + n\bar{\eta} - \sum_{k=0}^{n-1} P^k c.$$$
```

This gives the desired result by rearranging terms and using the assumption that $V \geq 0$. $\square$

We have seen that the average-cost bound given in Proposition 6.4 is tight for a finite space Markov chain, under the assumptions of Theorem 6.3: we can take $V = h + const.,$ where the constant is chosen large enough so that $V \geq 0$.

The beauty of Lyapunov theory is that we can obtain performance bounds without knowing your model. This is illustrated in the next example.