# 10.10 Notes

# 10.10 Fisher Information

The interpretation of (10.54) as Fisher information is not easily.
The term arises in the theory of parameter estimation as in Borkar's thesis [61, 62]: In the context of this chapter, the estimation problem is the same as before. The input is chosen according to $\phi^	heta$ for some $	heta \in \mathbb{R}^d$. Given samples $\{\Phi(k) : 0 \le k \le n\}$, the maximum likelihood estimate $	heta_n^	heta$ is a solution to

```
$0 = \nabla_	heta \log \left( \prod_{k=0}^{n-1} T_	heta(\Phi(k), \Phi(k+1)) \right) \big|_{\theta=	heta_n^	heta} = \sum_{k=1}^n \Lambda^	heta(\Phi(k)) \big|_{\theta=	heta_n^	heta}$.
```

In this context, the Fisher information is the normalized covariance of this statistic, evaluated at $	heta = 	heta^	heta$:

```
$F_n(\theta^	heta) = \frac{1}{n} \text{Cov} \left( \sum_{k=1}^n \Lambda_{(k)}^	heta \right).$.
```

Due to the martingale difference property established Lemma 10.20,

```
$\lim_{n \to \infty} F_n(\theta^	heta) = \frac{1}{n} \text{Cov}(\Lambda_{(k)}^	heta) = F(\theta^	heta)$,
```

with the right-hand side defined in (10.54).

The matrix $F_n(\theta^	heta)$ is a measure of the sensitivity of the first $n$ observations to the parameter $	heta^	heta$, and from this limit we can justify the interpretation of $F(\theta^	heta)$ as the sensitivity with respect to the entire history of observations. This is an elegant conclusion for applications to parameter estimation, but doesn't explain why the inverse of $F(\theta_n)$ is a good gain for applications to actor-critic algorithms.