
## Exercise 79

Show that the following codes are perfect:

- (a) the codes \(\mathcal{C} = \mathbb{F}_q^n\),
- (b) the codes consisting of exactly one codeword (the zero vector in the case of linear codes),
- (c) the binary repetition codes of odd length, and
- (d) the binary codes of odd length consisting of a vector \(\mathbf{c}\) and the complementary vector \(\overline{\mathbf{c}}\) with 0s and 1s interchanged.

These codes are called trivial perfect codes.

## Exercise 80

Prove that a perfect \(t\)-error-correcting linear code of length \(n\) has precisely \(\binom{n}{i}\) cosets of weight \(i\) for \(0 \le i \le t\) and no other cosets. Hint: How many weight \(i\) vectors in \(\mathbb{F}_q^n\) are there? Could distinct vectors of weights \(i\) and \(j\) with \(i \le t\) and \(j \le t\) be in the same coset? Use the equality in the Sphere Packing Bound.

So the Hamming codes are perfect, as are two of the Golay codes, as shown in Exercise 78. Furthermore, Theorem 1.8.2 shows that all linear codes of the same length, dimension, and minimum weight as a Hamming code are equivalent. Any of these codes can be called Hamming code. There are also some trivial perfect codes as described in Exercise 79. Thus we have part of the proof of the following theorem.

## Theorem 1.12.3

- (i) There exist perfect single error-correcting codes over \(\mathbb{F}_q\) which are not linear and all such codes have parameters corresponding to those of the Hamming codes, namely, length \(n = (q^r - 1)/(q - 1)\) with \(q^{n-r}\) codewords and minimum distance 3. The only single error-correcting linear codes over \(\mathbb{F}_q\) are the Hamming codes.
- (ii) The only nontrivial perfect multiple error-correcting codes have the same length, number of codewords, and minimum distance as either the [23, 12, 7] binary Golay code or the [11, 6, 5] ternary Golay code.
- (iii) Any binary (respectively, ternary) possibly nonlinear code with \(2^{12}\) (respectively, \(3^6\)) vectors containing the \(\mathbf{0}\) vector with length 23 (respectively, 11) and minimum distance 7 (respectively, 5) is equivalent to the [23, 12, 7] binary (respectively, [11, 6, 5] ternary) Golay code.

The classification of the perfect codes as summarized in this theorem was a significant and difficult piece of mathematics, in which a number of authors contributed. We will prove part (iii) in Chapter 10. The rest of the proof can be found in [137, Section 5]. A portion of part (ii) is proved in Exercise 81.

## Exercise 81

The purpose of this exercise is to prove part of Theorem 1.12.3(ii). Let \(\mathcal{C}\) be an \([n, k, 7]\) perfect binary code.

- (a) Using equality in the Sphere Packing Bound, prove that
  \((n+1)[(n+1)^2 - 3(n+1) + 8] = 3 \cdot 2^{n-k+1}\).
- (b) Prove that \(n + 1\) is either \(2^b\) or \(3 \cdot 2^b\) where, in either case, \(b \le n - k + 1\).
- (c) Prove that \(b < 4\).
- (d) Prove that \(n = 23\) or \(n = 7\).
- (e) Name two codes that are perfect \([n, k, 7]\) codes, one with \(n = 7\) and the other with \(n = 23\).

One can obtain nonlinear perfect codes by taking a coset of a linear perfect code; see Exercise 82. Theorem 1.12.3 shows that all multiple error-correcting nonlinear codes are cosets of the binary Golay code of length 23 or the ternary Golay code of length 11. On the other hand, there are nonlinear single error-correcting codes which are not cosets of Hamming codes; these were first constructed by Vasil'ev [338].

## Exercise 82

Prove that a coset of a linear perfect code is also a perfect code.

Let \(C\) be an \([n, k, d]\) code over \(\mathbb{F}_q\) and let \(t = \lfloor (d - 1)/2 \rfloor\). When you do not have a perfect code, in order to fill the space \(\mathbb{F}_q^n\) with spheres centered at codewords, the spheres must have radius larger than \(t\). Of course when you increase the sphere size, not all spheres will be pairwise disjoint. We define the covering radius \(\rho(C)\) to be the smallest integer \(s\) such that \(\mathbb{F}_q^n\) is the union of the spheres of radius \(s\) centered at the codewords of \(C\). Equivalently,

\[
\rho(C) = \max_{\mathbf{x} \in \mathbb{F}_q^n} \min_{\mathbf{c} \in C} d(\mathbf{x}, \mathbf{c}).
\]

Obviously, \(t \le \rho(C)\) and \(t = \rho(C)\) if and only if \(C\) is perfect. By Theorem 1.1.14, the packing radius of a code is the largest radius of spheres centered at codewords so that the spheres are disjoint. So a code is perfect if and only if its covering radius equals its packing radius. If the code is not perfect, its covering radius is larger than its packing radius. For a nonlinear code \(C\), the covering radius \(\rho(C)\) is defined in the same way to be

\[
\rho(C) = \max_{\mathbf{x} \in \mathbb{F}_q^n} \min_{\mathbf{c} \in C} d(\mathbf{x}, \mathbf{c}).
\]

Again if \(d\) is the minimum distance of \(C\) and \(t = \lfloor (d - 1)/2 \rfloor\), then \(t \le \rho(C)\) and \(t = \rho(C)\) if and only if \(C\) is perfect. The theorems that we prove later in this section are only for linear codes.

If \(C\) is a code with packing radius \(t\) and covering radius \(t + 1\), \(C\) is called quasi-perfect. There are many known linear and nonlinear quasi-perfect codes (e.g. certain double error-correcting BCH codes and some punctured Preparata codes). However, unlike perfect codes, there is no general classification.

## Example 1.12.4

By Exercise 56, the binary \([8, 4, 4]\) code is shown to be unique, in the sense that all such codes are equivalent to \(\tilde{\mathcal{H}}_8\). In Example 1.1.17, we give the complete coset weight distribution of this code. Since there are no cosets of weight greater than 2, the covering radius, \(\rho(\tilde{\mathcal{H}}_8)\), is 2. Since the packing radius is \(t = \lfloor (4 - 1)/2 \rfloor = 1\), this code is quasi-perfect. Both the covering and packing radius of the nonextended Hamming code \(\tilde{\mathcal{H}}_7\) equals 1. This is an illustration of the fact that extending a binary code will not increase its packing radius (error-correcting capability) but will increase its covering radius. See Theorem 1.12.6(v) below.

Recall that the weight of a coset of a code \(C\) is the smallest weight of a vector in the coset. The definition of the covering radius implies the following characterization of the covering radius of a linear code in terms of coset weights and in terms of syndromes.

## Theorem 1.12.5

Let \(C\) be a linear code with parity check matrix \(H\). Then:

- (i) \(\rho(C)\) is the weight of the coset of largest weight;
- (ii) \(\rho(C)\) is the smallest number \(s\) such that every nonzero syndrome is a combination of \(s\) or fewer columns of \(H\), and some syndrome requires \(s\) columns.

## Exercise 83

Prove Theorem 1.12.5. \(\blacklozenge\)

We conclude this chapter by collecting some elementary facts about the covering radius of codes and coset leaders, particularly involving codes arising in Section 1.5. More on covering radius can be found in Chapter 11.

## Theorem 1.12.6

Let \(C\) be an \([n, k]\) code over \(\mathbb{F}_q\). Let \(\widehat{C}\) be the extension of \(C\), and let \(C^*\) be a code obtained from \(C\) by puncturing on some coordinate. The following hold:

- (i) If \(C = C_1 \oplus C_2\), then \(\rho(C) = \rho(C_1) + \rho(C_2)\).
- (ii) \(\rho(C^*) = \rho(C)\) or \(\rho(C^*) = \rho(C) - 1\).
- (iii) \(\rho(\widehat{C}) = \rho(C)\) or \(\rho(\widehat{C}) = \rho(C) + 1\).
- (iv) If \(q = 2\), then \(\rho(\widehat{C}) = \rho(C) + 1\).
- (v) Assume that \(x\) is a coset leader of \(C\). If \(x^* \in \mathbb{F}_q^n\) all of whose nonzero components agree with the same components of \(x\), then \(x^*\) is also a coset leader of \(C\). In particular, if there is a coset of weight \(s\), there is also a coset of any weight less than \(s\).

Proof. The proofs of the first three assertions are left as exercises. For (iv), let \(x = x_1 \cdots x_n\) be a coset leader of \(C\). Let \(x^* = x_1 \cdots x_n\). By part (iii), it suffices to show that \(x^*\) is a coset leader of \(\widehat{C}\). Let \(c = c_1 \cdots c_n \in C\), and let \(\widehat{c} = c_1 \cdots c_n c_{n+1}\) be its extension. If \(c\) has even weight, then \(\mathrm{wt}(\widehat{c} + x^*) = \mathrm{wt}(c + x) + 1 \ge \mathrm{wt}(x) + 1\). Assume \(c\) has odd weight. Then \(\mathrm{wt}(\widehat{c} + x^*) = \mathrm{wt}(c + x)\). If \(x\) has even (odd) weight, then \(c + x\) has odd (even) weight by Theorem 1.4.3, and so \(\mathrm{wt}(c + x) > \mathrm{wt}(x)\) as \(x\) is a coset leader. Thus in all cases, \(\mathrm{wt}(\widehat{c} + x^*) \ge \mathrm{wt}(x) + 1 = \mathrm{wt}(x^*)\) and so \(x^*\) is a coset leader of \(\widehat{C}\).

To prove (v), it suffices, by induction, to verify the result when \(x = x_1 \cdots x_n\) is a coset leader and \(x^* = x^*_1 \cdots x^*_n\), where \(x_j = x^*_j\) for all \(j \ne i\) and \(x_i \ne x^*_i\). Notice that \(\mathrm{wt}(x^*) = \mathrm{wt}(x) + 1\). Suppose that \(x^*\) is not a coset leader. Then there is a codeword \(c \in C\) such that \(x^* + c\) is a coset leader and hence

\[
\mathrm{wt}(x + c) \le \mathrm{wt}(x^*) - 1 = \mathrm{wt}(x) - 2. \tag{1.13}
\]

But as \(x\) and \(x^*\) disagree in only one coordinate, \(\mathrm{wt}(x + c) \le \mathrm{wt}(x^* + c) + 1\). Using (1.13), this implies that \(\mathrm{wt}(x + c) \le \mathrm{wt}(x) - 1\), a contradiction as \(x\) is a coset leader. \(\square\)

## Exercise 84

Prove parts (i), (ii), and (iii) of Theorem 1.12.6. \(\blacklozenge\)

The next example illustrates that it is possible to extend or puncture a code and leave the covering radius unchanged. Compare this to Theorem 1.12.6(ii) and (iii).
