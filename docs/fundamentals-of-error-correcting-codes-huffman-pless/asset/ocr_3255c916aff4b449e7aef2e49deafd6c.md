**Exercise 79** Show that the following codes are perfect:
(a) the codes \(\mathcal{C} = \mathbb{F}_q^n\),
(b) the codes consisting of exactly one codeword (the zero vector in the case of linear codes),
(c) the binary repetition codes of odd length, and
(d) the binary codes of odd length consisting of a vector \(\mathbf{c}\) and the complementary vector \(\overline{\mathbf{c}}\) with 0s and 1s interchanged.
These codes are called trivial perfect codes.

**Exercise 80** Prove that a perfect \(t\)-error-correcting linear code of length \(n\) has precisely \(\binom{n}{i}\) cosets of weight \(i\) for \(0 \le i \le t\) and no other cosets. Hint: How many weight \(i\) vectors in \(\mathbb{F}_q^n\) are there? Could distinct vectors of weights \(i\) and \(j\) with \(i \le t\) and \(j \le t\) be in the same coset? Use the equality in the Sphere Packing Bound.

So the Hamming codes are perfect, as are two of the Golay codes, as shown in Exercise 78. Furthermore, Theorem 1.8.2 shows that all linear codes of the same length, dimension, and minimum weight as a Hamming code are equivalent. Any of these codes can be called Hamming code. There are also some trivial perfect codes as described in Exercise 79. Thus we have part of the proof of the following theorem.

**Theorem 1.12.3**
(i) There exist perfect single error-correcting codes over \(\mathbb{F}_q\) which are not linear and all such codes have parameters corresponding to those of the Hamming codes, namely, length \(n = (q^r - 1)/(q - 1)\) with \(q^{n-r}\) codewords and minimum distance 3. The only single error-correcting linear codes over \(\mathbb{F}_q\) are the Hamming codes.
(ii) The only nontrivial perfect multiple error-correcting codes have the same length, number of codewords, and minimum distance as either the [23, 12, 7] binary Golay code or the [11, 6, 5] ternary Golay code.
(iii) Any binary (respectively, ternary) possibly nonlinear code with \(2^{12}\) (respectively, \(3^6\)) vectors containing the \(\mathbf{0}\) vector with length 23 (respectively, 11) and minimum distance 7 (respectively, 5) is equivalent to the [23, 12, 7] binary (respectively, [11, 6, 5] ternary) Golay code.

The classification of the perfect codes as summarized in this theorem was a significant and difficult piece of mathematics, in which a number of authors contributed. We will prove part (iii) in Chapter 10. The rest of the proof can be found in [137, Section 5]. A portion of part (ii) is proved in Exercise 81.

**Exercise 81** The purpose of this exercise is to prove part of Theorem 1.12.3(ii). Let \(\mathcal{C}\) be an \([n, k, 7]\) perfect binary code.
(a) Using equality in the Sphere Packing Bound, prove that
\((n + 1)(n + 1)^2 - 3(n + 1) + 8] = 3 \cdot 2^{n-k+1}\).
(b) Prove that \(n + 1\) is either \(2^b\) or \(3 \cdot 2^b\) where, in either case, \(b \le n - k + 1\).
(c) Prove that \(b < 4\).