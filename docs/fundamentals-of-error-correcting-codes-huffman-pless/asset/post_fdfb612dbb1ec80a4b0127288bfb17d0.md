
### Exercise 225 Find the generator polynomials and the generating idempotents of the following codes from Example 4.3.4: $\mathcal{C}_1 + \mathcal{C}_6, \mathcal{C}_2 + \mathcal{C}_3, \mathcal{C}_2 + \mathcal{C}_4, \mathcal{C}_2 + \mathcal{C}_5, \mathcal{C}_3 + \mathcal{C}_4, \mathcal{C}_3 + \mathcal{C}_5, \mathcal{C}_1 \cap \mathcal{C}_6, \mathcal{C}_2 \cap \mathcal{C}_3, \mathcal{C}_2 \cap \mathcal{C}_4, \mathcal{C}_3 \cap \mathcal{C}_4, \text{and } \mathcal{C}_3 \cap \mathcal{C}_5$.

### Exercise 226 Which pairs of codes in Exercise 220 sum to the code $\mathbb{F}_q^8$? Which pairs of codes in that example have intersection $\{0\}$?

### Exercise 227 If $\mathcal{C}_i$ is a cyclic code with generator polynomial $g_i(x)$ and generating idempotent $e_i(x)$ for $1 \le i \le 3$, what are the generator polynomial and generating idempotent of $\mathcal{C}_1 + \mathcal{C}_2 + \mathcal{C}_3$?

We are now ready to describe a special set of idempotents, called primitive idempotents, that, once known, will produce all the idempotents in $\mathcal{R}_n$ and therefore all the cyclic codes. Let $x^n - 1 = f_1(x) \cdots f_s(x)$, where $f_i(x)$ is irreducible over $\mathbb{F}_q$ for $1 \le i \le s$. The $f_i(x)$ are distinct as $x^n - 1$ has distinct roots. Let $\widehat{f}_i(x) = (x^n - 1)/f_i(x)$. In the next theorem we show that the ideals $\langle \widehat{f}_i(x) \rangle$ of $\mathcal{R}_n$ are the minimal ideals of $\mathcal{R}_n$. Recall that an ideal $\mathcal{I}$ in a ring $\mathcal{R}$ is a *minimal ideal* provided there is no proper ideal between $\{0\}$ and $\mathcal{I}$. We denote the generating idempotent of $\langle \widehat{f}_i(x) \rangle$ by $\widehat{e}_i(x)$. The idempotents $\widehat{e}_1(x), \dots, \widehat{e}_s(x)$ are called the primitive idempotents of $\mathcal{R}_n$.

## Theorem 4.3.8

The following hold in $\mathcal{R}_n$.

- (i) The ideals $\langle \widehat{f}_i(x) \rangle$ for $1 \le i \le s$ are all the minimal ideals of $\mathcal{R}_n$.
- (ii) $\mathcal{R}_n$ is the vector space direct sum of $\langle \widehat{f}_i(x) \rangle$ for $1 \le i \le s$.
- (iii) If $i \neq j$, then $\widehat{e}_i(x)\widehat{e}_j(x) = 0$ in $\mathcal{R}_n$.
- (iv) $\sum_{i=1}^s \widehat{e}_i(x) = 1$ in $\mathcal{R}_n$.
- (v) The only idempotents in $\langle \widehat{f}_i(x) \rangle$ are $0$ and $\widehat{e}_i(x)$.
- (vi) If $e(x)$ is a nonzero idempotent in $\mathcal{R}_n$, then there is a subset $T$ of $\{1, 2, \dots, s\}$ such that $e(x) = \sum_{i \in T} \widehat{e}_i(x)$ and $\langle e(x) \rangle = \sum_{i \in T} \langle \widehat{f}_i(x) \rangle$.

**Proof:** Suppose that $\langle \widehat{f}_i(x) \rangle$ is not a minimal ideal of $\mathcal{R}_n$. By Corollary 4.2.5, there would be a generator polynomial $g(x)$ of a nonzero ideal properly contained in $\langle \widehat{f}_i(x) \rangle$ such that $\widehat{f}_i(x) \mid g(x)$ with $g(x) \neq \widehat{f}_i(x)$. As $f_i(x)$ is irreducible and $g(x) \mid (x^n - 1)$, this is impossible. So $\langle \widehat{f}_i(x) \rangle$ is a minimal ideal of $\mathcal{R}_n$, completing part of (i). As $\langle \widehat{f}_i(x) \rangle \mid 1 \le i \le s$ has no common irreducible factor of $x^n - 1$ and each polynomial in the set divides $x^n - 1$, $\gcd(\widehat{f}_1(x), \dots, \widehat{f}_s(x)) = 1$. Applying the Euclidean Algorithm inductively,

```
1 = \sum_{i=1}^s a_i(x) \widehat{f}_i(x) \tag{4.3}
```

for some $a_i(x) \in \mathbb{F}_q[x]$. So 1 is in the sum of the ideals $\langle \widehat{f}_i(x) \rangle$, which is itself an ideal of $\mathcal{R}_n$. In any ring, the only ideal containing the identity of the ring is the ring itself. This proves that $\mathcal{R}_n$ is the vector space sum of the ideals $\langle \widehat{f}_i(x) \rangle$. To prove it is a direct sum, we must show that $\langle \widehat{f}_i(x) \rangle \cap \sum_{j \neq i} \langle \widehat{f}_j(x) \rangle = \{0\}$ for $1 \le i \le s$. As $f_i(x) \mid \widehat{f}_j(x)$ for $j \neq i$, $f_i(x) \nmid \widehat{f}_i(x)$, and the irreducible factors of $x^n - 1$ are distinct, we conclude that $f_i(x) = \gcd(\widehat{f}_j(x) \mid 1 \le j \le s, j \neq i)$. Applying induction to the results of Theorem 4.3.7(ii) shows that $\langle f(x) \rangle = \sum_{j \neq i} \langle \widehat{f}_j(x) \rangle$. So $\langle \widehat{f}_i(x) \rangle \cap \sum_{j \neq i} \langle \widehat{f}_j(x) \rangle = \langle \widehat{f}_i(x) \rangle \cap \langle f(x) \rangle = \langle \text{lcm}(\widehat{f}_i(x), f(x)) \rangle = \langle x^n - 1 \rangle = \{0\}$ by Theorem 4.3.7 completing (ii).

Let $\mathcal{M} = \langle m(x) \rangle$ be any minimal ideal of $\mathcal{R}_n$. As

$0 \neq m(x) = m(x) \cdot 1 = \sum_{i=1}^s m(x)a(x)\widehat{f}_i(x)$

by (4.3), there is an $i$ such that $m(x)a(x)\widehat{f}_i(x) \neq 0$. Hence $\mathcal{M} \cap \langle \widehat{f}_i(x) \rangle \neq \{0\}$ as $m(x)a(x)\widehat{f}_i(x) \in \mathcal{M} \cap \langle \widehat{f}_i(x) \rangle$, and therefore $\mathcal{M} = \langle \widehat{f}_i(x) \rangle$ by minimality of $\mathcal{M}$ and $\langle \widehat{f}_i(x) \rangle$. This completes the proof of (i).

If $i \neq j$, $\widehat{e}_i(x)\widehat{e}_j(x) \in (\widehat{f}_i(x)) \cap (\widehat{f}_j(x)) = \{0\}$ by (ii), yielding (iii). By using (iii) and applying induction to Theorem 4.3.7(ii), $\sum_{i=1}^s \widehat{e}_i(x)$ is the generating idempotent of $\sum_{i=1}^s \langle \widehat{f}_i(x) \rangle = \mathcal{R}_n$ by part (ii). The generating idempotent of $\mathcal{R}_n$ is 1, verifying (iv).

If $e(x)$ is a nonzero idempotent in $\langle \widehat{f}_i(x) \rangle$, then $e(x)$ is an ideal contained in $\langle \widehat{f}_i(x) \rangle$. By minimality as $e(x)$ is nonzero, $\langle \widehat{f}_i(x) \rangle = \langle e(x) \rangle$, implying by Theorem 4.3.2 that $e(x) = \widehat{e}_i(x)$ as both are the unique unity of $\langle \widehat{f}_i(x) \rangle$. Thus (v) holds.

For (vi), note that $e(x)\widehat{e}_i(x)$ is an idempotent in $\langle \widehat{f}_i(x) \rangle$. Thus either $e(x)\widehat{e}_i(x)$ is 0 or $\widehat{e}_i(x)$ by (v). Let $T = \{i \mid e(x)\widehat{e}_i(x) \neq 0\}$. Then by (iv), $e(x) = e(x) \cdot 1 = e(x)\sum_{i=1}^s \widehat{e}_i(x) = \sum_{i=1}^s e(x)\widehat{e}_i(x) = \sum_{i \in T} e(x)\widehat{e}_i(x)$. Furthermore, $\langle e(x) \rangle = \langle \sum_{i \in T} \widehat{e}_i(x) \rangle$ by Theorem 4.3.7(ii) and induction.

We remark that the minimal ideals in this theorem are extension fields of $\mathbb{F}_q$. Theorem 4.4.19 will also characterize these minimal ideals using the trace map.

## Theorem 4.3.9

Let $\mathcal{M}$ be a minimal ideal of $\mathcal{R}_n$. Then $\mathcal{M}$ is an extension field of $\mathbb{F}_q$.

Proof: We only need to show that every nonzero element in $\mathcal{M}$ has a multiplicative inverse in $\mathcal{M}$. Let $a(x) \in \mathcal{M}$ be nonzero. Then $a(x)$ is a nonzero ideal of $\mathcal{R}_n$ contained in $\mathcal{M}$, and hence $\langle a(x) \rangle = \mathcal{M}$. So if $e(x)$ is the unity of $\mathcal{M}$, there is an element $b(x)$ in $\mathcal{R}_n$ with $a(x)b(x) = e(x)$. Now $c(x) = b(x)e(x) \in \mathcal{M}$ as $e(x) \in \mathcal{M}$. Hence $a(x)c(x) = e(x)^2 = e(x)$. $\square$

### Exercise 228 What fields arise as the minimal ideals in $\mathcal{R}_7$ and $\mathcal{R}_{15}$ over $\mathbb{F}_2$? $\blacklozenge$

Theorem 4.3.8 shows that every idempotent is a sum of primitive idempotents and that cyclic codes are sums of minimal cyclic codes. An interesting consequence, found in [280], of this characterization of cyclic codes is that the dimension of a sum of cyclic codes satisfies the same formula as that of the inclusion-exclusion principle, a fact that fails in general.

## Theorem 4.3.10

Let $C_i$ be a cyclic code of length $n$ over $\mathbb{F}_q$ for $1 \le i \le a$. Then:

$\dim(C_1 + C_2 + \cdots + C_a) = \sum_i \dim(C_i) - \sum_{i<j} \dim(C_i \cap C_j)$
$+ \sum_{i<j<k} \dim(C_i \cap C_j \cap C_k) - \cdots$
$+ (-1)^{a-1} \dim(C_1 \cap C_2 \cap \cdots \cap C_a).$

Proof: Let $\{\widehat{e}_i(x) \mid 1 \le i \le s\}$ be the primitive idempotents of $\mathcal{R}_n$. By Theorem 4.3.8, the minimal ideals of $\mathcal{R}_n$ are $\langle \widehat{e}_i(x) \rangle$. Fix a basis $B_i$ of $\langle \widehat{e}_i(x) \rangle$ for $1 \le i \le s$. Also by
