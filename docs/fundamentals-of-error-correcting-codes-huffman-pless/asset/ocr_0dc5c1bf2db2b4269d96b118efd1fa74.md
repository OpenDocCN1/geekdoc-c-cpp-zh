this step is time consuming. For binary codes, the Berlekamp–Massey Algorithm builds the error locator polynomial by requiring that its coefficients satisfy a set of equations called the Newton identities rather than (5.10). These identities hold over general fields provided all error magnitudes are 1, which is precisely the case when the field is $\mathbb{F}_2$. The equations (5.10) are sometimes called generalized Newton identities. The Newton identities are:

```
S_1 + \sigma_1 = 0,
S_2 + \sigma_1 S_1 + 2\sigma_2 = 0,
S_3 + \sigma_1 S_2 + \sigma_2 S_1 + 3\sigma_3 = 0,
\vdots
S_v + \sigma_1 S_{v-1} + \dots + \sigma_{v-1} S_1 + v\sigma_v = 0,
and for j > v:
S_j + \sigma_1 S_{j-1} + \dots + \sigma_j S_{j-v} = 0.
```

A proof that these identities hold is found in [210] or [50, Theorem 3.3]. It turns out that we only need to look at the first, third, fifth, ... of these. For convenience we number these Newton identities (noting that \(t\sigma_t = \sigma_t\) when \(t\) is odd):

+   (1) S_1 + \sigma_1 = 0,
+   (2) S_3 + \sigma_1 S_2 + \sigma_2 S_1 + \sigma_3 = 0,
+   (3) S_5 + \sigma_1 S_4 + \sigma_2 S_3 + \sigma_3 S_2 + \sigma_4 S_1 + \sigma_5 = 0,
+   \vdots
+   (\mu) S_{2\mu-1} + \sigma_1 S_{2\mu-2} + \sigma_2 S_{2\mu-3} + \dots + \sigma_{2\mu-2} S_1 + \sigma_{2\mu-1} = 0,
+   \vdots

Define a sequence of polynomials \(\sigma^{(\mu)}(x)\) of degree \(d_\mu\), indexed by \(\mu\) as follows:

```
\sigma^{(\mu)}(x) = 1 + \sigma_1^{(\mu)} x + \sigma_2^{(\mu)} x^2 + \dots + \sigma_{d_\mu}^{(\mu)} x^{d_\mu}.
```

The polynomial \(\sigma^{(\mu)}(x)\) is calculated to be the minimum degree polynomial whose coefficients \(\sigma_1^{(\mu)}, \sigma_2^{(\mu)}, \sigma_3^{(\mu)}, \dots\) satisfy all of the first \(\mu\) numbered Newton identities. Associated to each polynomial is its discrepancy \(\Delta_\mu\), which measures how far \(\sigma^{(\mu)}(x)\) is from satisfying the \(\mu + 1\)st identity:

```
\Delta_\mu = S_{2\mu+1} + \sigma_1^{(\mu)} S_{2\mu} + \sigma_2^{(\mu)} S_{2\mu-1} + \dots + \sigma_{2\mu}^{(\mu)} S_1 + \sigma_{2\mu+1}^{(\mu)}.
```

We start with two initial polynomials, \(\sigma^{(-1/2)}(x) = 1\) and \(\sigma^{(0)}(x) = 1\), and then generate \(\sigma^{(\mu)}(x)\) inductively in a manner that depends on the discrepancy. The discrepancy \(\Delta_{-1/2} = 1\) by convention; the remaining discrepancies are calculated. Plugging the coefficients of \(\sigma^{(0)}(x)\) into identity (1), we obtain \(S_1\) (as \(\sigma_1^{(0)} = 0\)) and so the discrepancy of \(\sigma^{(0)}(x)\) is \(\Delta_0 = S_1\).

We proceed with the first few polynomials to illustrate roughly the ideas involved. Noting the discrepancy \(\Delta_0 = S_1\), if \(\sigma^{(0)}(x)\) had an additional term \(S_1 x\), the coefficients of this polynomial \(\sigma^{(0)}(x) + S_1 x = 1 + S_1 x\) would satisfy identity (1) since \(S_1 + S_1 = 0\). So \(\sigma^{(1)}(x) = 1 + S_1 x\). Plugging the coefficients of \(\sigma^{(1)}(x)\) into (2), we have \(\Delta_1 = S_3 + \sigma_1^{(1)} S_2 = S_3 + S_1 S_2\). If \(\Delta_1 = 0\), then \(\sigma^{(1)}(x)\) satisfies (2) also. Also if \(\Delta_1 \neq 0\) and if \(S_1 \neq 0\), then setting