\(\sigma^{(2)}(x) = \sigma^{(1)}(x) + (S_3 + S_1 S_2) S_1^{-1} x^2 = \sigma^{(1)}(x) + \Delta_1 \Delta_{-1}^{-1} x^2\), we see that this polynomial satisfies (1) and (2). If \(\Delta_1 \neq 0\) but \(S_1 = 0\), then \(\sigma^{(1)}(x) = 1, \Delta_1 = S_3\), and the lowest degree polynomial that will satisfy (1) and (2) is \(\sigma^{(2)}(x) = \sigma^{(1)}(x) + S_3 x^3 = \sigma^{(1)}(x) + \Delta_1 x^3\). The choices get more complicated as the process continues, but, remarkably, the Berlekamp-Massey Algorithm reduces each stage down to one of two choices.

The Berlekamp-Massey Algorithm for computing an error locator polynomial for binary BCH codes is the following iterative algorithm that begins with \(\mu = 0\) and terminates when \(\sigma^{(\mu)}(x)\) is computed:

+   I. If \(\Delta_\mu = 0\), then \(\sigma^{(\mu+1)}(x) = \sigma^{(\mu)}(x)\).

+   II. If \(\Delta_\mu \neq 0\), then find a value \(-(1/2) \le \rho < \mu\) such that \(\Delta_\rho \neq 0\) and \(2\rho - d_\mu\) is as large as possible. Then \(\sigma^{(\mu+1)}(x) = \sigma^{(\mu)}(x) + \Delta_\mu \Delta_\rho^{-1} x^{2(\mu-\rho)} \sigma^{(\rho)}(x)\).

The error locator polynomial is \(\sigma(x) = \sigma^{(t)}(x)\); if this polynomial has degree greater than \(t\), more than \(t\) errors have been made, and the decoder should declare the received vector is uncorrectable. Once the error locator polynomial is determined, one of course proceeds as in the Peterson-Gorenstein-Zierler Algorithm to complete the decoding. We now reexamine Examples 5.4.3, 5.4.4, and 5.4.5 using the Berlekamp-Massey Algorithm. It is helpful in keeping track of the computations to fill out the following table.

| \(\mu\) | \(\sigma^{(\mu)}(x)\) | \(\Delta_\mu\) | \(d_\mu\) | \(2\mu - d_\mu\) |
|---|---|---|---|---|
| \(-1/2\) | \(1\) | \(1\) | \(0\) | \(-1\) |
| \(0\) | \(1\) | \(S_1\) | \(0\) | \(0\) |
| \(1\) | | | | |
| \(\vdots\) | | | | |
| \(t\) | | | | |

Example 5.4.7 We recompute \(\sigma(x)\) from Example 5.4.3, using Table 5.1. In that example \(t = 2\), and the syndromes are \(S_1 = \alpha^2, S_2 = \alpha^4, S_3 = \alpha^{11}\), and \(S_4 = \alpha^9\). We obtain the table

| \(\mu\) | \(\sigma^{(\mu)}(x)\) | \(\Delta_\mu\) | \(d_\mu\) | \(2\mu - d_\mu\) |
|---|---|---|---|---|
| \(-1/2\) | \(1\) | \(1\) | \(0\) | \(-1\) |
| \(0\) | \(1\) | \(\alpha^2\) | \(0\) | \(0\) |
| \(1\) | \(1 + \alpha^2 x\) | \(\alpha\) | \(1\) | \(1\) |
| \(2\) | \(1 + \alpha^2 x + \alpha^{14} x^2\) | | | |

We explain how this table was obtained. Observe that \(\Delta_0 = S_1 = \alpha^2\) and so II is used in computing \(\sigma^{(1)}(x)\). We must choose \(\rho < 0\) and the only choice is \(\rho = -1/2\). So \(\sigma^{(1)}(x) = \sigma^{(0)}(x) + \Delta_0 \Delta_{-1/2}^{-1} x^{2(0+1/2)} \sigma^{(-1/2)}(x) = 1 + \alpha^2 x\).

After computing \(\Delta_1 = S_3 + \sigma_1^{(1)} S_2 + \sigma_2^{(1)} S_1 + \sigma_3^{(1)} = \alpha^{11} + \alpha^2 \alpha^4 = \alpha\), we again use II to find \(\sigma^{(2)}(x)\). We must find \(\rho < 1\) with \(\Delta_\rho \neq 0\) and \(2\rho - d_\rho\) as large as possible.