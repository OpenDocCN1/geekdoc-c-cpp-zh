
Now let q = 3. Consider first the case p ≡ -1 (mod 12). Here the all-one vector extends to the all-one vector of length p + 1 and it is orthogonal to itself. By Lemma 6.2.4, -1 ∈ Np and (ii)(a) follows from Theorem 6.4.2. Now suppose that p ≡ 1 (mod 12). By Lemma 6.2.4, -1 ∈ Qp and by Theorem 6.4.3, C⊥1 = D2. In this case the all-one vector in D1 extends to Ĩ = 1_{p+1} · (-1) in D̃1. This vector is not orthogonal to itself, but is orthogonal to ĨD = 1_{p+1}, where 1_{p+1} is the all-one vector of length p + 1 and D is the diagonal matrix diag(1, 1, ..., 1, -1). This proves (ii)(b).

**Example 6.6.15** We describe the extensions of the QR codes discussed in Examples 6.6.7, 6.6.8, and 6.6.11. We give the extension of the generating idempotent of odd-like codes; from this one can form a basis of the extended codes using shifts of the generating idempotent extended in the same way (see Theorem 4.3.6).

- The extended coordinate of either generating idempotent of an odd-like binary QR code of length 23 is 1. These extended codes are each self-dual and doubly-even by Theorem 6.6.14. They are extended binary Golay codes.
- The extended coordinate of either generating idempotent of an odd-like QR code of length 11 over F3 is -1. The extended codes are each self-dual by Theorem 6.6.14 and are extended ternary Golay codes.
- The extended coordinate of either generating idempotent of an odd-like QR code of length 5 over F7 is 1. These extended codes are each Hermitian self-dual; they are also dual to each other under the ordinary inner product by Theorem 6.6.14. They are equivalent to the hexacode.

We are now ready to describe, in general, the extensions of the odd-like QR codes D1 and D2 of length p over Fq. We want them both to be extended in the same way whenever possible. Recall that we defined D̃ for an arbitrary odd-like duadic code D of length n using a solution γ of (6.11). As an odd-like QR code is obtained from its even-like subcode by adjoining the all-one vector 1, in order for either D̃1 to be self-dual or dual to D̃2, the extended vector Ĩ, which is 1 extended by some γ ∈ Fq, must be orthogonal to itself. This means that p + γ²p² = 0 or

1 + γ²p = 0, (6.12)

which is (6.11) with n = p. Suppose that C1 is the even-like subcode of D1. We know that either -1 ∈ Np or -1 ∈ Qp, implying C1μ+1 = C2 or C1μ-1 = C1, respectively. By Theorems 6.4.2 or 6.4.3, these yield C̃⊥1 = D̃1 or C̃1 = D̃2, respectively. Therefore, whenever (6.12) is satisfied, if -1 ∈ Np, D̃i is self-dual for i = 1 and 2, and if -1 ∈ Qp, D̃1 and D̃2 are duals of each other. This proves the following, using Lemma 6.2.4.

**Theorem 6.6.16** Let D1 and D2 be the odd-like QR codes of length p over Fq, p an odd prime. Suppose that (6.12) is satisfied. Then if p ≡ -1 (mod 4), D̃i is self-dual for i = 1 and 2, and if p ≡ 1 (mod 4), D̃1 and D̃2 are duals of each other.

Thus we are interested in the cases where (6.12) has a solution γ in Fq. This is answered by the following. We only need the case where q is a square modulo p since we are assuming QR codes of length p over Fq exist.

**Lemma 6.6.17** Let $r$ be a prime so that $q = r^t$ for some positive integer $t$. Let $p$ be an odd prime with $p \neq r$ and assume that $q$ is a square modulo $p$. There is a solution $\gamma$ of (6.12) in $\mathbb{F}_q$ except when $t$ is odd, $p \equiv 1 \pmod 4$, and $r \equiv -1 \pmod 4$. In that case there is a solution $\gamma_1$ in $\mathbb{F}_q$ of $-1 + \gamma_1^2 p = 0$.

**Proof:** If $r$ is even, then every quadratic equation with coefficients in $\mathbb{F}_r$, such as (6.12), has a solution in $\mathbb{F}_r \le \mathbb{F}_q$. Assume that $t$ is odd. Then $q$ is a square modulo $p$ if and only if $r$ is a square modulo $p$ as $q = (r^{(t-1)/2})^2 r$. So $\left(\frac{r}{p}\right) = 1$. Solving (6.12) is equivalent to solving $x^2 = -p$ in $\mathbb{F}_r$. As $r$ is odd, there is a solution in $\mathbb{F}_q$ if and only if the solution is in $\mathbb{F}_r$. This equation reduces to $x^2 = 1$ if $r = 2$, which obviously has a solution $x = 1$. Assume that $r$ is odd. Thus we have a solution to $x^2 = -p$ in $\mathbb{F}_r$ if and only if $\left(\frac{-p}{r}\right) = \left(\frac{-1}{r}\right)\left(\frac{p}{r}\right) = 1$. By the Law of Quadratic Reciprocity,

\(\left(\frac{r}{p}\right)\left(\frac{p}{r}\right) = (-1)^{\frac{r-1}{2} \frac{p-1}{2}}.\)

Hence as \(\left(\frac{p}{r}\right) = 1\),

\(\left(\frac{-1}{p}\right)\left(\frac{p}{r}\right) = (-1)^{\frac{p-1}{2}} (-1)^{\frac{r-1}{2} \frac{p-1}{2}}\)

using Lemma 6.2.2. The only time the right-hand side of this equation is not 1 is when $p \equiv 1 \pmod 4$ and $r \equiv -1 \pmod 4$. In this exceptional case

\(\left(\frac{p}{r}\right) = (-1)^{\frac{r-1}{2} \frac{p-1}{2}} = 1,\)

showing that $x^2 = p$ has a solution in $\mathbb{F}_q$; hence $-1 + \gamma_1^2 p = 0$ has a solution $\gamma_1$ in $\mathbb{F}_q$.

Combining Theorem 6.6.16 and Lemma 6.6.17, we obtain the following.

**Theorem 6.6.18** Let $r$ be a prime so that $q = r^t$ for some positive integer $t$. Let $p$ be an odd prime with $p \neq r$ and assume that $q$ is a square modulo $p$. Assume that if $t$ is odd, then either $p \not\equiv 1 \pmod 4$ or $r \not\equiv -1 \pmod 4$. Let $\mathcal{D}_1$ and $\mathcal{D}_2$ be the two odd-like QR code over $\mathbb{F}_q$ of length $p$.

- (i) If $p \equiv -1 \pmod 4$, then $\widehat{\mathcal{D}}_i$ is self-dual for $i = 1$ and 2.
- (ii) If $p \equiv 1 \pmod 4$, then $\widehat{\mathcal{D}}_1$ and $\widehat{\mathcal{D}}_2$ are duals of each other.

This theorem gives the extension except when $q = r^t$ where $t$ is odd, $p \equiv 1 \pmod 4$, and $r \equiv -1 \pmod 4$. But in that case $-1 + \gamma_1^2 p = 0$ has a solution $\gamma_1$ in $\mathbb{F}_q$ by Lemma 6.6.17. If $\mathcal{D}$ is an odd-like QR code of length $p$, define $\widehat{\mathcal{D}} = \{ \tilde{\mathbf{c}} \mid \mathbf{c} \in \mathcal{D} \}$, where $\tilde{\mathbf{c}} = c_\infty = c_0 \cdots c_{p-1}$ and

\(c_\infty = -\gamma_1 \sum_{j=0}^{p-1} c_j.\)

**Theorem 6.6.19** Let $r$ be a prime so that $q = r^t$ for some odd positive integer $t$ and $r \equiv -1 \pmod 4$. Assume $p \equiv 1 \pmod 4$ is a prime such that $q$ is a square modulo $p$. Let $\mathcal{D}_1$ and $\mathcal{D}_2$ be the two odd-like QR codes over $\mathbb{F}_q$ of length $p$. Then $\mathcal{D}_1$ and $\mathcal{D}_2$ are duals of each other, where $D$ is the diagonal matrix $\text{diag}(1, 1, \dots, 1, -1)$.

Proof: By our assumption and Lemma 6.6.17, $-1 + \gamma_1^2 p = 0$ has a solution $\gamma_1$ in $\mathbb{F}_q$. As \(p \equiv 1 \pmod 4\), \(-1 \in Q_p\). Let \(C_t\) be the even-like subcode of \(\mathcal{D}_t\). Then \(C_{t,\mu-1} = C_t\), and by Theorem 6.4.3, \(C_t^\perp = D_t\) and \(C_t^\perp = D_1\). The result follows as \(\mathbf{1}^I\) is orthogonal to \(\mathbf{1}^D\) because $-1 + \gamma_1^2 p = 0$.

Note that if \(r \neq 2\), there are two solutions \(\gamma\) of \(1 + \gamma^2 p = 0\) over \(\mathbb{F}_q\), one the negative of the other. Similarly \(-1 + \gamma_1^2 p = 0\) has two solutions. We can use either solution to define the extensions. When \(r = 2\), we can always choose \(\gamma = 1\), and hence for the codes over fields of characteristic 2, \(\widehat{\mathcal{D}} = \widehat{\mathcal{D}}\). We see that when \(p \equiv -1 \pmod{12}\), the solution of (6.12) in \(\mathbb{F}_q\) is \(\gamma = 1\) and so here also \(\widehat{\mathcal{D}} = \widehat{\mathcal{D}}\). When \(p \equiv 1 \pmod{12}\), (6.12) has no solution in \(\mathbb{F}_q\) but one solution of \(-1 + \gamma_1^2 p = 0\) in \(\mathbb{F}_q\) is \(\gamma_1 = 1\); thus in this case \(\widehat{\mathcal{D}} = \widehat{\mathcal{D}}\). We now look at the extended codes over fields of characteristic 2 and 3.

## Corollary 6.6.20 Let \(\mathcal{D}_1\) and \(\mathcal{D}_2\) be odd-like QR codes over \(\mathbb{F}_q\) of length \(p\).

- (i) Suppose that \(r = 2\). The following hold:
  - (a) \(\widehat{\mathcal{D}}_i\) is self-dual for \(i = 1\) and \(2\) when \(p \equiv -1 \pmod 8\) or when \(p \equiv 3 \pmod 8\) with \(t\) even.
  - (b) \(\widehat{\mathcal{D}}_1\) and \(\widehat{\mathcal{D}}_2\) are duals of each other when \(p \equiv 1 \pmod 8\) or when \(p \equiv -3 \pmod 8\) with \(t\) even.
- (ii) Suppose that \(r = 3\). The following hold:
  - (a) \(\widehat{\mathcal{D}}_i\) is self-dual for \(i = 1\) and \(2\) when \(p \equiv -1 \pmod{12}\).
  - (b) If \(p \equiv 1 \pmod{12}\), then \(\widehat{\mathcal{D}}_1\) and \(\widehat{\mathcal{D}}_2\) are duals of each other, where \(D\) is the diagonal matrix \(\text{diag}(1, 1, \dots, 1, -1)\).
  - (c) If \(p \equiv -5 \pmod{12}\) with \(t\) even, then \(\widehat{\mathcal{D}}_i\) is self-dual for \(i = 1\) and \(2\), where \(\gamma = \rho^2\) from Table 6.4.
  - (d) If \(p \equiv 5 \pmod{12}\) with \(t\) even, then \(\widehat{\mathcal{D}}_1\) and \(\widehat{\mathcal{D}}_2\) are duals of each other.

## Exercise 369 Explicitly find the solutions of \(1 + \gamma^2 p = 0\) and \(-1 + \gamma_1^2 p = 0\) over \(\mathbb{F}_q\) and \(\mathbb{F}_q\). Then use that information to prove Corollary 6.6.20.

## Exercise 370 Do the following:

- (a) Give the appropriate extended generating idempotents for all odd-like quadratic residue codes of prime length \(p \le 29\) over \(\mathbb{F}_q\). Distinguish between those that arise when \(t\) is even and when \(t\) is odd. Also give the duality relationships between the extended codes. See Exercise 364.
- (b) Give the appropriate extended generating idempotents for all odd-like quadratic residue codes of prime length \(p \le 29\) over \(\mathbb{F}_q\). Distinguish between those that arise when \(t\) is even and when \(t\) is odd. Also give the duality relationships between the extended codes. See Exercise 367.

## 6.6.4 Automorphisms of extended QR codes

In this section, we briefly present information about the automorphism groups of the extended QR codes. Those interested in a complete description of the automorphism groups of the extended QR codes (and extended generalized QR codes) should consult either [147]
