# 7.8 Bandits

in which $D_k$ is a diagonal matrix with entries

```
$D_k(i,i) = \frac{1}{\sigma_{W_i}^2}n_i(k),
```

where $\sigma_{W_i}^2$ is the variance of the Gaussian random variable $W_i(k)$ (independent of $k$). Consequently, $\Sigma_k 	o 0$ as $k 	o \infty$ if and only if each arm is pulled infinitely often.

Proof Part (i) follows from the first equation in (7.50), and from the second we obtain the second update equation

```
$\Sigma_k = \Sigma_{k-1} - \gamma^{-1}VV^	op, \quad V = \Sigma_{k-1}H_k^	op, \quad \gamma = H_k\Sigma_{k-1}H_k^	op + H_k\Sigma_W H_k$,
```

The Matrix Inversion Lemma gives

```
$\Sigma_k^{-1} = \Sigma_{k-1}^{-1} + \Sigma_{k-1}^{-1}V[\gamma - V^	op\Sigma_{k-1}^{-1}V]^	op\Sigma_{k-1}^{-1},
```

which simplifies dramatically when we insert the definition of $V$ and $y$:

```
$\Sigma_k^{-1} = \Sigma_{k-1}^{-1} + \frac{1}{H_k\Sigma_W H_k^	op}H_k^	op H_k$.
```

The second term is a matrix with all entries zero, except a term on the diagonal. Specifically, for all $i,j$,

```
$\Sigma_k^{-1}(i,j) = \begin{cases} \Sigma_0^{-1}(i,j) & i \neq j \ \Sigma_{k-1}^{-1}(i,i) + \frac{1}{\sigma_{W_i}^2}\mathbb{1}\{U(k)=i\} & i = j' \end{cases}$
```

which establishes (ii).

The Proposition implies that to compute the conditional covariance, it is sufficient to keep track of the number of times we have pulled each arm.

```
$\lim_{k\to\infty} \Sigma_k^{-1}(i,i) = \Sigma_0^{-1}(i,i) + \frac{1}{\sigma_{W_i}^2}\sum_{k=1}^{\\infty}\mathbb{1}\{U(k)=i\}$.
```

Hence a logarithmic boost over $n_i(k)$ does not prevent convergence of $\Sigma_k(i,i)$ to zero.

# 7.8 Naive Optimism Can Be Successful

Bandit theory is theoretically posed in a far more general than Gaussian bandits, and algorithm design is often based on a frequentist setting. That, algorithms are based on empirical priors, and there is no use for a prior distribution over the rewards.

A model is required for analysis. A typical choice is a parameterized model in which the vector-valued process $\mathbf{Z}$ is i.i.d.,

```
$Z_u(k) \sim f(\cdot;\theta_u)$,
```

in which $f(\cdot;\theta_u)$ is a density on $\mathbb{R}$ for $u \in \mathbb{U}$, with parameter $	heta \in \mathbb{R}^K$. Hence for $u_u$,

```
$ar{	au}_u = E[Z_u(k)] = \int f(r;\theta_u)dr$.
```