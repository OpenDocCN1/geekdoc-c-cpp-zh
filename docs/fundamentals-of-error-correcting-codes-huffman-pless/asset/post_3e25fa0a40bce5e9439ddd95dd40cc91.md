
Two elements of $\mathbb{F}_{q^r}$ which have the same minimal polynomial in $\mathbb{F}_q[x]$ are called conjugate over $\mathbb{F}_q$. It will be important to find all the conjugates of $\alpha \in \mathbb{F}_{q^r}$, that is, all the roots of $M_d(x)$. We know by Theorem 3.7.3(ii) that the roots of $M_d(x)$ are distinct and lie in $\mathbb{F}_{q^r}$. We can find these roots with the assistance of the following theorem.

### Theorem 3.7.4 Let $f(x)$ be a polynomial in $\mathbb{F}_q[x]$ and let $\alpha$ be a root of $f(x)$ in some extension field $\mathbb{F}_{q^r}$. Then:

- (i) $f(\alpha^q) = f(\alpha)^q$, and
- (ii) $\alpha^q$ is also a root of $f(x)$ in $\mathbb{F}_q$.

**Proof:** Let $f(x) = \sum_{i=0}^m a_i x^i$. Since $q = p^m$, where $p$ is the characteristic of $\mathbb{F}_q$, $f(x)^q = \sum_{i=0}^m a_i^q x^{iq}$ by applying Exercise 152 repeatedly. However, $a_i^q = a_i$, because $a_i \in \mathbb{F}_q$ and elements of $\mathbb{F}_q$ are roots of $x^q - x$ by Theorem 3.3.2. Thus (i) holds. In particular, $f(\alpha^q) = f(\alpha)^q = 0$, implying (ii).

Repeatedly applying this theorem we see that $\alpha, \alpha^q, \alpha^{q^2}, \dots$ are all roots of $M_d(x)$. Where does this sequence stop? It will stop after $r$ terms, where $\alpha^{q^r} = \alpha$. Suppose now that $\gamma$ is a primitive element of $\mathbb{F}_{q^r}$. Then $\alpha = \gamma^s$ for some $s$. Hence $\alpha^{q^r} = \alpha$ if and only if $s q^r \equiv s \pmod{q^r - 1}$. By Theorem 3.3.1(ii), $sq^r \equiv s \pmod{q^r - 1}$. Based on this, we define the $q$-cyclotomic coset of $s$ modulo $q^r - 1$ to be the set

$C_s = \{s, sq, \dots, sq^{r-1}\} \pmod{q^r - 1}$,

where $r$ is the smallest positive integer such that $sq^r \equiv s \pmod{q^r - 1}$. The sets $C_s$ partition the set $\{0, 1, 2, \dots, q^r - 2\}$ of integers into disjoint sets. When listing the cyclotomic cosets, it is usual to list $C_s$ only once, where $s$ is the smallest element of the coset.

### Example 3.7.5 The 2-cyclotomic cosets modulo 15 are $C_0 = \{0\}, C_1 = \{1, 2, 4, 8\}, C_3 = \{3, 6, 12, 9\}, C_5 = \{5, 10\}, \text{and } C_7 = \{7, 14, 13, 11\}$.

### Exercise 184 Compute the 2-cyclotomic cosets modulo:

- (a) 7,
- (b) 31,
- (c) 63.

### Exercise 185 Compute the 3-cyclotomic cosets modulo:

- (a) 8,
- (b) 26.

### Exercise 186 Compute the 4-cyclotomic cosets modulo:

- (a) 15,
- (b) 63.

Compare your answers to those of Example 3.7.5 and Exercise 184.

We now know that the roots of $M_\alpha(x)$ include $\{y^i \mid i \in C_s\}$. In fact these are all the roots. So if we know the size of $C_s$, we know the degree of $M_\alpha(x)$, as these are the same.

### Theorem 3.7.6 If \(\gamma\) is a primitive element of \(\mathbb{F}_{q^l}\), then the minimal polynomial of \(\gamma^j\) over \(\mathbb{F}_q\) is
\(M_{\gamma^j}(x) = \prod_{i \in C_j} (x - \gamma^i).\)

**Proof:** This theorem is claiming that, when expanded, \(f(x) = \prod_{i \in C_j} (x - \gamma^i) = \sum_j f_j x^j\) is a polynomial in \(\mathbb{F}_q[x]\), not merely \(\mathbb{F}_{q^l}[x]\). Let \(g(x) = f(x^q)\). Then \(g(x) = \prod_{i \in C_j} (x^q - \gamma^i)\) by Exercise 152. As \(C_j\) is a \(q\)-cyclotomic coset, \(q i\) runs through \(C_j\) as \(i\) does. Thus \(g(x) = f(x^q) = \sum_j f_j x^{qj}\). But \(g(x) = (\sum_j f_j x^j)^q = \sum_j f_j^q x^{qj}\), again by Exercise 152. Equating coefficients, we have \(f_j^q = f_j\) and hence by Theorem 3.6.1(iii), \(f(x) \in \mathbb{F}_q[x]\).

### Exercise 187 Prove that the size \(r\) of a \(q\)-cyclotomic coset modulo \(q^l - 1\) satisfies \(r \mid l\).

### Example 3.7.7 The field \(\mathbb{F}_8\) was constructed in Examples 3.4.2 and 3.4.3. In the table below we give the minimal polynomial over \(\mathbb{F}_2\) of each element of \(\mathbb{F}_8\) and the associated 2-cyclotomic coset modulo 7.

| Roots | Minimal polynomial | 2-cyclotomic coset |
| :--- | :--- | :--- |
| 0 | \(x\) | |
| 1 | \(x + 1\) | |
| \(\alpha, \alpha^2, \alpha^4\) | \(x^3 + x + 1\) | \(\{1, 2, 4\}\) |
| \(\alpha^3, \alpha^5, \alpha^6\) | \(x^3 + x^2 + 1\) | \(\{3, 5, 6\}\) |

Notice that \(x^8 - x = x(x+1)(x^3+x+1)(x^3+x^2+1)\) is the factorization of \(x^8 - x\) into irreducible polynomials in \(\mathbb{F}_2[x]\) consistent with Theorem 3.7.3(iv). The polynomials \(x^3+x+1\) and \(x^3+x^2+1\) are primitive polynomials of degree 3.

### Example 3.7.8 In Exercise 173, you are asked to construct \(\mathbb{F}_{16}\) using the irreducible polynomial \(x^4 + x + 1\) over \(\mathbb{F}_2\). With \(\alpha\) as a root of this polynomial, we give the minimal polynomial over \(\mathbb{F}_2\) of each element of \(\mathbb{F}_{16}\) and the associated 2-cyclotomic coset modulo 15 in the table below.

| Roots | Minimal polynomial | 2-cyclotomic coset |
| :--- | :--- | :--- |
| 0 | \(x\) | |
| 1 | \(x + 1\) | |
| \(\alpha, \alpha^2, \alpha^4, \alpha^8\) | \(x^4 + x + 1\) | \(\{1, 2, 4, 8\}\) |
| \(\alpha^3, \alpha^6, \alpha^9, \alpha^{12}\) | \(x^4 + x^3 + x^2 + x + 1\) | \(\{3, 6, 9, 12\}\) |
| \(\alpha^5, \alpha^{10}\) | \(x^2 + x + 1\) | \(\{5, 10\}\) |
| \(\alpha^7, \alpha^{11}, \alpha^{13}, \alpha^{14}\) | \(x^4 + x^3 + 1\) | \(\{7, 11, 13, 14\}\) |

The factorization of \(x^{15} - 1\) into irreducible polynomials in \(\mathbb{F}_2[x]\) is
\((x+1)(x^4+x+1)(x^4+x^3+x^2+x+1)(x^2+x+1)(x^4+x^3+1),\)
again consistent with Theorem 3.7.3.(iv).

### Exercise 188 Referring to Example 3.7.8:

- (a) verify that the table is correct,
- (b) find the elements of $\mathbb{F}_{16}$ that make up the subfields $\mathbb{F}_2$ and $\mathbb{F}_4$, and
- (c) find which irreducible polynomials of degree 4 are primitive.

### Exercise 189 The irreducible polynomials of degree 2 over $\mathbb{F}_3$ were found in Exercise 170.

- (a) Which of the irreducible polynomials of degree 2 are primitive?
- (b) Let $\alpha$ be a root of one of these primitive polynomials. Construct the field $\mathbb{F}_9$ by adjoining $\alpha$ to $\mathbb{F}_3$ and giving a table with each vector in $\mathbb{F}_3$ assigned to 0 and the powers of $\alpha$.
- (c) In a table as in Examples 3.7.7 and 3.7.8, give the minimal polynomial over $\mathbb{F}_3$ of each element of $\mathbb{F}_9$ and the associated 3-cyclotomic coset modulo 8.
- (d) Verify that the product of all the elements in your table is $x^9 - x$.

### Exercise 190 Without factoring $x^{63} - 1$, how many irreducible factors does it have over $\mathbb{F}_2$ and what are their degrees? Answer the same question about $x^{63} - 1$ over $\mathbb{F}_4$. See Exercises 184 and 186.

### Exercise 191 Without factoring $x^{26} - 1$, how many irreducible factors does it have over $\mathbb{F}_3$ and what are their degrees? See Exercise 185.

### Exercise 192 Let $f(x) = f_0 + f_1 x + \dots + f_a x^a$ be a polynomial of degree $a$ in $\mathbb{F}_q[x]$. The reciprocal polynomial of $f(x)$ is the polynomial
$f^*(x) = x^a f(x^{-1}) = f_a + f_{a-1}x + \dots + f_0 x^a$.
(We will study reciprocal polynomials further in Chapter 4.)

- (a) Give the reciprocal polynomial of each of the polynomials in the table of Example 3.7.7.
- (b) Give the reciprocal polynomial of each of the polynomials in the table of Example 3.7.8.
- (c) What do you notice about the roots and the irreducibility of the reciprocal polynomials that you found in parts (a) and (b)?
- (d) How can you use what you have learned about reciprocal polynomials in parts (a), (b), and (c) to help find irreducible factors of $x^q - x$ over $\mathbb{F}_p$ where $q = p^m$ with $p$ a prime?

## 3.8 Trace and subfield subcodes

Suppose that we have a code $\mathcal{C}$ over a field $\mathbb{F}_{q^r}$. It is possible that some of the codewords have all their components in the subfield $\mathbb{F}_q$. Can much be said about the code consisting of such codewords? Using the trace function, a surprising amount can be said.

Let $\mathcal{C}$ be an $[n, k]$ code over $\mathbb{F}_{q^r}$. The subfield subcode $\mathcal{C}|_{\mathbb{F}_q}$ of $\mathcal{C}$ with respect to $\mathbb{F}_q$ is the set of codewords in $\mathcal{C}$ each of whose components is in $\mathbb{F}_q$. Because $\mathcal{C}$ is linear over $\mathbb{F}_{q^r}$, $\mathcal{C}|_{\mathbb{F}_q}$ is a linear code over $\mathbb{F}_q$.

We first describe how to find a parity check matrix for $\mathcal{C}|_{\mathbb{F}_q}$, beginning with a parity check matrix $H$ of $\mathcal{C}$. Because $\mathbb{F}_{q^r}$ is a vector space of dimension $r$ over $\mathbb{F}_q$, we can choose a basis $\{b_1, b_2, \dots, b_r\} \subset \mathbb{F}_{q^r}$ of $\mathbb{F}_{q^r}$ over $\mathbb{F}_q$. Each element $z \in \mathbb{F}_{q^r}$ can be uniquely written
