The importance of the coefficients \(\tilde{w}_{k,s}\) is that they constitute the CWT of \(x_M\) relative to the analyzing wavelet \(\psi_m\) at certain dyadic points—namely

(7.49) 
\(\tilde{w}_{k,s} = 2^{\frac{s}{2}}(W_{\psi} x_M)(\frac{k}{2^s}, \frac{1}{2^s}), \quad M - M' \le s < M, \quad k \in \mathbb{Z}.\)

# FIGURE 7.11: Standard wavelet decomposition process implemented with change of bases.

![](bbox=[0.14, 0.38, 0.82, 0.59])

# 7.6 SIGNAL RECONSTRUCTION IN SEMIIORTHOGONAL SUBSPACES

The algorithm described in Section 7.4 concerns the recovery of the original data. In that case, the original data are the set of scaling function coefficients \(\{a_M\}\) at the highest resolution. Since the original input signal is an analog function \(x(t) = x_M(t) = \sum a_{M,\ell} \phi(2^M t - \ell)\), it is necessary to recover the signal by performing the summation. Recall that the decomposition algorithm discussed in Section 7.5 produces the spline and wavelet