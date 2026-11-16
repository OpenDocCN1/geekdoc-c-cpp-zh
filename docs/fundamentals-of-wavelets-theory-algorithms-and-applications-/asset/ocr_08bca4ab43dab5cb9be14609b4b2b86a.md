Now going back to the first problem of mapping \(x_M\) to \(x_M^n\), we observe that since \(V_M \neq V_M^n\), we cannot expect to have \(x_M^n = x_M\) in general. However, if the MRA spaces \(\{V_s\}\) contain locally all of the polynomials up to order \(m\) in the sense that for each \(, 0 \le s \le m - 1\),

```
\(t' = \sum_k a_{t,k} \phi(t - k),\)
(8.26)
```

pointwise, for some sequence \(\{a_k\} k \in \mathbb{Z}\), then it is clear that \(\{V_s^n\}\) also possesses the same property. Consequently, the vanishing moment properties of the interoctave scale wavelets \(\Psi_{0,s}^n\) are the same as those of the original \(\psi\).

Hence in constructing the mapping of \(x_M\) to \(x_M^n\), we must ensure that this transformation preserves all polynomials up to order \(m\).

For the case of linear splines, such mapping can be easily obtained based on the fact that the coefficients in the linear-spline representation of a function are the function values evaluated at appropriate locations.

From the points of symmetry of \(N_2(2^M t)\) and \(N_2(2^M a_{nt})\) we obtain the magnitude of the shift \(\xi\) in the centers (Figure 8.5)

```
\(\xi = \frac{1}{2^M} \left( \frac{1}{\alpha_n} - 1 \right) = \frac{n}{2^{M+N}},\)
(8.27)
```