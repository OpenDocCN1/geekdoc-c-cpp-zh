# ## 4.1 Factoring $x^n - 1$

We are interested in finding the irreducible factors of $x^n - 1$ over $\mathbb{F}_q$. Two possibilities arise: either $x^n - 1$ has repeated irreducible factors or it does not. The study of cyclic codes has primarily focused on the latter case. By Exercise 201, $x^n - 1$ has no repeated factors if and only if $q$ and $n$ are relatively prime, an assumption we make throughout this chapter.

+   **Exercise 201** For $f(x) = a_0 + a_1 x + \cdots + a_n x^n \in \mathbb{F}_q[x]$, define the formal derivative of $f(x)$ to be the polynomial $f'(x) = a_1 + 2a_2 x + 3a_3 x^2 + \cdots + n a_n x^{n-1} \in \mathbb{F}_q[x]$. From this definition, show that the following rules hold:
+   (a) $(f+g)'(x) = f'(x) + g'(x)$.
+   (b) $(fg)'(x) = f(x)g'(x) + f'(x)g(x)$.
+   (c) $(f(x)^m)' = m f(x)^{m-1} f'(x)$ for all positive integers $m$.
+   (d) If $f(x) = f_1(x)^{a_1} f_2(x)^{a_2} \cdots f_t(x)^{a_t}$, where $a_1, \dots, a_t$ are positive integers and $f_1(x), \dots, f_t(x)$ are distinct and irreducible over $\mathbb{F}_q$, then
+   $$ \frac{f(x)}{\gcd(f(x), f'(x))} = f_1(x) \cdots f_t(x). $$
+   (e) Show that $f(x)$ has no repeated irreducible factors if and only if $f(x)$ and $f'(x)$ are relatively prime.
+   (f) Show that $x^n - 1$ has no repeated irreducible factors if and only if $q$ and $n$ are relatively prime.

To help factor $x^n - 1$ over $\mathbb{F}_q$, it is useful to find an extension field $\mathbb{F}_{q^t}$ of $\mathbb{F}_q$ that contains all of its roots. In other words, $\mathbb{F}_{q^t}$ must contain a primitive $n$th root of unity, which occurs precisely when $n | (q^t - 1)$ by Theorem 3.3.3. Define the order $\text{ord}_n(q)$ of $q$ modulo $n$ to be the smallest positive integer $s$ such that $q^s \equiv 1 (\text{mod } n)$. Notice that if $t = \text{ord}_n(q)$, then $\mathbb{F}_{q^t}$ contains a primitive $n$th root of unity $\alpha$, but no smaller extension field of $\mathbb{F}_q$ contains such a primitive root. As the $\alpha^i$ are distinct for $0 \le i < n$ and $(\alpha^i)^n = 1$, $\mathbb{F}_{q^t}$ contains all the roots of $x^n - 1$. Consequently, $\mathbb{F}_{q^t}$ is called a splitting field of $x^n - 1$ over $\mathbb{F}_q$. So the irreducible factors of $x^n - 1$ over $\mathbb{F}_q$ must be product of the distinct minimal polynomials of the $n$th roots of unity in $\mathbb{F}_{q^t}$. Suppose that $\gamma$ is a primitive element of $\mathbb{F}_q$. Then $\alpha = \gamma^d$ is a primitive $n$th root of unity where $d = (q^t - 1)/n$. The roots of $M_\alpha(x)$ are $\{\gamma^d, \gamma^{dq}, \gamma^{dq^2}, \dots, \gamma^{dq^{r-1}}\} = \{\alpha^1, \alpha^q, \alpha^{q^2}, \dots, \alpha^{q^{r-1}}\}$, where $r$ is the smallest positive integer such that $dsq^r \equiv ds (\text{mod } q^t - 1)$ by Theorem 3.7.6. But $dsq^r \equiv ds (\text{mod } q^t - 1)$ if and only if $sq^r \equiv s (\text{mod } n)$.

This leads us to extend the notion of $q$-cyclotomic cosets first developed in Section 3.7. Let $s$ be an integer with $0 \le s < n$. The $q$-cyclotomic coset of $s$ modulo $n$ is the set

$C_s = \{s, sq, \dots, sq^{r-1}\} (\text{mod } n)$.

where $r$ is the smallest positive integer such that $sq^r \equiv s (\text{mod } n)$. It follows that $C_s$ is the orbit of the permutation $i \mapsto iq (\text{mod } n)$ that contains $s$. The distinct $q$-cyclotomic cosets