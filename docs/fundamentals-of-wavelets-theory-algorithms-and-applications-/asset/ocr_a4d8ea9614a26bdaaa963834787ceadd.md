For orthonormal wavelets \( W^T = W^{-1} \) and the transformation (10.19) is unitary similar. It has been shown [9, 10] that the impedance matrix \( A_w \) is sparse, which reduces the inversion time significantly. Discrete wavelet transform (DWT) algorithms can be used to obtain \( A_w \) and finally the solution vector \( c \).

# 10.3.2 Direct Application of Wavelets

In another method of applying wavelets to integral equations, wavelets are directly applied—that is, first the unknown function is represented as a superposition of wavelets at several levels (scales) along with the scaling function at the lowest level, before using Galerkin's method described before.

Let us expand the unknown function \( f \) in (10.1) in terms of the scaling functions and wavelets as

```
\( f(x) = \sum_{s=s_0}^{s_L} \sum_{k=K_1}^{K_2} w_{k,s} \psi_{k,s}(x) + \sum_{k=K_1}^{K_2} a_{k,s_0} \phi_{k,s_0}(x). \)
(10.22)
```

It should be pointed out here that the wavelets \( \{\psi_{k,s}\} \) by themselves form a complete set; therefore, the unknown function could be expanded entirely in terms of the wavelets. However, to retain only a finite number of terms in the expansion, the scaling function part of (10.22) must be included. In other words, \( \{\psi_{k,s}\} \), because of their band-pass filter characteristics, extract successively lower and lower frequency components of the unknown function with decreasing values of the scale parameter \( s \), while