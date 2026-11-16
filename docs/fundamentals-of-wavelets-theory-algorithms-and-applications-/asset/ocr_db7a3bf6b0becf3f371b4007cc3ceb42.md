```
E_{N_m}(z) = \sum_{k=-\infty}^{\infty} \left| \hat{N}_m \left( \frac{\omega}{2} + 2\pi k \right) \right|^2
= \sum_{k=-\infty}^{\infty} A_{N_m}(k) z^k
= \sum_{k=m+1}^{m-1} N_{2m}(m+k) z^k ,
```

# (6.33)

with \( z := e^{-j\omega/2} \) and the autocorrelation function

```
A_{N_m}(k) = \int_{-\infty}^{\infty} N_m(x) N_m(k+m) dx = N_{2m}(m+k) .
```

# (6.34)

Finally, by using the relation (6.16), we have

```
g_1[k] := g_1[m,k] = (-1)^k 2^{-m+1} \sum_{\ell=0}^{m} \binom{m}{\ell} N_{2m}(k+1-\ell), \quad 0 \le k \le 3m-2 .
```

# (6.35)

# 6.2.2 Remarks

Recall that, in the expressions for \( H_0(z) \) and \( H_1(z) \) in terms of \( G_0(z) \) and \( G_1(z) \), there is a term \( \Delta_{G_0 G_1}(z) = z^m E_{N_m}(z) \) in the denominator. Consequently, the sequences \( \{h_0[k]\} \) and \( \{h_1[k]\} \) are infinitely long, although their magnitude decays exponentially. These are the sequences that will be used in the development of decomposition and reconstruction algorithms in Chapters 7 and 8. It is clear that while \( G_0 \) and \( G_1 \) form FIR filters, \( H_0 \) and \( H_1 \) are