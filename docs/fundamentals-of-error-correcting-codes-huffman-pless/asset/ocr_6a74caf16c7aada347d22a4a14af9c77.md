Proof: We prove only the case when $r$ is odd and leave the case when $r$ is even to Exercise 728. Working in $\mathfrak{R}_p$, by Lemma 12.4.1,

\[ Q(x)^2 = \left( \sum_{i \in \mathbb{Q}_p} x^i \right)^2 = \sum_{i \in \mathbb{Q}_p} x^{2i} + \sum_{i \neq j, i, j \in \mathbb{Q}_p} x^{i+j} \\
= Q(x) + 2r(1 - Q(x)) + rN(x) = Q(x) + 2N(x) \]

since $r$ is odd and $2 \in \mathbb{Q}_p$ by Lemma 6.2.5. Similarly,

\[ N(x)^2 = \left( \sum_{i \in N_r} x^i \right)^2 = \sum_{i \in N_r} x^{2i} + \sum_{i \neq j, i, j \in N_r} x^{i+j} \\
= N(x) + 2r(1 - N(x)) + rQ(x) = N(x) + 2Q(x). \]

So $(Q(x) + 2N(x))^2 = Q(x)^2 = Q(x) + 2N(x)$, $(N(x) + 2Q(x))^2 = N(x)^2 = N(x) + 2Q(x)$, $(1 - Q(x) + 2N(x))^2 = 1 - Q(x)^2 = 1 - 2Q(x) + Q(x)^2 = 1 - Q(x) + 2N(x)$, and $(1 - N(x) + 2Q(x))^2 = 1 - N(x)^2 = 1 - 2N(x) + N(x)^2 = 1 - N(x) + 2Q(x)$. Finally, $j(x)^2 = p^2 \sum_{i=0}^{r-1} x^i = \sum_{j=0}^{p-1} x^j = p^r (p \sum_{i=0}^{p-1} x^i) = j(x)$ (since $p^2 \equiv 1 \pmod 8$).

# Exercise 728 Prove Lemma 12.4.2 when $r$ is even.

We now define the $\mathbb{Z}_4$-quadratic residue codes using the idempotents of Lemma 12.4.2. The definitions depend upon the value of $p$ modulo 8.

# 12.4.1 $\mathbb{Z}_4$-quadratic residue codes: $p \equiv -1 \pmod 8$

We first look at the case where $p \equiv -1 \pmod 8$. Let $p + 1 = 8r$. If $r$ is odd, define $D_1 = \langle Q(x) + 2N(x) \rangle$, $D_2 = \langle N(x) + 2Q(x) \rangle$, $C_1 = \langle 1 - N(x) + 2Q(x) \rangle$, and $C_2 = \langle 1 - Q(x) + 2N(x) \rangle$. If $r$ is even, define $D_1 = \langle -Q(x) \rangle$, $D_2 = \langle -N(x) \rangle$, $C_1 = \langle 1 + N(x) \rangle$, and $C_2 = \langle 1 + Q(x) \rangle$. These codes are called $\mathbb{Z}_4$-quadratic residue codes when $p \equiv -1 \pmod 8$.

The next result, from [279, 289], shows why these codes are called quadratic residue codes; compare this result with those in Chapter 6.

# Theorem 12.4.3 Let $p \equiv -1 \pmod 8$. The $\mathbb{Z}_4$-quadratic residue codes satisfy the following:

+   (i) $D_1 \mu_a = D_1$ and $C_1 \mu_a = C_1$ for $a \in \mathbb{Q}_p$; $D_1 \mu_a = D_2$ and $C_1 \mu_a = C_2$ for $a \in N_p$; in particular $D_1$ and $D_2$ are equivalent as are $C_1$ and $C_2$.
+   (ii) $D_1 \cap D_2 = \langle j(x) \rangle$ and $D_1 + D_2 = \mathfrak{R}_p$.
+   (iii) $C_1 \cap C_2 = \{0\}$ and $C_1 + C_2 = \langle j(x) \rangle^\perp$.
+   (iv) $D_1$ and $D_2$ have type $4^{(p+1)/2}$. $C_1$ and $C_2$ have type $4^{(p-1)/2}$.
+   (v) $D_i = C_i + \langle j(x) \rangle$ for $i = 1$ and $2$.
+   (vi) $C_1$ and $C_2$ are self-orthogonal and $C_i^\perp = D_i$ for $i = 1$ and $2$.

Proof: Suppose that $p + 1 = 8r$. We verify this result when $r$ is odd and leave the proof for $r$ even as an exercise.