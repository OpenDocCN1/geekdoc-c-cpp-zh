in Example 2.3.10 or the punctured Preparata codes in Example 2.3.11, and that all nearly perfect nonbinary codes must be perfect.

# ## 2.4 The Singleton Upper Bound and MDS codes

The next upper bound for \(A_q(n, d)\) and \(B_q(n, d)\), called the Singleton Bound, is much simpler to prove than the previous upper bounds. It is a rather weak bound in general but does lead to the class of codes called MDS codes; this class contains the very important family of codes known as Reed-Solomon codes, which are generally very useful in many applications. They correct burst errors and provide the high fidelity in CD players.

**Theorem 2.4.1 (Singleton Bound [312])** For \(d \le n\), \(A_q(n, d) \le q^{n-d+1}\). Furthermore if an \([n, k, d]\) linear code over \(\mathbb{F}_q\) exists, then \(k \le n - d + 1\).

**Proof:** The second statement follows from the first by Theorem 2.1.1. Recall that \(A_q(n, n) = q\) by Theorem 2.1.5 yielding the bound when \(d = n\). Now assume that \(d < n\). By Theorem 2.1.6 \(A_q(n, d) \le q A_q(n - 1, d)\). Inductively we have that \(A_q(n, d) \le q^{n-d} A_q(d, d)\). Since \(A_q(d, d) = q\), \(A_q(n, d) \le q^{n-d+1}\).

**Example 2.4.2** The hexacode of Example 1.3.4 is a \((6, 3, 4)\) linear code over \(\mathbb{F}_4\). In this code, \(k = 3 = 6 - 4 + 1 = n - d + 1\) and the Singleton Bound is met. So \(A_4(6, 4) = 4^3\).

**Exercise 111** Prove using either the parity check matrix or the standard form of the generator matrix for an \([n, k, d]\) linear code that \(d \le n - k + 1\), hence verifying directly the linear version of the Singleton Bound.

A code for which equality holds in the Singleton Bound is called *maximum distance separable*, abbreviated *MDS*. No code of length \(n\) and minimum distance \(d\) has more codewords than an MDS code with parameters \(n\) and \(d\); equivalently, no code of length \(n\) with \(M\) codewords has a larger minimum distance than an MDS code with parameters \(n\) and \(M\). We briefly discuss some results on linear MDS codes.

**Theorem 2.4.3** Let \(\mathcal{C}\) be an \([n, k]\) code over \(\mathbb{F}_q\) with \(k \ge 1\). Then the following are equivalent: (i) \(\mathcal{C}\) is MDS. (ii) Every set of \(k\) coordinates is an information set for \(\mathcal{C}\). (iii) \(\mathcal{C}^\perp\) is MDS. (iv) Every set of \(n - k\) coordinates is an information set for \(\mathcal{C}^\perp\).

**Proof:** The first two statements are equivalent by Theorem 1.4.15 as an \([n, k]\) code is MDS if and only if \(k = n - d + 1\). Similarly the last two are equivalent. Finally, (ii) and (iv) are equivalent by Theorem 1.6.2.