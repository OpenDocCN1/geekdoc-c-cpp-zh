
for some polynomial \(a(x)\). Multiply (5.13) by \(\sigma(x)\) and (5.14) by \(b_I(x)\) to obtain

\(a_I(x)\sigma(x)^{2^l} + b_I(x)\sigma(x)S(x) = r_I(x)\sigma(x)\) and
\(a(x)b_I(x)^{2^l} + \sigma(x)b_I(x)S(x) = \omega(x)b_I(x).\) (5.15) (5.16)

Modulo \(x^{2^l}\) these imply that

\(r_I(x)\sigma(x) \equiv \omega(x)b_I(x) \pmod{x^{2^l}}.\) (5.17)

As \(\deg \sigma(x) \le t\), by the choice of \(I\), \(\deg(r_I(x)\sigma(x)) = \deg r_I(x) + \deg \sigma(x) < t + t = 2t\). By Lemma 5.4.11(iv), the choice of \(I\), and the fact that \(\deg \omega(x) < t\), \(\deg(\omega(x) \times b_I(x)) = \deg \omega(x) + \deg b_I(x) < t + \deg b_I(x) = t + (\deg x^{2^l} - \deg r_{I-1}(x)) \le 3t - t = 2t\). Therefore (5.17) implies that \(r_I(x)\sigma(x) = \omega(x)b_I(x)\). This, together with (5.15) and (5.16), shows that

\(a_I(x)\sigma(x) = a(x)b_I(x).\) (5.18)

However, Lemma 5.4.11(iii) implies that \(a_I(x)\) and \(b_I(x)\) are relatively prime and hence \(a(x) = \lambda(x)a_I(x)\) by (5.18). Substituting this into (5.18) produces

\(\sigma(x) = \lambda(x)b_I(x).\) (5.19)

Plugging these into (5.14) we obtain \(\lambda(x)a_I(x)x^{2^l} + \lambda(x)b_I(x)S(x) = \omega(x)\). Thus (5.13) implies that

\(\omega(x) = \lambda(x)r_I(x).\) (5.20)

By Lemma 5.4.10, (5.19), and (5.20), \(\lambda(x)\) must be a nonzero constant, verifying Step III of the Sugiyama Algorithm.

Since we are only interested in the roots of \(\sigma(x)\), it suffices to find the roots of \(b_I(x)\) produced in Step II; this gives the desired error location numbers.

**Example 5.4.12** We obtain a scalar multiple of \(\sigma(x)\) from Example 5.4.3, using the Sugiyama Algorithm and Table 5.1. In that example \(t = 2\), and the syndromes are \(S_1 = \alpha^2\), \(S_2 = \alpha^4\), \(S_3 = \alpha^{11}\), and \(S_4 = \alpha^8\). The following table summarizes the results.

| i | r_I(x) | h_I(x) | b_I(x) |
|---|---|---|---|
| -1 | x^4 | | 0 |
| 0 | \alpha^8x^3 + \alpha^{11}x^2 + \alpha^4x + \alpha^2 | | 1 |
| 1 | \alpha x^2 + \alpha^4x + \alpha^{12} | \alpha^7x + \alpha^{10} | \alpha^7x + \alpha^{10} |
| 2 | \alpha^2 | \alpha^7x | \alpha^{14}x^2 + \alpha^2x + 1 |

The first index \(I\) where \(\deg r_I(x) < t = 2\) is \(I = 2\). Hence \(\sigma(x)\) is a multiple of \(b_2(x) = \alpha^{14}x^2 + \alpha^2x + 1\); in fact from Example 5.4.3, \(b_2(x) = \sigma(x)\).

**Example 5.4.13** Using the Sugiyama Algorithm we examine Example 5.4.4 where \( t = 2 \), \( S_1 = S_2 = S_4 = 0 \), and \( S_5 = \alpha^{10} \). The following table summarizes the computations.

| i | r_i(x) | h_i(x) | b_i(x) |
|---|---|---|---|
| -1 | x^4 | | 0 |
| 0 | \alpha^{10} x^2 | | 1 |
| 1 | 0 | \alpha^5 x^2 | \alpha^5 x^2 |

The first index \( I \) where \( \deg r_I(x) < t = 2 \) is \( I = 1 \). But in this case \( b_1(x) = \alpha^5 x^2 \), which has 0 for its roots indicating that more than two errors were made, in agreement with Example 5.4.4. Note also that \( r_1(x) = 0 \) implies by (5.20) that \( \omega(x) = 0 \), which is obviously impossible as \( \sigma(x) \) and \( \omega(x) \) are supposed to be relatively prime by Lemma 5.4.10.

**Example 5.4.14** We obtain a scalar multiple of \( \sigma(x) \) from Example 5.4.5 using the Sugiyama Algorithm. Here \( t = 3 \) and \( S_1 = \alpha^{14} \), \( S_2 = \alpha^{13} \), \( S_3 = \alpha^{14} \), \( S_4 = \alpha^{11} \), \( S_5 = 1 \), and \( S_6 = \alpha^{13} \). The following table summarizes the results.

| i | r_i(x) | h_i(x) | b_i(x) |
|---|---|---|---|
| -1 | x^5 | | 0 |
| 0 | \alpha^{13} x^5 + x^4 + \alpha^{11} x^3 + \alpha^4 x^2 + \alpha^{13} x + \alpha^4 | | 1 |
| 1 | \alpha^{11} x^4 + \alpha^4 x^3 + \alpha^{14} x^2 + \alpha x + \alpha^3 | \alpha^2 x + \alpha^4 | \alpha^2 x + \alpha^4 |
| 2 | \alpha^{12} | \alpha^2 x + \alpha^2 | \alpha^4 x^2 + \alpha^{12} x + \alpha^{13} |

The first index \( I \) where \( \deg r_I(x) < t = 3 \) is \( I = 2 \). Hence \( \sigma(x) \) is a multiple of \( b_2(x) = \alpha^4 x^2 + \alpha^{12} x + \alpha^{13} \). From Example 5.4.5, \( \sigma(x) = \alpha^2 b_2(x) \).

- Exercise 305 Verify the calculations in Examples 5.4.12, 5.4.13, and 5.4.14.

- Exercise 306 Using the Sugiyama Algorithm, find a scalar multiple of the error locator polynomial from Example 5.4.6.

- Exercise 307 Using the Sugiyama Algorithm, find scalar multiples of the error locator polynomials from Exercise 299.

- Exercise 308 Using the Sugiyama Algorithm, find scalar multiples of the error locator polynomials from Exercise 300.

- Exercise 309 Using the Sugiyama Algorithm, find scalar multiples of the error locator polynomials from Exercise 301.

We remark that the Sugiyama Algorithm applies with other choices for \( f(x) \) and \( s(x) \), with an appropriate modification of the condition under which the algorithm stops in Step II. Such modification works for decoding Goppa codes; see [232].

It is worth noting that the Peterson–Gorenstein–Zierler, the Berlekamp–Massey, or the Sugiyama Algorithm can be used to decode any cyclic code up to the BCH Bound. Let \( C \) be a cyclic code with defining set \( T \) and suppose that \( T \) contains \( \delta \) consecutive elements \( \{b, b+1, \dots, b+\delta-2\} \). Let \( B \) be the BCH code with defining set \( C_b \cup C_{b+1} \cup \dots \cup C_{b+\delta-2} \), which is a subset of \( T \). By Exercise 239, \( C \subseteq B \). Let \( t = \lfloor (\delta-1)/2 \rfloor \). Suppose that a codeword \(c(x) \in \mathcal{C}\) is transmitted and \(y(x)\) is received where \(t\) or fewer errors have been made. Then \(c(x) \in \mathcal{B}\) and any of the decoding algorithms applied to \(\mathcal{B}\) will correct \(y(x)\) and produce \(c(x)\). Thus these algorithms will correct a received word in any cyclic code provided that if errors are made, \(2t + 1\) does not exceed the BCH Bound of the code. Of course this number of errors may be less than the actual number of errors that \(\mathcal{C}\) is capable of correcting.

## 5.4.4 The Sudan–Guruswami Decoding Algorithm

In a 1997 paper Madhu Sudan [323] developed a procedure for decoding \([n, k, d]\) Reed–Solomon codes that is capable of correcting some \(e\) errors where \(e > (d - 1)/2\). This method was extended by Guruswami and Sudan [113] to remove certain restrictions in the original Sudan Algorithm. To be able to correct \(e\) errors where \(e > (d - 1)/2\), the algorithm produces a list of all possible codewords within Hamming distance \(e\) of any received vector; such an algorithm is called a *list-decoding algorithm*. The Sudan–Guruswami Algorithm applies to generalized Reed–Solomon codes as well as certain BCH and algebraic geometry codes. In this section we present this algorithm for generalized Reed–Solomon codes and refer the interested reader to [113] for the other codes. The Sudan–Guruswami Algorithm has itself been generalized by Kötter and Vardy [179] to apply to soft decision decoding.

To prepare for the algorithm we need some preliminary notation involving polynomials in two variables. Suppose \(x\) and \(y\) are independent indeterminates and \(p(x, y) = \sum \sum p_{i,j} x^i y^j\) is a polynomial in \(\mathbb{F}_q[x, y]\), the ring of all polynomials in the two variables \(x\) and \(y\). Let \(w_x\) and \(w_y\) be nonnegative real numbers. The \((w_x, w_y)\)-weighted degree of \(p(x, y)\) is defined to be

\(\max\{w_x i + w_y j \mid p_{i,j} \neq 0\}.\)

Notice that the \((1, 1)\)-weighted degree of \(p(x, y)\) is merely the degree of \(p(x, y)\). For positive integers \(s\) and \(\delta\), let \(N_s(\delta)\) denote the number of monomials \(x^i y^j\) whose \((1, s)\)-weighted degree is \(s\) or less. We say that the point \((\alpha, \beta) \in \mathbb{F}_q^2\) *lies on* or *is a root* of \(p(x, y)\) provided \(p(\alpha, \beta) = 0\). We will need the multiplicity of this root. To motivate the definition of multiplicity, recall that if \(f(x) \in \mathbb{F}_q[x]\) and \(\alpha\) is a root of \(f(x)\), then its multiplicity as a root of \(f(x)\) is the number \(m\) where \(f(x) = (x - \alpha)^m g(x)\) for some \(g(x) \in \mathbb{F}_q[x]\) with \(g(\alpha) \neq 0\). When working with two variables we cannot generalize this notation directly. Notice, however, that \(f(x + \alpha) = x^m h(x)\), where \(h(x) = g(x + \alpha)\); also \(h(0) \neq 0\). In particular \(f(x + \alpha)\) contains a monomial of degree \(m\) but none of smaller degree. This concept can be generalized. The root \((\alpha, \beta)\) of the polynomial \(p(x, y)\) has multiplicity \(m\) provided the shifted polynomial \(p(x + \alpha, y + \beta)\) contains a monomial of degree \(m\) but no monomial of lower degree.

**Exercise 310** Let \(p(x, y) = 1 + x + y - x^2 - y^2 - 2x^2y + xy^2 - y^3 + x^4 - 2x^3y - x^2y^2 + 2xy^3 \in \mathbb{F}_5[x]\). Show that \((1, 2) \in \mathbb{F}_5^2\) is a root of \(p(x, y)\) with multiplicity 3.
