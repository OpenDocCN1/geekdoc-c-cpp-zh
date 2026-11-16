
From Exercise 819, one can check relatively easily to see if a generator matrix for an \((n, 1)\) convolutional code is canonical or not. The process is not so clear for \((n, k)\) codes with \(k > 1\). It turns out (see Theorem 14.3.7) that a generator matrix is canonical if it is both basic and reduced, terms requiring more notation.

Let \(G\) be a \(k \times n\) polynomial matrix with \(k \le n\). A \(k \times k\) minor of \(G\) is the determinant of a matrix consisting of \(k\) columns of \(G\), \(G\) has \(\binom{n}{k}\) minors. The internal degree of \(G\), denoted \(\text{indeg } G\), is the maximum degree of all of the \(k \times k\) minors of \(G\). A basic polynomial generator matrix of a convolutional code is any polynomial generator matrix of minimal internal degree.

## Exercise 820
Find the internal degree of each matrix \(G_1, G'_1, G_2, G'_2, G''_2\), and \(G'''_2\) from Example 14.1.1. Notice that the internal degrees are always less than or equal to the external degrees found in Example 14.3.1 and Exercise 818.

A \(k \times k\) matrix \(U\) with entries in \(\mathbb{F}_2[D]\) (that is, polynomials in \(D\)) is *unimodular* if its determinant is 1. A polynomial matrix \(G\) is *reduced* if among all polynomial matrices of the form \(UG\), where \(U\) is a \(k \times k\) unimodular matrix, \(G\) has the smallest external degree. Since a unimodular matrix can be shown to be a product of elementary matrices, a matrix is reduced if and only if its external degree cannot be reduced by applying a sequence of elementary row operations to the matrix.

In [235], six equivalent formulations are given for a matrix to be basic and three are given for a matrix to be reduced. We present some of these equivalent statements here, omitting the proofs and referring the interested reader to [235, Appendix A].

## Theorem 14.3.3
Let \(G\) be a polynomial generator matrix of an \((n, k)\) convolutional code. The matrix \(G\) is basic if and only if any of the following hold.
- (i) The greatest common divisor of the \(k \times k\) minors of \(G\) is 1.
- (ii) There exists an \(n \times k\) matrix \(K\) with polynomial entries so that \(GK = I_k\).
- (iii) If \(\mathbf{c} \in \mathbb{F}_2[D]^n\) and \(\mathbf{c} = \mathbf{x}G\), then \(\mathbf{x} \in \mathbb{F}_2[D]^k\).

Recall that the matrix \(K\) in (ii) is a right inverse of \(G\). Part (iii) of Theorem 14.3.3 states that if \(G\) is a basic encoder, then whenever the output is polynomial, so is the input. In Section 14.5, we will examine the situation where (iii) fails, namely where there is a polynomial output that comes from a non-polynomial input. Note that the proof that (ii) implies (iii) is simple. If (ii) holds and \(\mathbf{c} = \mathbf{x}G\), then \(\mathbf{x} = \mathbf{x}I_k = \mathbf{x}GK = \mathbf{c}K\); as \(\mathbf{c}\) and \(K\) have only polynomial entries, so does \(\mathbf{x}\).

The degree of a vector \(\mathbf{v}(D) \in \mathbb{F}[D]^l\) is the largest degree of any of its components. Note that this definition is consistent with the definition of "degree" for a matrix given in (14.4).

## Theorem 14.3.4
Let \(G\) be a \(k \times n\) polynomial matrix. Let \(\mathbf{g}_i(D)\) be the \(i\)th row of \(G\). The matrix \(G\) is *reduced* if and only if either of the following hold.
- (i) \(\text{indeg } G = \text{outdeg } G\).
- (ii) For any \(\mathbf{x}(D) = (x_1(D), \dots, x_k(D)) \in \mathbb{F}_2[D]^k\),
  \[
  \deg(\mathbf{x}(D)G) = \max_{1 \le i \le k} (\deg x_i(D) + \deg \mathbf{g}_i(D)).
  \]

Part (ii) is called the *predictable degree property* of reduced matrices.

## Example 14.3.5
Notice that Exercise 819 shows that a polynomial generator matrix of an \((n, 1)\) convolutional code is canonical if and only if it is basic. If \(G\) is any \(1 \times n\) polynomial matrix, then the \(1 \times 1\) minors of \(G\) are precisely the polynomial entries of the matrix. So \(G\) is reduced by Theorem 14.3.4. This shows that for an \((n, 1)\) code, a polynomial generator matrix is canonical if and only if it is basic and reduced.

We wish to show in general that a polynomial generator matrix for any \((n, k)\) convolutional code is canonical if and only if it is basic and reduced. Exercise 820 hints at part of the following, which will be necessary for our result.

## Lemma 14.3.6
Let \(G\) be a \(k \times n\) polynomial matrix over \(\mathbb{F}_2[D]\) with \(k \le n\). Let \(N\) be a nonsingular \(k \times k\) polynomial matrix with entries in \(\mathbb{F}_2[D]\). The following hold:
- (i) \(\text{indeg } NG = \text{indeg } G + \deg \det N\).
- (ii) \(\text{indeg } G \le \text{indeg } NG\). Equality holds if and only if \(N\) is unimodular.
- (iii) \(\text{indeg } G \le \text{extdeg } G\).

**Proof:** To prove (i), we observe that the \(k \times k\) submatrices of \(NG\) are precisely the \(k \times k\) minors of \(G\) each multiplied on the left by \(N\). Thus the \(k \times k\) minors of \(NG\) are exactly the \(k \times k\) minors of \(G\) each multiplied by \(\det N\). This proves (i). Part (ii) follows from (i). For (iii), suppose the degree of the \(i\)th row of \(G\) is \(m_i\). Then \(\text{extdeg } G = m_1 + m_2 + \cdots + m_k\). Any \(k \times k\) minor of \(G\) is a sum of products of entries of \(G\) with one factor in each product from each row. Hence the highest degree product is at most \(m_1 + m_2 + \cdots + m_k\), implying that this is the maximum degree of the minor. Thus \(\text{indeg } G \le \text{extdeg } G\).

## Theorem 14.3.7
A polynomial generator matrix of an \((n, k)\) convolutional code \(\mathcal{C}\) is canonical if and only if it is basic and reduced.

**Proof:** Let \(G\) be a canonical generator matrix for \(\mathcal{C}\). Since the basic generator matrices have a common internal degree, let this degree be \(d_0\). Choose from among the basic generator matrices a matrix \(G_0\) whose external degree is as small as possible. If \(U\) is any unimodular matrix, then \(\text{indeg } UG_0 = \text{indeg } G_0 = d_0\) by Lemma 14.3.6(ii). By definition of \(G_0\), \(\text{extdeg } UG_0 \ge \text{extdeg } G_0\) (as \(UG_0\) generates \(\mathcal{C}\)), implying that \(G_0\) is reduced. Since \(G_0\) has the smallest possible internal degree of any polynomial generator matrix of \(\mathcal{C}\), \(\text{indeg } G_0 \le \text{indeg } G\). But \(\text{indeg } G \le \text{extdeg } G\) by Lemma 14.3.6(iii) and \(\text{extdeg } G \le \text{extdeg } G_0\) by definition as \(G\) is canonical. Thus

\[
\text{indeg } G_0 \le \text{indeg } G \le \text{extdeg } G \le \text{extdeg } G_0. \quad (14.5)
\]

As \(G_0\) is reduced, \(\text{indeg } G_0 = \text{extdeg } G_0\) by Theorem 14.3.4(i). Therefore we have equality everywhere in (14.5). Thus \(\text{indeg } G = \text{indeg } G_0 = d_0\) showing that \(G\) has minimal internal degree among all polynomial generator matrices of \(\mathcal{C}\), implying that \(G\) is basic also. As \(\text{indeg } G = \text{extdeg } G\), \(G\) is reduced by Theorem 14.3.4(i).

Now suppose that \(G\) is both a basic and a reduced polynomial matrix of \(\mathcal{C}\).

Let \(G_0\) be any other polynomial generator matrix of \(\mathcal{C}\). By Lemma 14.3.6, \(\text{extdeg } G_0 \ge \text{indeg } G_0\). Since \(G\) is basic, \(\text{indeg } G_0 \ge \text{indeg } G\). As \(G\) is reduced, \(\text{indeg } G = \text{extdeg } G\) by Theorem 14.3.4(i). By combining these inequalities, \(\text{extdeg } G_0 \ge \text{extdeg } G\) implying that \(G\) is canonical.

## Exercise 821
Which of the polynomial generator matrices \(G_2, G'_2, G''_2,\) and \(G'''_2\) of the \((4, 2)\) convolutional code \(\mathcal{C}_2\) from Example 14.1.1 are basic? Which are reduced? Which are canonical?

The proof of Theorem 14.3.7 shows that the minimal internal degree of any polynomial generator matrix of an \((n, k)\) convolutional code \(\mathcal{C}\) is also the minimal external degree of any polynomial generator matrix of \(\mathcal{C}\), that is, the sum of the row degrees of a canonical generator matrix. Amazingly, the set of row degrees is unique for a canonical generator matrix. To prove this, we need the following lemma.

## Lemma 14.3.8
Let \(G\) be a canonical generator matrix for an \((n, k)\) convolutional code \(\mathcal{C}\). Reorder the rows of \(G\) so that the row degrees satisfy \(m_1 \le m_2 \le \cdots \le m_k\), where \(m_i\) is the degree of the \(i\)th row. Let \(G'\) be any polynomial generator matrix for \(\mathcal{C}\). Analogously reorder its rows so that its row degrees \(m'_i\) satisfy \(m'_1 \le m'_2 \le \cdots \le m'_k\). Then \(m_i \le m'_i\) for \(1 \le i \le k\).

**Proof.** Let \(\mathbf{g}_i(D)\) be the \(i\)th row of \(G\) with \(\deg \mathbf{g}_i(D) = m_i\). Analogously let \(\mathbf{g}'_i(D)\) be the \(i\)th row of \(G'\) with \(\deg \mathbf{g}'_i(D) = m'_i\). Suppose the result is false. Then there exists an integer \(j\) such that \(m_1 \le m'_1, \dots, m_j \le m'_j\) but \(m_{j+1} > m'_{j+1}\). Let \(1 \le i \le j + 1\). Then \(\deg \mathbf{g}_i(D) < m_{j+1}\). Since \(\mathbf{g}_i(D)\) is a polynomial codeword, that is, a “polynomial output,” and \(G\) is basic, there exists a “polynomial input” \(\mathbf{x}_i(D) = (x_{i1}(D), \dots, x_{ik}(D))\) such that \(\mathbf{g}'_i(D) = \mathbf{x}_i(D)G\) by Theorem 14.3.3(ii). As \(G\) is also reduced, the “predictable degree property” of Theorem 14.3.4(ii) implies that:

\[
m'_i = \deg \mathbf{g}'_i(D) = \deg(\mathbf{x}_i(D)G) = \max_{1 \le \ell \le k} (\deg x_{i\ell}(D) + \deg \mathbf{g}_\ell(D))
\]

\[
= \max_{1 \le \ell \le k} (\deg x_{i\ell}(D) + m_\ell).
\]

As \(\deg \mathbf{g}_i(D) < m_{j+1}\), this implies that \(\deg x_{i\ell}(D) = -\infty\) for \(\ell \ge j + 1\). In other words \(x_{i\ell}(D) = 0\) for \(\ell \ge j + 1\). Since \(\mathbf{g}'_i(D) = \mathbf{x}_i(D)G\), \(\mathbf{g}'_i(D)\) must be a polynomial combination of the first \(j\) rows of \(G\) for \(1 \le i \le j + 1\). Hence the first \(j + 1\) rows of \(G'\) are dependent over \(\mathbb{F}_2(D)\), a contradiction.

This lemma immediately yields the following.

## Theorem 14.3.9
Let \(\mathcal{C}\) be an \((n, k)\) convolutional code. The set of row degrees is the same for all canonical generator matrices for \(\mathcal{C}\).

This unique set of row degrees of a canonical generator matrix for \(\mathcal{C}\) is called the set of Forney indices of \(\mathcal{C}\). The sum of the Forney indices is the external degree of a canonical generator matrix, which is the degree of \(\mathcal{C}\). (The degree of \(\mathcal{C}\) is sometimes called the constraint length or the overall constraint length.) If \(m\) is the degree of the code, the code is often termed an \((n, k, m)\) code. The Viterbi Algorithm requires \(2^m\) states when a canonical encoder is used. If we construct a physical encoder for \(\mathcal{C}\) from a canonical generator matrix, the memory of the encoder is the largest Forney index. Since this index is unique, it is called the memory \(M\) of the code. Note that by Lemma 14.3.8, the memory of a physical encoder derived from any polynomial generator matrix is at least the memory of the code. For example, the memory of the physical encoders \(G_2, G'_2, G''_2,\) and \(G'''_2\) for \(\mathcal{C}_2\) of Example 14.1.1 are 2, 1, 1, and 2, respectively; \(\mathcal{C}_2\) has memory 1.
