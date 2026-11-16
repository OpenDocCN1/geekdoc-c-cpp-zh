(10.28) 
\(\langle f, g \rangle := \int_a^b f(x) g(x) dx,\)

(10.29) 
\((L_K f)(x) := \int_a^b f(x') K(x, x') dx'.\)

In (10.23), \([w_{n,s}]_{n,x}\) is a one-dimensional vector and should not be confused with a two-dimensional matrix. Here the index \(n\) is varied first for a fixed value of \(s\).

We can explain the denseness of the conventional MoM and the sparseness of the wavelet MoM by recalling the fact that unlike wavelets, the scaling functions discussed in this book do not have vanishing moments properties. Consequently, for two pulse or triangular functions \(\phi_1\) and \(\phi_2\) (usual bases for the conventional MoM and suitable candidates for the scaling functions), even though \(\langle \phi_1, \phi_2 \rangle = 0\) for nonoverlapping supports, \(\langle \phi_1, L_K \phi_2 \rangle\) is not very small since \(L_K \phi_2\) is not very small. On the other hand, as is clear from the vanishing moment property—namely

(10.30) 
\(\int_{-\infty}^{\infty} t^p \psi_m(t) dt = 0; \quad p = 0, ..., m - 1\)

that the integral vanishes if the function against which the wavelet is being integrated behaves as a polynomial of a certain order locally. Away from the singular points the kernel usually has a locally polynomial behavior. Consequently, the integrals such as \((L_K \psi_{n,s})\) and the inner products involving the wavelets are very small for nonoverlapping supports.