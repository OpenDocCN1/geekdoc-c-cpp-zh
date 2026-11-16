then we leave it as an exercise to show that \(\overline{C}\) is a cyclic code with generating idempotent \(\overline{e(x)} = \sum_j \overline{a_j} \sum_{i \in C_j} x^i\). Furthermore, by examining (4.6), we see that \(\overline{e(x)} = e(x)\mu_2\). By Theorem 4.3.13, \(\overline{C} = \langle \mu_2 \rangle\). We summarize these results.

# **Theorem 4.3.16** Let \(C\) be a cyclic code over \(\mathbb{F}_4\) with generating idempotent \(e(x)\). Then \(e(x)\) has the form given in (4.6). Also \(\overline{C} = C\mu_2\) is cyclic with generating idempotent \(e(x)\mu_2\).

# **Exercise 235** Show that if \(e(x)\) is the generating idempotent of a cyclic code \(\mathcal{C}\) over \(\mathbb{F}_4\), then \(\overline{C}\) is a cyclic code with generating idempotent \(\overline{e(x)} = \sum_j \overline{a_j} \sum_{i \in C_j} x^i\). Show also that \(e(\overline{C}) = e(x)\mu_2\).

# **Exercise 236** Do the following:

+   (a) List the 4-cyclotomic cosets modulo 21.

+   (b) Construct a set \(S = K \cup L_1 \cup L_2\) of distinct 4-cyclotomic coset representatives modulo 21 which can be used to construct idempotents in \(\mathcal{R}_{21}\) over \(\mathbb{F}_4\) as in the discussion prior to Theorem 4.3.16.

+   (c) Give the general form of such an idempotent.

+   (d) How many of these idempotents are there?

+   (e) Write down four of these idempotents.

Theorem 4.3.13 shows that \(\mu_a\) maps cyclic codes to cyclic codes with the generating idempotent mapped to the generating idempotent; however, the generator polynomial may not be mapped to the generator polynomial of the image code. In fact, the automorphism \(\mu_a\) maps the generator polynomial to its \(qh\) power. See Exercise 232.

A multiplier takes a cyclic code into an equivalent cyclic code. The following theorem, a special case of a theorem of Pálfy (see [150]), implies that, in certain instances, two cyclic codes are permutation equivalent if and only if a multiplier takes one to the other. This is a very powerful result when it applies.

# **Theorem 4.3.17** Let \(C_1\) and \(C_2\) be cyclic codes of length \(n\) over \(\mathbb{F}_q\). Assume that \(\gcd(n, \phi(n)) = 1\), where \(\phi\) is the Euler \(\phi\)-function. Then \(C_1\) and \(C_2\) are permutation equivalent if and only if there is a multiplier that maps \(C_1\) to \(C_2\).

Since multipliers send generating idempotents to generating idempotents, we have the following corollary.

# **Corollary 4.3.18** Let \(C_1\) and \(C_2\) be cyclic codes of length \(n\) over \(\mathbb{F}_q\). Assume that \(\gcd(n, \phi(n)) = 1\), where \(\phi\) is the Euler \(\phi\)-function. Then \(C_1\) and \(C_2\) are permutation equivalent if and only if there is a multiplier that maps the idempotent of \(C_1\) to the idempotent of \(C_2\).

# ## 4.4 Zeros of a cyclic code

Recall from Section 4.1 and, in particular Theorem 4.1.1, that if \(t = \text{ord}_n(q)\), then \(\mathbb{F}_q\) is a splitting field of \(x^n - 1\); so \(\mathbb{F}_q\) contains a primitive nth root of unity \(\alpha\), and \(x^n - 1 = \prod_{i=0}^{n-1} (x - \alpha^i)\) is the factorization of \(x^n - 1\) into linear factors over \(\mathbb{F}_q\). Furthermore \(x^n - 1 = \prod_i M_{\alpha^i}(x)\) is the factorization of \(x^n - 1\) into irreducible factors