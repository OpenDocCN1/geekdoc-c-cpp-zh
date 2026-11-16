# **Exercise 715** Do the following:

(a) Suppose that $n$ is odd and the factorization of $x^n + 1$ into irreducible polynomials in $F_3[x]$ is $x^n + 1 = (x + 1)(x^{n-1} + x^{n-2} + \cdots + x + 1)$. Show that the factorization of $x^n - 1$ into monic irreducible polynomials in $Z_4[x]$ is $x^n - 1 = (x - 1)(x^{n-1} + x^{n-2} + \cdots + x + 1)$. Note that this does not require the use of Graeffe's method.

(b) Show that when $n = 3, 5, 11, 13, \text{ and } 19$, the factorization of $x^n - 1$ in $Z_4[x]$ is given by (a).

# 12.3.2 The ring $R_n = Z_4[x]/(x^n - 1)$

To study cyclic codes over $F_q$ we needed to find the ideals of $F_q[x]/(x^n - 1)$. Similarly, we need to find the ideals of $R_n$, in order to study cyclic codes over $Z_4$. We first need to know the ideal structure of $Z_4[x]/(f(x))$, where $f(x)$ is a basic irreducible polynomial.

# Lemma 12.3.9 If $f(x) \in Z_4[x]$ is a basic irreducible polynomial, then $R = Z_4[x]/(f(x))$ has only three ideals: $(0)$, $(2) = (2s(x) + (f(x)) \mid s(x) \in Z_4[x])$, and $(1) = R$.

Proof: Suppose $I$ is a nonzero ideal in $R$. Let $g(x) + (f(x)) \in I$ with $g(x) \notin (f(x))$. As $\mu(f(x))$ is irreducible, $\gcd(\mu(g(x)), \mu(f(x)))$ is either $1$ or $\mu(f(x))$. Arguing as in the proof of Lemma 12.3.2, either $a(x)g(x) + b(x)f(x) = 1 + 2s(x)$ or $g(x) = f(x)a(x) + 2s(x)$ for some $a(x)$, $b(x)$, and $s(x) \in Z_4[x]$. In the former case, $a(x)g(x)(1 + 2s(x)) + b(x)f(x)(1 + 2s(x)) = (1 + 2s(x))^2 = 1$, implying that $g(x) + (f(x))$ has an inverse $a(x)(1 + 2s(x)) + f(x)$ in $R$. But this means that $I$ contains an invertible element and hence equals $R$ by Exercise 716. In the latter case, $g(x) + (f(x)) \in (2)$, and hence we may assume that $I \subseteq (2)$. As $I \neq \{0\}$, there exists $h(x) \in Z_4[x]$ such that $2h(x) + (f(x)) \in I$ with $2h(x) \notin (f(x))$. Assume that $\mu(h(x)) \in (\mu(f(x)))$; then $h(x) = f(x)s(x) + 2s(x)$ for some $a(x)$ and $s(x)$ in $Z_4[x]$ implying $2h(x) = 2f(x)s(x) \in (f(x))$, a contradiction. Hence as $\mu(h(x)) \notin (\mu(f(x)))$ and $\mu(f(x))$ is irreducible, $\gcd(\mu(h(x)), \mu(f(x))) = 1$. Again, $a(x)h(x) + b(x)f(x) = 1 + 2s(x)$ for some $a(x)$, $b(x)$, and $s(x)$ in $Z_4[x]$. Therefore $a(x)(2h(x)) + 2b(x)f(x) = 2$ showing that $2 + (f(x)) \in I$ and so $(2) \subseteq I$. Thus $I = (2)$.

# Exercise 716 Prove that if $I$ is an ideal of a ring $R$ and $I$ contains an invertible element, then $I = R$.

We do not have the Division Algorithm in $Z_4[x]$ and so the next result is not as obvious as the corresponding result in $F_q[x]$.

# Lemma 12.3.10 Let $m(x)$ be a monic polynomial of degree $r$ in $Z_4[x]$. Then $Z_4[x]/(m(x))$ has $4^r$ elements, and every element of $Z_4[x]/(m(x))$ is uniquely expressible in the form $a(x) + (m(x))$, where $a(x)$ is the zero polynomial or has degree less than $r$.

Proof: Let $a(x) = a_r x^r + a_{r-1} x^{r-1} + \cdots + a_0 \in Z_4[x]$. If $d \ge r$, then $h(x) = a(x) - a_r x^{d-r} m(x)$ has degree less than $d$ and $a(x) + (m(x)) = h(x) + (m(x))$. Hence every element $a(x) + (m(x))$ of $Z_4[x]/(m(x))$ has a representative of degree less than $r$. Furthermore, if $b_1(x) + (m(x)) = b_2(x) + (m(x))$ with $b_i(x)$ each of degree less than $r$, then $b_1(x) - b_2(x)$ is a multiple of $m(x)$. By Exercise 717, $b_1(x) = b_2(x)$. The result follows.