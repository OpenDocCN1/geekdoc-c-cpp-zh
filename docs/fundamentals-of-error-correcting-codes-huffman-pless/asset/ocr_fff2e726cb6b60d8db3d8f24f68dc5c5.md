**Theorem 3.3.2** The elements of $\mathbb{F}_q$ are precisely the roots of $x^q - x$.

In Theorem 3.1.1(v) we claim that the field with $q = p^m$ elements is unique. Theorem 3.3.2 shows that a field with $q$ elements is the smallest field containing $\mathbb{F}_p$ and all the roots of $x^q - x$. Such a field is termed a splitting field of the polynomial $x^q - x$ over $\mathbb{F}_p$, that is, the smallest extension field of $\mathbb{F}_p$ containing all the roots of the polynomial. In general splitting fields of a fixed polynomial over a given field are isomorphic; by carefully defining a map between the roots of the polynomial in one field and the roots in the other, the map can be shown to be an isomorphism of the splitting fields.

**Exercise 161** Using the table for $\mathbb{F}_4$ in Example 1.1.3, verify that all the elements of $\mathbb{F}_4$ are roots of $x^4 - x = 0$.

In analyzing the field structure, it will be useful to know the number of primitive elements in $\mathbb{F}_q$, and how to find them all once one primitive element has been found. Since $\mathbb{F}_q^*$ is cyclic, we recall a few facts about finite cyclic groups. In any finite cyclic group $\mathcal{G}$ of order $n$ with generator $g$, the generators of $\mathcal{G}$ are precisely the elements $g^i$ where $\text{gcd}(i, n) = 1$. We let $\phi(n)$ be the number of integers $i$ with $1 \le i \le n$ such that $\text{gcd}(i, n) = 1$; $\phi$ is called the *Euler totient* or the *Euler* $\phi$-*function*. So there are $\phi(n)$ generators of $\mathcal{G}$. The order of an element $\alpha \in \mathcal{G}$ is the smallest positive integer $i$ such that $\alpha^i = 1$. An element of $\mathcal{G}$ has order $d$ if and only if $d \mid n$. Furthermore $g^i$ has order $d = n/\text{gcd}(i, n)$, and there are $\phi(d)$ elements of order $d$. When speaking of field elements $\alpha \in \mathbb{F}_q^*$, the order of $\alpha$ is its order in the multiplicative group $\mathbb{F}_q^*$. In particular, primitive elements of $\mathbb{F}_q$ are those of order $q - 1$. The next theorem follows from this discussion.

**Theorem 3.3.3** Let $\gamma$ be a primitive element of $\mathbb{F}_q$.

+   (i) There are $\phi(q-1)$ primitive elements in $\mathbb{F}_q$; these are the elements $\gamma^i$ where $\text{gcd}(i, q-1) = 1$.
+   (ii) For any $d$ where $d \mid (q-1)$, there are $\phi(d)$ elements in $\mathbb{F}_q$ of order $d$; these are the elements $\gamma^{(q-1)i/d}$ where $\text{gcd}(i, d) = 1$.

An element $\xi \in \mathbb{F}_q$ is an $n$th root of unity provided $\xi^n = 1$, and is a *primitive nth root of unity* if in addition $\xi^k \neq 1$ for $0 < k < n$. A primitive element $\gamma$ of $\mathbb{F}_q$ is therefore a primitive $(q-1)$st root of unity. It follows from Theorem 3.3.1 that the field $\mathbb{F}_q$ contains a primitive $n$th root of unity if and only if $n \mid (q-1)$, in which case $\gamma^{(q-1)/n}$ is a primitive $n$th root of unity.

**Exercise 162** (a) Find a primitive element $\gamma$ in the field $\mathbb{F}_q$ given below. (b) Then write every nonzero element in $\mathbb{F}_q$ as a power of $\gamma$. (c) What is the order of each element and which are primitive? (d) Verify that there are precisely $\phi(d)$ elements of order $d$ for every $d \mid (q-1)$.

+   (i) $\mathbb{F}_5$.
+   (ii) $\mathbb{F}_7$.
+   (iii) $\mathbb{F}_{13}$.