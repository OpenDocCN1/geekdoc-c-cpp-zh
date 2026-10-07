# Data Clustering: Algorithms and Applications

### Procedure 1: The computation of $F$,$
1: Let $n^* = \max n_i$.
2: Sort the class sizes so that $n_{[1]} \leq \dots \leq n_{[K^*]}$.
3: Let $a_j = 0$, for $j = 1, 2, \dots, K^*$.
4: for $j=1: K'
5: if $n^* \leq n_{[j]}$, $a_j = n^*$, break.
6: else $a_j = n_{[j]}$, $n^* \leftarrow n^* - n_{[j]}$.
7: $F_- = (2/n)\sum_{i=1}^K a_i / (1 + \max n_i/n^*)$.

PROOF. It is easy to show

```
$F = \sum_{j=1}^n \max \frac{n_{ij}}{n_i + n_j} \geq 2 \max_{j} \frac{n_{ij}}{n_i/n_j + 1} \quad (23.4)$
```

Consider an optimization problem as follows:

```
$\min_{x_{ij}} \frac{x_{ij}}{n_i/n_j + 1}$
s.t. $\sum_{j} x_{ij} = n_i; x_{ij} \leq n_j; \forall j, x_{ij} \in \mathbb{Z}_+$
```

For this optimization problem, need to have the minimum objective value, as many objects as be assigned to the cluster with minimum $n_i/n_j + 1$, or equivalently, with maximum $n_j$. Let $n_{[0]} \leq n_{[1]} \leq \dots \leq n_{[K']}$ where the virtual $n_{[0]} = 0$, and assume $\sum_{j=0}^{l-1} n_{[j]} < n_{[l]} \leq \sum_{j=0}^{l} n_{[j]}$, $l \in \{0, 1, \dots, K'-1\}$. The optimal solution is given

```
$x_{ij} = \begin{cases} n_{[j]}, & 1 \leq j \leq l \ n^* - \sum_{k=1}^l n_{[k]}, & j = l+1 \ 0, & l+1 < j \leq K' \end{cases}$
```

Therefore, according to (23.4), $F \geq \frac{2}{n} \max_i \sum_{j=1}^n \frac{n_{ij}}{n_i/n_j + 1}$. Let $F_i = \frac{2}{n} \sum_{j=1}^n \frac{n_{ij}}{n_i/n_j + 1}$. Denote '$[x_{ij}/n_i]$' by '$[y_{ij}/n_i]$', and '$[1/(n_i/n_j+1)]$' by '$[p_{ij}]$', when $\$[p_{ij}]$", then $F_i = \sum_{j=1}^n y_{ij}p_{ij}$. Next, it remains to show

```
$\arg max F_- = \arg max n_i$.
```

Assume $n_i \leq n_l$, and for some $l$, $\sum_{j=0}^{l-1} n_{[j]} < n_i \leq \sum_{j=0}^l n_{[j]}$, $l \in \{0, \dots, K'-1\}$. This implies that

```
$Y_{ij} = \begin{cases} \geq p_{[ij]}, & 1 \leq j \leq l \ \leq p_{[ij]}, & l+1 < j \leq K' \end{cases}$$
```

Since $F_i = \sum_{j=1}^n y_{ij}p_{ij} = \sum_{j=1}^n p_{ij}p_{ij} = 1$ and $\Rightarrow F_i \uparrow p_{[ij]}$, thus $F_i = \sum_{j=1}^n p_{ij}p_{ij} \leq \sum_{j=1}^n p_{[ij]}p_{[ij]} =$. Furthermore, according to the definition of $p_{[ij]}$, $p_{ij} \leq p_{[ij]}, \forall j \in \{1, \dots, K'\}$.

```
$F_i = \frac{2}{n} \sum_{j=1}^n p_{ij}p_{ij} \geq \frac{2}{n} \sum_{j=1}^{K'} p_{[ij]}p_{[ij]} \geq \frac{2}{n} \sum_{j=1}^{K'} p_{[ij]}p'_ij = F'_i$
```

which implies that $n_i \leq n_l$, is the sufficient condition for $F_i \leq F_l'$.$. By Procedure 1, $F_- = \max F_i$, which finally leads to $F \geq F_-$.