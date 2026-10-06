# Value Function Approximations

**Proposition 5.4** *Suppose that $R_N$ has rank less than $d$. Then there is a nonzero vector $v \in \mathbb{R}^d$ with the following holding, for each $0 \le k \le N-1$:*

+   (i) For any $\theta \in \mathbb{R}^d$ and $r \in \mathbb{R}$,

```
$\mathcal{D}_{k+1}(Q^{\theta})=\mathcal{D}_{k+1}(Q^{\theta'}), \quad \text{with } \theta'=\theta+rv$
```

+   (ii) For the on-policy implementation,

```
$v^T \psi(x(0), u(0)) = v^T \psi(x(k), u(k)).$
```

Hence this falls into the "redundant" category discussed in Section 5.1.5.

Proof *If $R_N$ does not have full rank, then it follows that there is a nonzero vector $v$ satisfying $v^T R_N v = 0$. By definition,

```
$0 = v^T R_N v = \frac{1}{N} \sum_{k=0}^{N-1} (v^T \Upsilon_{k+1})^2$.
```

That is, $v^T \Upsilon_k = 0$ for every observed sample, which means

```
$0 = v^T \psi(x(k), u(k)) - v^T \psi(x(k+1), \phi(x(k+1))), \quad 0 \le k \le N-1. \quad (5.35)
```

Part (i) follows from (5.35) and the definition (5.28a): for any scalar $r$, with $\theta' = \theta + rv$

```
$\mathcal{D}_{k+1}(Q^{\theta}) = -Q^{\theta}(x(k), u(k)) + c(x(k), u(k)) + Q^{\theta}(x(k+1), \phi(x(k+1)))\n= c(x(k), u(k)) + [\theta + rv]^T [-\psi(x(k), u(k)) + \psi(x(k+1), \phi(x(k+1)))]\n= c(x(k), u(k)) + \theta^T [-\psi(x(k), u(k)) + \psi(x(k+1), \phi(x(k+1)))] = \mathcal{D}_{k+1}(Q^{\theta}).$
```

If $u(k) = \phi(x)$ for all $k$, then (5.35) becomes

```
$v^T \psi(x(k), u(k)) = v^T \psi(x(k+1), u(k)), \quad 0 \le k \le N-1$,
```

which implies (ii).

On-policy algorithms are preferred because of ease of analysis (mainly in the context of stochastic control). To ensure sufficient exploration, it is best to go with the restart option introduced in (2.55):

# **Least Squares Temporal Difference Learning (with Restart)**

Assumed given are $d \times d$ matrix $W > 0$, integers $N$ and $M$, and observed samples

```
${u'(k), x'(k) : 0 \le i \le N, 1 \le i \le M\}$ (5.36a)
```

with user-defined initial conditions $\{x^0(i) : 1 \le i \le M\}$, and with input $u'(k) = \phi(x(k), \xi'(k)),$.

The approximation of the Q-function $Q^{\theta^{\text{STD}}} = \psi^T \theta^{\text{STD}}}$ is obtained, in which the optimal parameter is determined by the following steps: