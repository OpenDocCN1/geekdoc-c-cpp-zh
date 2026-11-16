we obtain the wavelet-packet based cross-term deleted representation ( WPCDR), given by

$$WPCDR_k(t, f) = \sum_{j,m} WVD_{s_{j,m}}(t, f).$$
(9.14)

We remark here that the WPCDR actually gives the auto WVD of the signal components within each subband; therefore, it is quite effective and is perhaps the best choice for analyzing a multicomponent signal. In addition, the WPCDR is computationally advantageous, since both decomposition and representation can be implemented efficiently.

# 9.4.1 Best Basis Selection

Equation (9.8) is actually a special case of

$$W_j = U_{j-k}^{2^k} \oplus U_{j-k}^{2^k+1} \oplus \dots \oplus U_{j-k}^{2^{k+1}-1}$$
(9.15)

when \( k = j \) Equation (9.15) means that the \( j \)th frequency band \( H_j \) can be partitioned into \( 2^k, k=0, 1, \dots, j \), subbands

$$H_j^{k,m}, m=0, \dots, 2^k-1.$$
(9.16)

The uniform division of the frequency axis and the logarithmic division for wavelets are just two extreme cases, when \( k \) in (9.16) takes on the values of \( j \) and 0, respectively. In fact, \( k \) is allowed to vary among \( H_j, j=1, 2, \dots \), so that the subbands adapt to (or match) the local spectra of the signal and thereby yield the best