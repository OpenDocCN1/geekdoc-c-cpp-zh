
as \( z = z_1 b_1 + \cdots + z_t b_t \), where \( z_i \in \mathbb{F}_q \) for \( 1 \le i \le t \). Associate to \( z \) the \( t \times 1 \) column vector \( \widetilde{z} = [z_1 \cdots z_t]^t \). Create \( \widetilde{H} \) from \( H \) by replacing each entry \( h \) by \( \widetilde{h} \). Because \( H \) is an \( (n-k) \times n \) matrix with entries in \( \mathbb{F}_q \), \( \widetilde{H} \) is a \( t(n-k) \times n \) matrix over \( \mathbb{F}_q \). The rows of \( \widetilde{H} \) may be dependent. So a parity check matrix for \( C|_{\mathbb{F}_q} \) is obtained from \( \widetilde{H} \) by deleting dependent rows; the details of this are left as an exercise. Denote this parity check matrix by \( H|_{\mathbb{F}_q} \).

## Exercise 193 Prove that by deleting dependent rows from \( \widetilde{H} \), a parity check matrix for \( C|_{\mathbb{F}_q} \) is obtained. \(\unknown\)

## Example 3.8.1 A parity check matrix for the \([6, 3, 4]\) hexacode \(\mathcal{G}_6\) over \(\mathbb{F}_4\) given in Example 1.3.4 is

\( H = \begin{bmatrix} 1 & \omega & \omega & 1 & 0 & 0 \\ \omega & 1 & \omega & 0 & 1 & 0 \\ \omega & \omega & 1 & 0 & 0 & 1 \end{bmatrix} \).

The set \(\{1, \omega\}\) is a basis of \(\mathbb{F}_4\) over \(\mathbb{F}_2\). So

\( \widetilde{0} = \begin{bmatrix} 0 \\ 0 \end{bmatrix}, \widetilde{1} = \begin{bmatrix} 1 \\ 0 \end{bmatrix}, \widetilde{\omega} = \begin{bmatrix} 0 \\ 1 \end{bmatrix}, \text{ and } \widetilde{\overline{\omega}} = \begin{bmatrix} 1 \\ 1 \end{bmatrix} \).

Thus

\( \widetilde{H} = \begin{bmatrix} 1 & 0 & 0 & 1 & 0 & 0 \\ 0 & 1 & 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 & 1 & 0 \\ 1 & 1 & 0 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 & 0 & 1 \\ 0 & 1 & 0 & 0 & 0 & 1 \\ 1 & 1 & 0 & 0 & 0 & 0 \end{bmatrix} \text{ and } H|_{\mathbb{F}_2} = \begin{bmatrix} 1 & 0 & 0 & 1 & 0 & 0 \\ 0 & 1 & 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 & 1 & 0 \\ 1 & 0 & 1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 & 0 & 1 \\ 0 & 1 & 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 & 0 & 1 \end{bmatrix} \).

So we see that \(\mathcal{G}_6|_{\mathbb{F}_2}\) is the \([6, 1, 6]\) binary repetition code. \(\blacksquare\)

## Exercise 194 The \([6, 3, 4]\) code \(\mathcal{C}\) over \(\mathbb{F}_4\) with generator matrix \( G \) given by

\( G = \begin{bmatrix} 1 & 0 & 0 & 1 & 1 & 1 \\ 0 & 1 & 0 & 1 & \omega & \overline{\omega} \\ 0 & 0 & 1 & 1 & \overline{\omega} & \omega \end{bmatrix} \)

is the hexacode (equivalent to but not equal to the code of Example 3.8.1). Using the basis \(\{1, \omega\}\) of \(\mathbb{F}_4\) over \(\mathbb{F}_2\), find a parity check matrix for \(\mathcal{C}|_{\mathbb{F}_2}\). \(\unknown\)

## Example 3.8.2 In Examples 3.4.2 and 3.4.3, we constructed \(\mathbb{F}_8\) by adjoining a primitive element \(\alpha\) to \(\mathbb{F}_2\) where \(\alpha^3 = \alpha + 1\). Consider the three codes \(\mathcal{C}_1, \mathcal{C}_2, \text{ and } \mathcal{C}_3\) of length 7 over \(\mathbb{F}_8\) given by the following parity check matrices, respectively:

\( H_1 = \left[ 1 \ \ \alpha \ \ \alpha^2 \ \ \alpha^3 \ \ \alpha^4 \ \ \alpha^5 \ \ \alpha^6 \right] . \)
\( H_2 = \left[ \begin{array}{ c c c c c c c } 1 & \alpha & \alpha^2 & \alpha^3 & \alpha^4 & \alpha^5 & \alpha^6 \\ 1 & \alpha^2 & \alpha^4 & \alpha^6 & \alpha & \alpha^3 & \alpha^5 \end{array} \right] , \text{ and} \)
\( H_3 = \left[ \begin{array}{ c c c c c c c } 1 & \alpha & \alpha^2 & \alpha^3 & \alpha^4 & \alpha^5 & \alpha^6 \\ 1 & \alpha^3 & \alpha^6 & \alpha^2 & \alpha^5 & \alpha^4 & \alpha^4 \end{array} \right] . \)

The code \(\mathcal{C}_1\) is a [7, 6, 2] MDS code, while \(\mathcal{C}_2\) and \(\mathcal{C}_3\) are [7, 5, 3] MDS codes. Choosing \((1, \alpha, \alpha^2)\) as a basis of \(\mathbb{F}_8\) over \(\mathbb{F}_2\), we obtain the following parity check matrices for \(\mathcal{C}_1|_{\mathbb{F}_2}\), \(\mathcal{C}_2|_{\mathbb{F}_2}\), and \(\mathcal{C}_3|_{\mathbb{F}_2}\):

\( H_1|_{\mathbb{F}_2} = H_2|_{\mathbb{F}_2} = \left[ \begin{array}{ c c c c c c c } 1 & 0 & 0 & 1 & 0 & 1 & 1 \\ 0 & 1 & 0 & 0 & 1 & 1 & 0 \\ 0 & 0 & 1 & 0 & 1 & 1 & 1 \end{array} \right] \text{ and} \)
\( H_3|_{\mathbb{F}_2} = \left[ \begin{array}{ c c c c c c c } 1 & 0 & 0 & 1 & 0 & 1 & 1 \\ 0 & 1 & 0 & 1 & 1 & 1 & 0 \\ 0 & 0 & 1 & 0 & 1 & 1 & 1 \\ 1 & 1 & 1 & 0 & 1 & 0 & 0 \\ 0 & 1 & 0 & 0 & 1 & 1 & 1 \\ 0 & 0 & 1 & 1 & 0 & 1 & 1 \end{array} \right] . \)

So \(\mathcal{C}_1|_{\mathbb{F}_2} = \mathcal{C}_2|_{\mathbb{F}_2}\) are both representations of the [7, 4, 3] binary Hamming code \(\mathcal{H}_3\), whereas \(\mathcal{C}_3|_{\mathbb{F}_2}\) is the [7, 1, 7] binary repetition code.

## Exercise 195 Verify all the claims in Example 3.8.2.

This example illustrates that there is no elementary relationship between the dimension of a code and the dimension of its subfield subcode. The following theorem does exhibit a lower bound on the dimension of a subfield subcode; its proof is left as an exercise.

## Theorem 3.8.3 Let \(\mathcal{C}\) be an \([n, k]\) code over \(\mathbb{F}_q\). Then:

- (i) \(\mathcal{C}|_{\mathbb{F}_r}\) is an \([n, k_r]\) code over \(\mathbb{F}_r\), where \(k_q \ge n - r(n-k)\), and
- (ii) if the entries of a monomial matrix \(M \in \Gamma \text{Aut}(\mathcal{C})\) belong to \(\mathbb{F}_q\), then \(M \in \Gamma \text{Aut}(\mathcal{C}|_{\mathbb{F}_r})\).

## Exercise 196 Prove Theorem 3.8.3.

An upper bound on the dimension of a subfield subcode is given by the following theorem.

## Theorem 3.8.4 Let \(\mathcal{C}\) be an \([n, k]\) code over \(\mathbb{F}_q\). Then \(\mathcal{C}|_{\mathbb{F}_r}\) is an \([n, k_q]\) code over \(\mathbb{F}_q\), where \(k_q \le k\). If \(\mathcal{C}\) has a basis of codewords in \(\mathbb{F}_q^n\), then this is also a basis of \(\mathcal{C}|_{\mathbb{F}_r}\) and \(\mathcal{C}|_{\mathbb{F}_r}\) is \(k\)-dimensional.

Proof: Let \(G\) be a generator matrix of \(\mathcal{C}|_{\mathbb{F}_r}\). Then \(G\) has \(k_q\) independent rows; thus the rank of \(G\) is \(k_q\) when considered as a matrix with entries in \(\mathbb{F}_q\), or in \(\mathbb{F}_{q^r}\). Hence the rows of \(G\) remain independent in \(\mathbb{F}_{q^r}^n\), implying all parts of the theorem.

Another natural way to construct a code over $\mathbb{F}_q$ from a code over $\mathbb{F}_{q'}$ is to use the *trace function* $\text{Tr} : \mathbb{F}_{q'} \to \mathbb{F}_q$ defined by

$$\text{Tr}(\alpha) = \sum_{i=0}^{r-1} \alpha^{q^i} = \sum_{i=0}^{r-1} \sigma_q^i(\alpha), \quad \text{for all } \alpha \in \mathbb{F}_{q'},$$

where $\alpha = \sigma_q^m$ and $\sigma_q(\alpha) = \alpha^{q^i}$. Furthermore, $\sigma_q^i(\alpha) = \alpha^{q^i} = \alpha$ as every element of $\mathbb{F}_{q'}$ is a root of $x^q - x$ by Theorem 3.3.2. So $\sigma_q^r$ is the identity and therefore $\sigma_q(\text{Tr}(\alpha)) = \text{Tr}(\alpha)$. Thus $\text{Tr}(\alpha)$ is a root of $x^q - x$ and hence is in $\mathbb{F}_q$ as required by the definition of trace.

## Exercise 197 Fill in the missing steps that show that $\sigma_q(\text{Tr}(\alpha)) = \text{Tr}(\alpha)$. $\unknown$

## Exercise 198 Using the notation of Examples 3.4.2 and 3.4.3, produce a table of values of $\text{Tr}_3(\beta)$ for all $\beta \in \mathbb{F}_8$ where $\text{Tr}_3 : \mathbb{F}_8 \to \mathbb{F}_2$. $\unknown$

As indicated in the following lemma, the trace function is a nontrivial linear functional on the vector space $\mathbb{F}_{q'}$ over $\mathbb{F}_q$.

**Lemma 3.8.5** _The following properties hold for_ \(\text{Tr} : \mathbb{F}_{q'} \to \mathbb{F}_q\) _:_
(i) Tr is not identically zero,
(ii) \(\text{Tr}(\alpha + \beta) = \text{Tr}(\alpha) + \text{Tr}(\beta)\), for all \(\alpha, \beta \in \mathbb{F}_{q'}\), _and_
(iii) \(\text{Tr}(a\alpha) = a\text{Tr}(\alpha)\), for all \(\alpha \in \mathbb{F}_{q'}\) and all \(a \in \mathbb{F}_q\).

**Proof:** Part (i) is clear because \(\text{Tr}(x)\) is a polynomial in \(x\) of degree \(q^{r-1}\) and hence has at most \(q^{r-1}\) roots in \(\mathbb{F}_{q'}\) by Exercise 159. Parts (ii) and (iii) follow from the facts that \(\sigma_q(\alpha + \beta) = \sigma_q(\alpha) + \sigma_q(\beta)\) and \(\sigma_q(a\alpha) = a\sigma_q(\alpha)\) for all \(\alpha, \beta \in \mathbb{F}_{q'}\) and all \(a \in \mathbb{F}_q\) since \(\sigma_q\) is a field automorphism that fixes \(\mathbb{F}_q\). \(\square\)

The *trace of a vector* \(\mathbf{c} = (c_1, c_2, \dots, c_n) \in \mathbb{F}_{q'}^n\) is defined by \(\text{Tr}(\mathbf{c}) = (\text{Tr}(c_1), \text{Tr}(c_2), \dots, \text{Tr}(c_n))\). The *trace of a linear code* \(\mathcal{C}\) of length \(n\) over \(\mathbb{F}_{q'}\) is defined by \(\text{Tr}(\mathcal{C}) = \{ \text{Tr}(\mathbf{c}) \mid \mathbf{c} \in \mathcal{C} \}\).

The trace of \(\mathcal{C}\) is a linear code of length \(n\) over \(\mathbb{F}_q\). The following theorem of Delsarte [64] exhibits a dual relation between subfield subcodes and trace codes.

**Theorem 3.8.6 (Delsarte)** _Let_ \(\mathcal{C}\) _be a linear code of length_ \(n\) _over_ \(\mathbb{F}_{q'}\)_. Then_
$$(\mathcal{C}|_{\mathbb{F}_q})^\perp = \text{Tr}(\mathcal{C}^\perp).$$

**Proof:** We first show that \((\mathcal{C}|_{\mathbb{F}_q})^\perp \supseteq \text{Tr}(\mathcal{C}^\perp)\). Let \(\mathbf{c} = (c_1, c_2, \dots, c_n)\) be in \(\mathcal{C}^\perp\) and let \(\mathbf{b} = (b_1, \dots, b_n)\) be in \(\mathcal{C}|_{\mathbb{F}_q}\). Then by Lemma 3.8.5(ii) and (iii),
$$\text{Tr}(\mathbf{c}) \cdot \mathbf{b} = \sum_{i=1}^n \text{Tr}(c_i)b_i = \text{Tr}\left( \sum_{i=1}^n c_i b_i \right) = \text{Tr}(\mathbf{0}) = 0$$

as \(\mathbf{c} \in \mathcal{C}^\perp\) and \(\mathbf{b} \in \mathcal{C}|_{\mathbb{F}_q} \subseteq \mathcal{C}\). Thus \(\text{Tr}(\mathbf{c}) \in (\mathcal{C}|_{\mathbb{F}_q})^\perp\).

We now show that \((\mathcal{C}|_{\mathbb{F}_q})^\perp \subseteq \text{Tr}(\mathcal{C}^\perp)\) by showing that \((\text{Tr}(\mathcal{C}^\perp))^\perp \subseteq \mathcal{C}|_{\mathbb{F}_q}\). Let \(\mathbf{a} = (a_1, \dots, a_n) \in (\text{Tr}(\mathcal{C}^\perp))^\perp\). Since \(a_i \in \mathbb{F}_q\) for \(1 \le i \le n\), we need only show that \(\mathbf{a} \in \mathcal{C}\),
