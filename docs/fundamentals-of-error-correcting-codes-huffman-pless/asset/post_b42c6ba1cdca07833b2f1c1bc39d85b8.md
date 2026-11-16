
### Table 6.2 Binary duadic codes of length 119 < n <= 241

| n | d | Comments |
|---|---|---|
| 127 | 15 | ‡ includes punctured Reed-Muller codes |
| 127 | 16 | ‡ |
| 127 | 19 | ‡ includes quadratic residue codes |
| 137 | 21 | ⊗ quadratic residue codes only |
| 151 | 19 | ‡ includes quadratic residue codes |
| 151 | 23 | ‡ |
| 161 | 4 | ‡ |
| 161 | 8 | † |
| 161 | 16 | ‡ |
| 167 | 23 | ‡ quadratic residue codes only |
| 191 | 27 | ‡ quadratic residue codes only |
| 193 | 27 | ⊗ quadratic residue codes only |
| 199 | 31 | ‡ quadratic residue codes only |
| 217 | 4 | ‡ |
| 217 | 8 | † |
| 217 | 12 | ‡ |
| 217 | 16 | † |
| 217 | 20 | ‡ |
| 217 | 24 | † |
| 223 | 31 | ‡ includes quadratic residue codes |
| 233 | 25 | ⊗ quadratic residue codes only |
| 233 | 29 | † |
| 233 | 32 | ⊗ |
| 239 | 31 | ‡ quadratic residue codes only |
| 241 | 25 | ⊗ |
| 241 | 30 | ⊗ |
| 241 | 31 | ⊗ quadratic residue codes only |

Hermitian inner product; see Theorem 6.4.14. At length 21, one of the splittings given by \(\mu_{-1}\) yields odd-like duadic codes whose weight 5 codewords support a projective plane of order 4.

**Exercise 360** Prove that if \(C\) is an \([n, n/2]\) code over \(\mathbb{F}_4\) with a generator matrix consisting of binary vectors, which is self-dual under the ordinary inner product, then \(C\) is also self-dual under the Hermitian inner product. \(\unknown\)

It has been a long-standing open problem to find a better bound than the Square Root Bound, since this seems to be a very weak bound. Additionally, it is not known whether the family of duadic codes over \(\mathbb{F}_q\) is asymptotically good or bad. (See Section 5.1 for the definition of asymptotically good.) Also there is no efficient decoding scheme known for duadic codes. Finding such a scheme would enhance their usefulness greatly. We pose these questions as research problems.

### Table 6.3 Duadic codes over $\mathbb{F}_4$ of length $n \le 41$ (excluding those with binary generating idempotents)

| n | d | \widehat{d} | Number of codes | Comments |
|---|---|---|---|---|
| 3 | 2 | 3 | 2 | ♦ quadratic residue |
| 5 | 3 | 4 | 2 | ♦ quadratic residue |
| 9 | 3 | 3 | 4 | ♥ |
| 11 | 5 | 6 | 2 | ♦ quadratic residue |
| 13 | 5 | 6 | 2 | ♥ quadratic residue |
| 15 | 6 | 7 | 4 | |
| 15 | 6 | 6 | 4 | |
| 15 | 4 | 4 | 4 | |
| 15 | 3 | 3 | 4 | |
| 17 | 7 | 8 | 4 | ♥ |
| 19 | 7 | 8 | 2 | ♦ quadratic residue |
| 21 | 4 | 4 | 4 | ♦ |
| 21 | 5 | 6 | 4 | ♦ projective plane |
| 21 | 6 | 6 | 4 | ♦ |
| 21 | 3 | 3 | 4 | ♦ |
| 25 | 3 | 4 | 4 | ♥ |
| 27 | 3 | 3 | 4 | ♦ |
| 27 | 3 | 3 | 4 | ♦ |
| 29 | 11 | 12 | 2 | ♥ quadratic residue |
| 33 | 3 | 3 | 4 | ♥ |
| 33 | 10 | 10 | 4 | ♦ |
| 33 | 6 | 6 | 4 | ♦ |
| 33 | 8 | 8 | 8 | ♥ |
| 35 | 7 | 8 | 4 | ♥ |
| 35 | 4 | 4 | 4 | ♥ |
| 37 | 11 | 12 | 2 | ♥ quadratic residue |
| 39 | 6 | 6 | 4 | |
| 39 | 3 | 3 | 4 | |
| 39 | 3 | 3 | 4 | |
| 39 | 10 | 11 | 4 | |
| 41 | 11 | 12 | 4 | ♥ |

**Research Problem 6.5.3** Improve the Square Root Bound for either the entire family of duadic codes or the subfamily of quadratic residue codes.

**Research Problem 6.5.4** Decide whether or not the family of duadic codes is asymptotically good or bad.

**Research Problem 6.5.5** Find an efficient decoding scheme for either the entire family of duadic codes or the subfamily of quadratic residue codes.

## 6.6 Quadratic residue codes

In this section we study more closely the family of quadratic residue codes, which, as we have seen, are special cases of duadic codes. These codes, or extensions of them, include the Golay codes and the hexacode. Quadratic residue codes are duadic codes over $\mathbb{F}_p$ of odd prime length $n = p$; by Theorem 6.3.2 $q$ must be a square modulo $n$. Throughout this section, we will let $n = p$ be an odd prime not dividing $q$; we will assume that $q$ is a prime power that is a square modulo $p$. Let $\mathcal{Q}_p$ denote the set of nonzero squares modulo $p$, and let $\mathcal{N}_p$ be the set of nonsquares modulo $p$. The sets $\mathcal{Q}_p$ and $\mathcal{N}_p$ are called the nonzero quadratic residues and the quadratic nonresidues modulo $p$, respectively. We begin with the following elementary lemma.

### **Lemma 6.6.1** Let $p$ be an odd prime. The following hold:
(i) $|\mathcal{Q}_p| = |\mathcal{N}_p| = (p - 1)/2$.
(ii) Modulo $p$, we have $\mathcal{Q}_p a = \mathcal{Q}_p, \mathcal{N}_p a = \mathcal{Q}_p, \mathcal{Q}_p b = \mathcal{N}_p$, and $\mathcal{N}_p b = \mathcal{Q}_p$ when $a \in \mathcal{Q}_p$ and $b \in \mathcal{N}_p$.

**Proof:** The nonzero elements of the field $\mathbb{F}_p^*$, form a cyclic group $\mathbb{F}_p^*$ of even order $p - 1$ with generator $\alpha$. $\mathcal{Q}_p$ is the set of even order elements, that is, $\mathcal{Q}_p = \{\alpha^{2i} \mid 0 \le i < (p - 1)/2\}$; this set forms a subgroup of index 2 in $\mathbb{F}_p^*$. Furthermore $\mathcal{N}_p$ is the coset $\mathcal{Q}_p \alpha$. The results now follow easily.

This lemma implies that the product of two residues or two nonresidues is a residue, while the product of a residue and a nonresidue is a nonresidue; these are facts we use throughout this section (see also Exercise 351). As a consequence of this lemma and Exercise 361, the pair sets $\mathcal{Q}_p$ and $\mathcal{N}_p$ is a splitting of $p$ given by the multiplier $\mu_b$ for any $b \in \mathcal{N}_p$. This splitting determines the defining sets for a pair of even-like duadic codes and a pair of odd-like duadic codes, called the quadratic residue codes or QR codes, of length $p$ over $\mathbb{F}_q$. The odd-like QR codes have defining sets $\mathcal{Q}_p$ and $\mathcal{N}_p$ and dimension $(p + 1)/2$, while the even-like QR codes have defining sets $\mathcal{Q}_p \cup \{0\}$ and $\mathcal{N}_p \cup \{0\}$ and dimension $(p - 1)/2$. This discussion proves the following theorem.

### **Theorem 6.6.2** Quadratic residue codes of odd prime length $p$ exist over $\mathbb{F}_q$ if and only if $q \in \mathcal{Q}_p$.

### **Exercise 361** Prove that if $p$ is an odd prime, $\mathcal{Q}_p$ and $\mathcal{N}_p$ are each unions of $q$-cyclotomic cosets if and only if $q \in \mathcal{Q}_p$.

In the next two subsections, we will present the generating idempotents for the QR codes over fields of characteristic 2 and 3 as described in [274]. The following two theorems will assist us with this classification. The first theorem provides, among other things, a form that an idempotent must have if it is the generating idempotent for a quadratic residue code. In that theorem, we have to distinguish between QR codes and trivial codes. The trivial codes of length $p$ over $\mathbb{F}_q$ are: $\mathbf{0}, \mathbb{F}_q^p$, the even-like subcode $\mathcal{E}_p$ of $\mathbb{F}_q^p$, and the code (1) generated by the all-one codeword. The second theorem will give the generating idempotents of the four QR codes from one of the even-like generators and describe how the generating idempotent of a QR code over some field is related to the generating idempotent of a QR code over an extension field.

### **Theorem 6.6.3** Let $\mathcal{C}$ be a cyclic code of odd prime length $p$ over $\mathbb{F}_q$, where $q$ is a square modulo $p$. Let $e(x)$ be the generating idempotent of $\mathcal{C}$. The following hold:
(i) $\mathcal{C}$ is a quadratic residue code or one of the trivial codes if and only if $e(x)\mu_c = e(x)$ for all $c \in \mathcal{Q}_p$.
(ii) If $\mathcal{C}$ is a quadratic residue code with generating idempotent $e(x)$, then $e(x) = a_0 + a_1 \sum_{i \in \mathcal{Q}_p} x^i + a_2 \sum_{i \in \mathcal{N}_p} x^i$ for some $a_0, a_1$, and $a_2$ in $\mathbb{F}_q$.
(iii) If $c \in \mathcal{Q}_p$ and $\mathcal{C}$ is a quadratic residue code, then $\mu_c \in \text{PAut}(\mathcal{C})$.

**Proof:** The trivial codes $\mathbf{0}, \mathbb{F}_q^p, \mathcal{E}_p, \mathcal{N}_p$ and (1) have defining sets $\{0\} \cup \mathcal{Q}_p \cup \mathcal{N}_p, \emptyset, \{0\}$, and $\mathcal{Q}_p \cup \mathcal{N}_p$, respectively. Let $T$ be the defining set of $\mathcal{C}$. By Theorem 4.3.13 and Corollary 4.4.5, the code $\mathcal{C}_{\mu_c}$ is cyclic with generating idempotent $e(x)\mu_c$ and defining set $c^{-1}T \mod p$. So $e(x)\mu_c = e(x)$ if and only if $cT = T (\mod p)$. Using Lemma 6.6.1, $e(x)\mu_c = e(x)$ for all $c \in \mathcal{Q}_p$ if and only if $T$ is a union of some of $\{0\}, \mathcal{Q}_p$, or $\mathcal{N}_p$. So part (i) follows. Part (ii) follows from (i) and Lemma 6.6.1 as $e(x)^c = e(x)$ for all $c \in \mathcal{Q}_p$. Part (iii) also follows from part (i) because $\mathcal{C}$ and $\mathcal{C}_{\mu_c}$ have the same defining set for $c \in \mathcal{Q}_p$ and hence are equal, implying that $\mu_c \in \text{PAut}(\mathcal{C})$.

### **Theorem 6.6.4** Let $\mathcal{C}$ be an even-like quadratic residue code of prime length $p$ over $\mathbb{F}_q$ with idempotent $e(x)$. The following hold:
(i) The four quadratic residue codes over $\mathbb{F}_q$ or any extension field of $\mathbb{F}_q$ have generating idempotents $e(x)$, $e(x)\mu_b$, $e(x) + \overline{j}(x)$, and $e(x)\mu_b + \overline{j}(x)$ for any $b \in \mathcal{N}_p$.
(ii) $e(x) + e(x)\mu_b = 1 - \overline{j}(x)$ for $b \in \mathcal{N}_p$.
(iii) The four quadratic residue codes over $\mathbb{F}_q$ have the same minimum weight and the same minimum weight codewords, up to scalar multiplication, as they do over an extension field of $\mathbb{F}_q$.

**Proof:** By (6.3) and Theorem 6.1.3, the generating idempotents for the four QR codes over $\mathbb{F}_q$ are as claimed in (i). Because these four idempotents remain idempotents over any extension field of $\mathbb{F}_q$ and are associated with the same splitting of $p$ into residues and nonresidues, they remain generating idempotents of QR codes over any extension field of $\mathbb{F}_q$, completing (i). Part (ii) follows from (6.1), while (iii) follows from Theorem 3.8.8.

Part (i) of this theorem was already illustrated in Example 6.1.9.

## 6.6.1 QR codes over fields of characteristic 2

In this subsection, we will find the generating idempotents of all the QR codes over any field of characteristic 2. We will see that we only have to look at the generating idempotents of QR codes over $\mathbb{F}_2$ and $\mathbb{F}_4$.
