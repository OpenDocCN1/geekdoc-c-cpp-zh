
modulo $n$ partition the set of integers $\{0, 1, 2, \dots, n-1\}$. As before we normally denote a cyclotomic coset in this partition by choosing $s$ to be the smallest integer contained in the cyclotomic coset. In Section 3.7 we had studied the more restricted case where $n = q' - 1$. Notice that $\text{ord}_n(q)$ is the size of the $q$-cyclotomic coset $C_1$ modulo $n$. This discussion gives the following theorem.

### Theorem 4.1.1 Let $n$ be a positive integer relatively prime to $q$. Let $t = \text{ord}_n(q)$. Let $\alpha$ be a primitive $n$th root of unity in $\mathbb{F}_q$.

- (i) For each integer $s$ with $0 \le s < n$, the minimal polynomial of $\alpha^s$ over $\mathbb{F}_q$ is $M_{\alpha^s}(x) = \prod_{i \in C_s} (x - \alpha^i)$,

where $C_s$ is the $q$-cyclotomic coset of $s$ modulo $n$.

- (ii) The conjugates of $\alpha^s$ are the elements $\alpha^i$ with $i \in C_s$.

- (iii) Furthermore,
\[x^n - 1 = \prod_s M_{\alpha^s}(x)\]

is the factorization of $x^n - 1$ into irreducible factors over $\mathbb{F}_q$, where $s$ runs through a set of representatives of the $q$-cyclotomic cosets modulo $n$.

### Example 4.1.2 The 2-cyclotomic cosets modulo 9 are $C_0 = \{0\}$, $C_1 = \{1, 2, 4, 8, 7, 5\}$, and $C_3 = \{3, 6\}$. So $\text{ord}_9(2) = 6$ and the primitive ninth roots of unity lie in $\mathbb{F}_{64}$ but in no smaller extension field of $\mathbb{F}_2$. The irreducible factors of $x^9 - 1$ over $\mathbb{F}_2$ have degrees 1, 6, and 2. These are the polynomials $M_1(x) = x + 1$, $M_\alpha(x)$, and $M_{\alpha^3}(x)$, where $\alpha$ is a primitive ninth root of unity in $\mathbb{F}_{64}$. The only irreducible polynomial of degree 2 over $\mathbb{F}_2$ is $x^2 + x + 1$, which must therefore be $M_{\alpha^3}(x)$. (Notice also that $\alpha^3$ is a primitive third root of unity, which must lie in the subfield $\mathbb{F}_4$ of $\mathbb{F}_{64}$.) Hence the factorization of $x^9 - 1$ is $x^9 - 1 = (x + 1)(x^2 + x + 1)(x^6 + x^3 + 1)$ and $M_\alpha(x) = x^6 + x^3 + 1$.

### Example 4.1.3 The 3-cyclotomic cosets modulo 13 are $C_0 = \{0\}$, $C_1 = \{1, 3, 9\}$, $C_2 = \{2, 6, 5\}$, $C_4 = \{4, 12, 10\}$, and $C_7 = \{7, 8, 11\}$. So $\text{ord}_{13}(3) = 3$ and the primitive 13th roots of unity lie in $\mathbb{F}_{27}$ but in no smaller extension field of $\mathbb{F}_3$. The irreducible factors of $x^{13} - 1$ over $\mathbb{F}_3$ have degrees 1, 3, 3, 3, and 3. These are the polynomials $M_1(x) = x - 1$, $M_\alpha(x)$, $M_{\alpha^2}(x)$, $M_{\alpha^4}(x)$, and $M_{\alpha^7}(x)$, where $\alpha$ is a primitive 13th root of unity in $\mathbb{F}_{27}$.

In these examples we notice that the size of each $q$-cyclotomic coset is a divisor of $\text{ord}_n(q)$. This holds in general.

### Theorem 4.1.4 The size of each $q$-cyclotomic coset is a divisor of $\text{ord}_n(q)$. Furthermore, the size of $C_1$ is $\text{ord}_n(q)$.

Proof: Let $t = \text{ord}_n(q)$ and let $m$ be the size of $C_s$. Then $M_{\alpha^s}(x)$ has degree $m$ where $\alpha$ is a primitive $n$th root of unity. So $m | t$ by Theorem 3.7.3. The fact that the size of $C_1$ is $\text{ord}_n(q)$ follows directly from the definitions of $q$-cyclotomic cosets and $\text{ord}_n(q)$ as mentioned prior to Theorem 4.1.1.

### Exercise 202 Let $q = 2$.

- (a) Find the $q$-cyclotomic cosets modulo $n$ where $n$ is:
  - (i) 23,
  - (ii) 45.
- (b) Find $\text{ord}_n(q)$ for the two values of $n$ given in part (a).
- (c) What are the degrees of the irreducible factors of $x^n - 1$ over $\mathbb{F}_q$ for the two values of $n$ given in part (a)?

### Exercise 203 Repeat Exercise 202 with $q = 3$ and $n = 28$ and $n = 41$.

### Exercise 204 Factor $x^{13} - 1$ over $\mathbb{F}_3$.

We conclude this section by noting that there are efficient computer algorithms for factoring polynomials over a finite field, among them the algorithm of Berlekamp, MacWilliams, and Sloane [18]. Many of the algebraic manipulation software packages can factor $x^n - 1$ over a finite field for reasonably sized integers $n$. There are also extensive tables in [256] listing all irreducible polynomials over $\mathbb{F}_2$ for $n \le 34$.

## 4.2 Basic theory of cyclic codes

We noted earlier that cyclic codes over $\mathbb{F}_q$ are precisely the ideals of $\mathcal{R}_n = \mathbb{F}_q[x]/(x^n - 1)$.

Exercises 153 and 166 show that $\mathbb{F}_q[x]$ is a principal ideal domain. It is straightforward then to show that the ideals of $\mathcal{R}_n$ are also principal, and hence cyclic codes are the principal ideals of $\mathcal{R}_n$. When writing a codeword of a cyclic code as $c(x)$, we technically mean the coset $c(x) + (x^n - 1)$ in $\mathcal{R}_n$. However, such notation is too cumbersome, and we will write $c(x)$ even when working in $\mathcal{R}_n$. Thus we think of the elements of $\mathcal{R}_n$ as the polynomials in $\mathbb{F}_q[x]$ of degree less than $n$ with multiplication being carried out modulo $x^n - 1$. So when working in $\mathcal{R}_n$, to multiply two polynomials, we multiply them as we would in $\mathbb{F}_q[x]$ and then replace any term of the form $ax^{n+j}$, where $0 \le j < n$, by $ax^j$. We see immediately that when writing a polynomial as both an element in $\mathbb{F}_q[x]$ and an element in $\mathcal{R}_n$, confusion can easily arise. The reader should be aware of which ring is being considered.

As stated earlier, though our study of cyclic codes, we make the basic assumption that the characteristic $p$ of $\mathbb{F}_q$ does not divide the length $n$ of the cyclic codes being considered, or equivalently, that $\text{gcd}(n, q) = 1$. The primary reason for this assumption is that $x^n - 1$ has distinct roots in an extension field of $\mathbb{F}_q$ by Exercise 201, and this enables us to describe its roots (and as we shall see, cyclic codes) by $q$-cyclotomic cosets modulo $n$. The assumption that $p$ does not divide $n$ also implies that $\mathcal{R}_n$ is semi-simple and thus that the Wedderburn Structure Theorems apply; we shall not invoke these structure theorems preferring rather to derive the needed consequences for the particular case of $\mathcal{R}_n$. The theory of cyclic codes with $\text{gcd}(n, q) \neq 1$ is discussed in [49, 201], but, to date, these "repeated root" cyclic codes do not seem to be of much interest.

To distinguish the principal ideal \(\langle g(x) \rangle\) of \(\mathbb{F}_q[x]\) from that ideal in \(\mathcal{R}_n\), we use the notation \(\langle g(x) \rangle\) for the principal ideal of \(\mathcal{R}_n\) generated by \(g(x)\). We now show that there is a bijective correspondence between the cyclic codes in \(\mathcal{R}_n\) and the monic polynomial divisors of \(x^n - 1\).

### Theorem 4.2.1 Let \(\mathcal{C}\) be a nonzero cyclic code in \(\mathcal{R}_n\). There exists a polynomial \(g(x) \in \mathcal{C}\) with the following properties:

- (i) \(g(x)\) is the unique monic polynomial of minimum degree in \(\mathcal{C}\),
- (ii) \(\mathcal{C} = \langle g(x) \rangle\), and
- (iii) \(g(x) | (x^n - 1)\).
- Let \(k = n - \deg g(x)\), and let \(g(x) = \sum_{i=0}^{n-k} g_i x^i\), where \(g_{n-k} = 1\). Then:
- (iv) the dimension of \(\mathcal{C}\) is \(k\) and \(\{g(x), xg(x), \dots, x^{k-1}g(x)\}\) is a basis for \(\mathcal{C}\),
- (v) every element of \(\mathcal{C}\) is uniquely expressible as a product \(g(x)f(x)\), where \(f(x) = 0\) or \(\deg f(x) < k\),
- (vi)
\[
G = \left[ \begin{array}{ccccccc} g_0 & g_1 & g_2 & \cdots & g_{n-k} & & 0 \\ 0 & g_0 & g_1 & \cdots & g_{n-k-1} & g_{n-k} & \\ & \ddots & \ddots & & \ddots & & \ddots \\ 0 & & g_0 & \cdots & & & g_{n-k} \\ \end{array} \right]
\]
\(\leftrightarrow \left[ \begin{array}{c} g(x) \\ xg(x) \\ \cdots \\ x^{k-1}g(x) \end{array} \right]\)

is a generator matrix for \(\mathcal{C}\), and
- (vii) if \(\alpha\) is a primitive $n$th root of unity in some extension field of $\mathbb{F}_q$, then
\[g(x) = \prod_j M_{\alpha^j}(x),\]

where the product is over a subset of representatives of the $q$-cyclotomic cosets modulo $n$.

**Proof:** Let \(g(x)\) be a monic polynomial of minimum degree in \(\mathcal{C}\). Since \(\mathcal{C}\) is nonzero, such a polynomial exists. If \(c(x) \in \mathcal{C}\), then by the Division Algorithm in \(\mathbb{F}_q[x]\), \(c(x) = g(x)h(x) + r(x)\), where either \(r(x) = 0\) or \(\deg r(x) < \deg g(x)\). As \(\mathcal{C}\) is an ideal in \(\mathcal{R}_n\), \(r(x) \in \mathcal{C}\) and the minimality of the degree of \(g(x)\) implies \(r(x) = 0\). This gives (i) and (ii). By the Division Algorithm \(x^n - 1 = g(x)h(x) + r(x)\), where again \(r(x) = 0\) or \(\deg r(x) < \deg g(x)\) in \(\mathbb{F}_q[x]\). As \(x^n - 1\) corresponds to the zero codeword in \(\mathcal{C}\) and \(\mathcal{C}\) is an ideal in \(\mathcal{R}_n\), \(r(x) \in \mathcal{C}\), a contradiction unless \(r(x) = 0\), proving (iii).

Suppose that \(\deg g(x) = n - k\). By parts (ii) and (iii), if \(c(x) \in \mathcal{C}\) with \(c(x) = 0\) or \(\deg c(x) < n\), then \(c(x) = g(x)f(x)\) in \(\mathbb{F}_q[x]\). If \(c(x) \neq 0\), \(\deg c(x) < n\) implies that \(\deg f(x) < k\), by Exercise 155. Therefore

\(\mathcal{C} = \{g(x)f(x) \mid f(x) = 0 \text{ or } \deg f(x) < k\}.\)
