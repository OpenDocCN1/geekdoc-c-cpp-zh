From (6.1.5) the result follows. The solution is

$$q = \sum_{n=1}^{\infty} \alpha^{n-1} \Phi^{n-1} \theta.$$

The numbers $q_{ij}$ have a probabilistic interpretation. Indeed $q_{ij}$ represents the average time to reach $j$ (or to come back to $i$ if $j=i$) starting from state $i$. More precisely we can write

$$q_{ij} = \sum_{n=1}^{\infty} n f^{(n)}(i, j),$$

where $f^{(n)}(i, j)$ is the probability to reach $j$ from $i$ in exactly $n$ steps. We have the recurrence formulas

$$f^{(n)}(i, j) = \sum_{k \neq j} \varpi(i, k) f^{(n-1)}(k, j), n \ge 2$$ $$f^{(1)}(i, j) = \varpi(i, j).$$

The key estimate is given in the following

**Lemma 6.2.** The solution $u_\alpha$ of equation (6.1.8) satisfies the estimate

$$(6.1.11) \quad u_\alpha(i) - u_\alpha(j) \le ||I|| q_{ij}.$$

PROOF. Consider the increasing iteration

$$u_\alpha^{k+1}(i) = \inf_{v \in U} [l(i, v) + \alpha \Phi^v u_\alpha^k(i)],$$

starting with $u_\alpha^0(i) = 0$. We shall check

$$u_\alpha^k(i) - u_\alpha^0(j) \le ||I|| q_{ij}, \forall k.$$

This inequality is clearly true for $k=0$. Assume it is true for $k$, then noting that

$$u_\alpha^{k+1}(i) \le ||I|| + \alpha \sum_l \varpi(i, l) u_\alpha^k(l),$$

and since all quantities are positive

$$u_\alpha^{k+1}(i) \le ||I|| + \sum_l \varpi(i, l) u_\alpha^k(l).$$

Using the recurrence we get

$$u_\alpha^{k+1}(i) \le ||I|| + \sum_{l \neq j} \varpi(i, l) u_\alpha^k(j) + ||I|| q_{ij} + \varpi(i, j) u_\alpha^k(j)$$ $$= ||I|| + u_\alpha^k(j) + ||I|| (q_{ij} - 1)$$ $$= u_\alpha^k(j) + ||I|| q_{ij}.$$

and since the sequence is increasing the property follows.

Applying the Lemma to the index $j$ corresponding to the minimum of $u_\alpha(j)$ and majorizing we obtain also

$$u_\alpha(i) - \min_j u_\alpha(j) \le ||I|| \max_{ij} q_{ij}.$$

With this estimate the proof can be carried over in the same way as in the proof of Theorem 6.1.