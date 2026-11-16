the simplest linear phase orthogonal filter bank. Indeed, if we denote

```
\( h_0^H(n) = \left\{ \frac{1}{\sqrt{2}}, \frac{1}{\sqrt{2}} \right\} \)
```

and

```
\( h_1^H(n) = \left\{ \frac{1}{\sqrt{2}}, -\frac{1}{\sqrt{2}} \right\}, \)
```

these two sequences satisfy the orthogonal conditions in (7.118). We recall that linear phase FIR filters must be either symmetric or antisymmetric, a condition not usually satisfied by orthogonal filters. This set of Haar filters is the only orthogonal set that has linear phase.

# 7.8.2.3 Two-Channel Biorthogonal Filter Bank in the Time-Domain.

We have shown in last section that the biorthogonal condition on the analysis and synthesis filters is

```
\( C_0(z) + C_0(-z) = H_0(z)G_0(z) + H_0(-z)G_0(-z) = 2. \)
```

Writing this equation in the time domain and using the convolution formula, yield the time-domain biorthogonal condition