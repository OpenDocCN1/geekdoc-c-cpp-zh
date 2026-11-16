Proof: By definition \(v(x) = g(x)f(x) + s(x)\), where \(s(x) = \sum_{i=0}^{n-k-1} s_i x^i\). So \(xv(x) = xg(x)f(x) + xs(x) = xg(x)f(x) + g(x)f_1(x) + s'(x)\), where \(s'(x) = R_{g(x)}(xs(x))\). Also \(xv(x) \mod (x^n - 1) = xv(x) - (x^n - 1)u_{n-1}\). Thus \(xv(x) \mod (x^n - 1) = xg(x)f(x) + g(x)f_1(x) + s'(x) - (x^n - 1)u_{n-1} = g(x)(xf(x) + f_1(x) - h(x)u_{n-1}) + s'(x)\), where \(g(x)|h(x) = x^n - 1\). Therefore \(R_{g(x)}(xv(x) \mod (x^n - 1)) = s'(x) = R_{g(x)}(xs(x))\) because \(\deg s'(x) < n - k\). As \(g(x)\) is monic of degree \(n - k\) and \(s(x) = \sum_{i=0}^{n-k-1} s_i x^{i+1}\), the remainder when \(x s(x)\) is divided by \(g(x)\) is \(xs(x) - g(x)x s_{n-k-1}\).

We now describe our first version of the Meggitt Decoding Algorithm and use an example to illustrate each step. Define the syndrome polynomial \(S(v(x))\) of any \(v(x)\) to be \(S(v(x)) = R_{g(x)}(x^{n-k}v(x))\).

By Theorem 4.6.1(iii), if \(v(x) \in R_n\), then \(S(v(x)) = 0\) if and only if \(v(x) \in C\).

+   Step I: This is a one-time precomputation. Find all the syndrome polynomials \(S(e(x))\) of error patterns \(e(x) = \sum_{i=0}^{n-1} e_i x^i\) such that \(wt(e(x)) \le t\) and \(e_{n-1} \neq 0\).

Example 4.6.3 Let C be the [15, 7, 5] binary cyclic code with defining set \(T = \{1, 2, 3, 4, 6, 8, 9, 12\}\). Let \(\alpha\) be a 15th root of unity in \(F_{16}\). Then \(g(x) = 1 + x^4 + x^6 + x^7 + x^8\) is the generator polynomial of \(C\) and the syndrome polynomial of \(e(x)\) is \(S(e(x)) = R_{g(x)}(x^8 e(x))\). Step I produces the following syndrome polynomials:

| e(x) | S(e(x)) | e(x) | S(e(x)) |
|---|---|---|---|
| \(x^{14}\) | \(x^7\) | \(x^6 + x^{14}\) | \(x^3 + x^5 + x^6\) |
| \(x^{13} + x^{14}\) | \(x^5 + x^7\) | \(x^5 + x^{14}\) | \(x^2 + x^4 + x^6 + x^7\) |
| \(x^{12} + x^{14}\) | \(x^4 + x^7\) | \(x^4 + x^{14}\) | \(x + x^3 + x^4 + x^5 + x^7\) |
| \(x^{11} + x^{14}\) | \(x^2 + x^7\) | \(x^3 + x^{14}\) | \(1 + x^2 + x^3 + x^4 + x^7\) |
| \(x^{10} + x^{14}\) | \(x^4 + x^7\) | \(x^2 + x^{14}\) | \(x + x^2 + x^3 + x^6\) |
| \(x^9 + x^{14}\) | \(x^2 + x^7\) | \(x + x^{14}\) | \(1 + x + x^4 + x^5 + x^6 + x^7\) |
| \(x^8 + x^{14}\) | \(x + x^7\) | \(1 + x^{14}\) | \(1 + x^4 + x^6\) |
| \(x^7 + x^{14}\) | \(1 + x^7\) | | |

The computations of these syndrome polynomials were aided by Theorems 4.6.1 and 4.6.2. For example, in computing the syndrome polynomial of \(x^{12} + x^{14}\), we have \(S(x^{12} + x^{14}) = R_{g(x)}(x^8(x^{12} + x^{14})) = R_{g(x)}(x^3 + x^7) = x^3 + x^7\), using Theorem 4.6.1(i). In computing the syndrome polynomial for \(1 + x^{14}\), first observe that \(R_{g(x)}(x^8) = 1 + x^4 + x^6 + x^7\), then \(S(1 + x^{14}) = R_{g(x)}(x^8 + 1^{14})) = R_{g(x)}(x^8) + R_{g(x)}(x^{12} + x^{14}) = x^3 + x^7\). We see by Theorem 4.6.2 that \(R_{g(x)}(x^{12}) = R_{g(x)}(x^{27}) = R_{g(x)}(x(1 + x^4 + x^6 + x^7)) = R_{g(x)}(x + x^5 + x^7) + R_{g(x)}(x^8) = x + x^4 + x^6 + x^7 + 1 + x + x^4 + x^6 + x^7 = x^5\). Therefore in computing the syndrome polynomial for \(x + x^{14}\), we have \(S(x + x^{14}) = R_{g(x)}(x^9(x^8 + x^{14})) = R_{g(x)}(x^9 + x^{13}) = R_{g(x)}(x^9) + R_{g(x)}(x^{13}) = 1 + x + x^4 + x^5 + x^6 + x^7\). The others follow similarly.