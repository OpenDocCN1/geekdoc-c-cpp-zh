# 6.2 Simple Examples

The state process $x$ is also Markovian: Given the full history of observations $\{x(i) : i \le k\}$, we can still predict $x(k+1)$ with exact accuracy, based only on knowledge of $x(k)$.

The transition kernel is easily described: For any $x \in X = \mathbb{R}^n$ and set $S \subset X$, we have

```
$P(x,S) = P\{X(1) \in S | X(0) = x\} = P\{Fx + N(1) \in S\$
```

If particular $N(1)$ is Gaussian $N(0, \Sigma_N)$, then $P(x, \cdot)$ is a Gaussian distribution, with mean $Fx$ rather than zero. If at some time $r \ge 0$ we observe $X(r) = x$, then for each $j \ge 0$

```
$X(r+j) = F^jx + \sum_{i=1}^j F^{j-i}N(r+i)$.
```

That is, conditioned on $X(r) = x$, the random vector $X(r+j)$ has a Gaussian distribution with mean $F^jx$ and covariance

```
$\Sigma_{X_j} = \sum_{i=1}^j (F^{j-i})^\top \Sigma_N F^{j-i}$.
```

If $\Sigma_{X_j}$ is full rank (so its inverse exists), $P^j$ admits a density:

```
$p_j(x,y) = \frac{1}{\sqrt{(2\pi)^n \det(\Sigma_{X_j})}} \exp(-\frac{1}{2}(y-F^jx)^\top \Sigma_{X_j}^{-1}(y-F^jx))$,
```

```
$P^j(x,S) = \int_S p_j(x,y)dy$,
```

The $j$-step transition kernel is defined in (6.5).

From this, we obtain our first ergodic theorem:

**Proposition 6.1** Suppose that the eigenvalues of $F$ lie in the open unit disk in $\mathbb{C}$, and that $N$ is i.i.d., with Gaussian marginal $N(0,\Sigma_N)$. Consider any factorization, $\Sigma_N = GG^	op$, with $G$ an $n \times m$ matrix for some $m \ge 1$, and suppose that the rank condition holds:

```
$rank(C) = n$, where $C = [G | FG | \dots | F^{n-1}G]$. (6.13)
```

Then the following conclusions hold:

+   (i) The steady-state covariance $\Sigma_{X_\infty}$ has rank $n$, where

```
$\Sigma_{X_\infty} = \lim_{j\to\infty} \sum_{k=0}^infty (F^k)^\top \Sigma_N F^k$.
```

+   (ii) The density $p_k$ exists for $k \ge n$, and converges as $k \to \infty$:

```
$\lim_{k\to\infty} p_k(x,y) = p\infty(y) = \frac{1}{\sqrt{(2\pi)^n \det(\Sigma_{X_\infty})}} \exp(-\frac{1}{2}y^\top \Sigma_{X_\infty}^{-1} y)$.
```