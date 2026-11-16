```
\(\begin{bmatrix} h_k & h_{k-1} & h_{k-2} & \cdots & h_0 & 0 \\ 0 & h_k & h_{k-1} & \cdots & h_1 & h_0 \\ \vdots & \ddots & \ddots & \ddots & \vdots & \vdots \\ 0 & \cdots & \cdots & h_k & \cdots & h_0 \end{bmatrix}.\)
(4.1)
```

**Example 4.2.8** The cyclic codes \(\mathbb{F}_q^n\) and \(\{\mathbf{0}\}\) are duals of one another. The repetition code of length \(n\) over \(\mathbb{F}_q\) is a cyclic code whose dual is the cyclic code of even-like vectors of \(\mathbb{F}_q^n\). \(\blacksquare\)

**Exercise 208** Prove Theorem 4.2.6. \(\diamond\)

**Exercise 209** Based on dimension only, for \(0 \le i \le 7\) find \(\mathcal{C}_i^\perp\) for the cyclic codes \(\mathcal{C}_i\) in Example 4.2.4. \(\diamond\)

It is also not surprising that a subfield subcode of a cyclic code is cyclic.

**Theorem 4.2.9** Let \(\mathcal{C}\) be a cyclic code over \(\mathbb{F}_q\). Then \(\mathcal{C}|_{\mathbb{F}_r}\) is also cyclic.

**Exercise 210** Prove Theorem 4.2.9. \(\diamond\)

**Exercise 211** Verify that the three codes \(\mathcal{C}_1\), \(\mathcal{C}_2\), and \(\mathcal{C}_3\) of length 7 over \(\mathbb{F}_8\) of Example 3.8.2 are cyclic. Verify that \(\mathcal{C}_i|_{\mathbb{F}_2}\) are all cyclic as well. \(\diamond\)

Cyclic codes are easier to decode than other codes because of their additional structure.

We will examine decoding algorithms for general cyclic codes in Section 4.6 and specific families in Section 5.4. We now examine three ways to encode cyclic codes. Let \(\mathcal{C}\) be a cyclic code of length \(n\) over \(\mathbb{F}_q\) with generator polynomial \(g(x)\) of degree \(n-k\); so \(\mathcal{C}\) has dimension \(k\).

The first encoding is based on the natural encoding procedure described in Section 1.11. Let \(G\) be the generator matrix obtained from the shifts of \(g(x)\) in Theorem 4.2.1. We encode the message \(\mathbf{m} \in \mathbb{F}_q^k\) as the codeword \(\mathbf{c} = \mathbf{m}G\). We leave it as Exercise 212 to show that if \(m(x)\) and \(c(x)\) are polynomials in \(\mathbb{F}_q[x]\) associated to \(\mathbf{m}\) and \(\mathbf{c}\), then \(c(x) = m(x)g(x)\). However, this encoding is not systematic.

**Exercise 212** Let \(\mathcal{C}\) be a cyclic code of length \(n\) over \(\mathbb{F}_q\) with generator polynomial \(g(x)\). Let \(G\) be the generator matrix obtained from the shifts of \(g(x)\) in Theorem 4.2.1. Prove that the encoding of the message \(\mathbf{m} \in \mathbb{F}_q^k\) as the codeword \(\mathbf{c} = \mathbf{m}G\) is the same as forming the product \(c(x) = m(x)g(x)\) in \(\mathbb{F}_q[x]\), where \(m(x)\) and \(c(x)\) are the polynomials in \(\mathbb{F}_q[x]\) associated to \(\mathbf{m}\) and \(\mathbf{c}\). \(\diamond\)

The second encoding procedure is systematic. The polynomial \(m(x)\) associated to the message \(\mathbf{m}\) is of degree at most \(k-1\) (or is the zero polynomial). The polynomial \(x^{n-k}m(x)\) has degree at most \(n-1\) and has its first \(n-k\) coefficients equal to 0; thus the message is contained in the coefficients of \(x^{n-k}, x^{n-k+1}, \dots, x^{n-1}\). By the Division Algorithm,

```
\(x^{n-k}m(x) = g(x)a(x) + r(x), \quad \text{where } \deg r(x) < n-k \text{ or } r(x) = 0.\)
```