Two elements of $\mathbb{F}_{q^r}$ which have the same minimal polynomial in $\mathbb{F}_q[x]$ are called conjugate over $\mathbb{F}_q$. It will be important to find all the conjugates of $\alpha \in \mathbb{F}_{q^r}$, that is, all the roots of $M_d(x)$. We know by Theorem 3.7.3(ii) that the roots of $M_d(x)$ are distinct and lie in $\mathbb{F}_{q^r}$. We can find these roots with the assistance of the following theorem.

# **Theorem 3.7.4** Let $f(x)$ be a polynomial in $\mathbb{F}_q[x]$ and let $\alpha$ be a root of $f(x)$ in some extension field $\mathbb{F}_{q^r}$. Then:

+   (i) $f(\alpha^q) = f(\alpha)^q$, and
+   (ii) $\alpha^q$ is also a root of $f(x)$ in $\mathbb{F}_q$.

**Proof:** Let $f(x) = \sum_{i=0}^m a_i x^i$. Since $q = p^m$, where $p$ is the characteristic of $\mathbb{F}_q$, $f(x)^q = \sum_{i=0}^m a_i^q x^{iq}$ by applying Exercise 152 repeatedly. However, $a_i^q = a_i$, because $a_i \in \mathbb{F}_q$ and elements of $\mathbb{F}_q$ are roots of $x^q - x$ by Theorem 3.3.2. Thus (i) holds. In particular, $f(\alpha^q) = f(\alpha)^q = 0$, implying (ii).

Repeatedly applying this theorem we see that $\alpha, \alpha^q, \alpha^{q^2}, \dots$ are all roots of $M_d(x)$. Where does this sequence stop? It will stop after $r$ terms, where $\alpha^{q^r} = \alpha$. Suppose now that $\gamma$ is a primitive element of $\mathbb{F}_{q^r}$. Then $\alpha = \gamma^t$ for some $s$. Hence $\alpha^{q^r} = \alpha$ if and only if $t q^{r-1} \equiv 1$. By Theorem 3.3.1(ii), $sq^r \equiv s \pmod{q^r - 1}$. Based on this, we define the $q$-cyclotomic coset of $s$ modulo $q^r - 1$ to be the set

$C_s = \{s, sq, \dots, sq^{r-1}\} \pmod{q^r - 1}$,

where $r$ is the smallest positive integer such that $sq^r \equiv s \pmod{q^r - 1}$. The sets $C_s$ partition the set $\{0, 1, 2, \dots, q^r - 2\}$ of integers into disjoint sets. When listing the cyclotomic cosets, it is usual to list $C_s$ only once, where $s$ is the smallest element of the coset.

# **Example 3.7.5** The 2-cyclotomic cosets modulo 15 are $C_0 = \{0\}, C_1 = \{1, 2, 4, 8\}, C_3 = \{3, 6, 12, 9\}, C_5 = \{5, 10\}, \text{and } C_7 = \{7, 14, 13, 11\}$.

# **Exercise 184** Compute the 2-cyclotomic cosets modulo:

+   (a) 7,
+   (b) 31,
+   (c) 63.

# **Exercise 185** Compute the 3-cyclotomic cosets modulo:

+   (a) 8,
+   (b) 26.

# **Exercise 186** Compute the 4-cyclotomic cosets modulo:

+   (a) 15,
+   (b) 63.

Compare your answers to those of Example 3.7.5 and Exercise 184.

We now know that the roots of $M_d(x) = M_{q^r}(x)$ include $\{y^i \mid i \in C_s\}$. In fact these are all the roots. So if we know the size of $C_s$, we know the degree of $M_{q^r}(x)$, as these are the same.