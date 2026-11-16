is the generating idempotent of $\langle h(x) \rangle$ by Theorem 12.3.12. Hence $1 - e(x)\mu_{-1}$ is the generating idempotent of $\langle h^*(x) \rangle = C^\perp$.

For (ii), clearly, $e_1(x)e_2(x) \in C_1 \cap C_2$. Thus $\langle e_1(x)e_2(x) \rangle \subseteq C_1 \cap C_2$. If $c(x) \in C_1 \cap C_2$, then $c(x) = s(x)e_1(x)$ and $c(x)e_2(x) = c(x)$, the latter by Exercise 725(a); thus $c(x) = c(x)e_2(x) = s(x)e_1(x)e_2(x) \in \langle e_1(x)e_2(x) \rangle$ and $C_1 \cap C_2 = \langle e_1(x)e_2(x) \rangle$. Next if $c(x) = c_1(x) + c_2(x)$ where $c_i(x) \in C_i$ for $i = 1$ and 2, then by Exercise 725(a), $c(x)e_1(x) + c_2(x) - c_1(x)e_2(x) = c_1(x) + c_1(x)e_2(x) - c_1(x)e_2(x) + c_2(x)e_1(x) + c_2(x) - c_2(x)e_1(x) = c(x)$. Since $e_1(x) + e_2(x) - e_1(x)e_2(x)$ is clearly in $C_1 + C_2$, $C_1 + C_2 = \langle e_1(x) + e_2(x) - e_1(x)e_2(x) \rangle$ by Exercise 725(b).

# **Exercise 725** Let $C$ be a cyclic code over either $\mathbb{F}_q$ or $\mathbb{Z}_4$. Do the following:

+   (a) Let $e(x)$ be a generating idempotent of $C$. Prove that $c(x) \in C$ if and only if $c(x)e(x) = c(x)$.

+   (b) Prove that if $e(x) \in C$ and $c(x)e(x) = c(x)$ for all $c(x) \in C$, then $e(x)$ is the generating idempotent of $C$. $\blacklozenge$

One way to construct the “generating idempotent” of $C$ is to begin with the primitive idempotents. We leave the proof of the following as an exercise.

# **Theorem 12.3.24** Let $n$ be odd and $g_1(x)g_2(x) \cdots g_k(x)$ be a factorization of $x^n - 1$ into irreducible polynomials in $\mathbb{Z}_4[x]$. Let $\widehat{g_i}(x) = \prod_{j \neq i} g_j(x)$ and $(\widehat{g_i}(x)) = (\widehat{e_i}(x))$, where $\widehat{e_i}(x)$ is an idempotent of $\mathfrak{R}_n$. Let $C = \langle f(x)g(x) \rangle \oplus \langle 2f(x)h(x) \rangle$ where $f(x)g(x)h(x) = x^n - 1$. Finally, suppose that $f(x)g(x) = \prod_{i \in J} e_i(x)$ and $f(x)h(x) = \prod_{j \notin J} g_j(x)$ for subsets $I$ and $J$ of $\{1, 2, \dots, k\}$. Then:

+   (i) $I' \cap J' = \emptyset$, where $I'$ and $J'$ are the complements of $I$ and $J$, respectively, in $\{1, 2, \dots, k\}$, and

+   (ii) $C = \langle e(x) + 2E(x) \rangle$, where $e(x) = \sum_{i \in I'} \widehat{e_i}(x)$ and $E(x) = \sum_{j \in J'} \widehat{e_j}(x)$. $\blacklozenge$

# **Exercise 726** Fill in the details of the proof of Theorem 12.3.24. $\blacklozenge$

There is a method for constructing idempotents, including the primitive ones, in $\mathfrak{R}_n$ found in [27, 289]. The method begins with binary idempotents in $\mathcal{R}_n$; these can be obtained from generator polynomials using the Euclidean Algorithm as given in the proof of Theorem 4.3.2.

# **Theorem 12.3.25** Let $\langle b(x) \rangle = \langle \mu(f(x)) \rangle$ where $f(x)g(x) = x^n - 1$ in $\mathbb{Z}_4[x]$, $b(x)$ is a binary idempotent in $\mathcal{R}_n = \mathbb{F}_2[x]/(x^n + 1)$, and $n$ is odd. Let $e(x) = b^2(x)$ where $b^2(x)$ is computed as in $\mathbb{Z}_4[x]$. Then $e(x)$ is the generating idempotent for $f(x)$.

**Proof:** As $b^2(x) = b(x)$ in $\mathcal{R}_n$, $\mu(e(x)) = \mu(b^2(x)) = b(x) + \mu(a(x))(x^n - 1)$ for some $a(x) \in \mathbb{Z}_4[x]$, implying that $e(x) = b(x) + a(x)(x^n - 1) + 2s(x)$ for some $s(x) \in \mathbb{Z}_4[x]$. Squaring and simplifying yields $e^2(x) = b^2(x) + d(x)(x^n - 1)$ in $\mathbb{Z}_4[x]$ or $e^2(x) = e(x)$ in $\mathfrak{R}_n$. Thus $e(x)$ is an idempotent in $\mathfrak{R}_n$.

By Theorem 4.4.6, $1 + b(x)$ is the generating idempotent in $\mathcal{R}_n$ of $\langle \mu(g(x)) \rangle$. So $1 + b(x) = r(x)g(x) + 2s(x)$ for some $r(x)$ and $s(x)$ in $\mathbb{Z}_4[x]$. Hence $b(x) = 1 + r(x)g(x) + 2(1 + s(x))$; squaring this, we obtain $e(x) = b^2(x) = 1 + t(x)g(x)$ for some $t(x)$ in $\mathbb{Z}_4[x]$. So $e(x)f(x) = f(x) + t(x)f(x)(x^n - 1)$ in $\mathbb{Z}_4[x]$ implying $f(x) \in \langle e(x) \rangle$ in $\mathfrak{R}_n$ or $\langle f(x) \rangle \subseteq \langle e(x) \rangle$.