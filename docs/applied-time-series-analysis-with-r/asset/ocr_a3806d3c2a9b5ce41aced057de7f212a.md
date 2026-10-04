# Wavelets

Since M is orthogonal when it also follows that

```
x = M'\mathbf{w}, (12.24)
```

where M' is the transpose of M. That is, knowing M allows us to transform from the data to the wavelet coefficients (the DWT), and M' allows us to perform an inverse discrete wavelet transform (IDWT), that is us to transform from the wavelet coefficients to the data.

NOTE: While the DWT can be applied to data sets whose length is not a power of 2, in the illustrative material, we will assume that n = 2^Jo for some J0.

For a discussion of discrete wavelets and scaling functions, see Percival and Walden (2000), Strang and Nguyen (1997), and Buce and Cao (1996). It should be noted that the discrete version of a wavelet takes the general form of the continuous wavelet, but is not simply a discretized version of it. Most authors refer to the elements of M as wavelet and scaling filter coefficients. Since the wavelet and scaling filter coefficients are close approximations to the corresponding discretized versions of the continuous dilated and translated wavelets, we use the notation \psi_{j,k} and \phi_{j,k} (see Percival and Walden, 2000, Equations 469 and 477a).

Using the partitioning in 12.23 we can write

| w1 | M1 |
| w2 | M2 |
| : | : |
| w Jo | MJo |
| v Jo | VJo | = x_r, (12.25)

where

| w1 = (d_{1,1} d_{1,2} d_{1,n/2}), |
| w2 = (d_{2,1} d_{2,2} ... d_{2,n/2}), |
| w Jo = d_{Jo,1} v Jo = s_{Jo,1}. |

Consider Percival and Walden (2000) for a discussion of the issues involved in constructing the matrix M.

# EXAMPLE 12.2: DISCRETE HAAR WAVELETS

Consider a data set of size n = 8 for which the Haar wavelet is used. In this case Jo = 3, the eight wavelet coefficients are w = (d_{1,1}, d_{1,2}, d_{1,3}, d_{1,4}, d_{2,2}, d_{3,3}, s_{3,3}), and Equation 12.22 takes the form