```
(6.86) 
\(\tilde{\phi}(t) = \sum_k \tilde{h}_0[k] \tilde{\phi}(t-k)\)
```

```
(6.87) 
\(\psi(t) = \sum_k g_1[k] \phi(t-k)\)
```

```
(6.88) 
\(\tilde{\psi}(t) = \sum_k \tilde{h}_1[k] \tilde{\phi}(t-k)\)
```

The orthogonality and biorthogonality between these bases give the following four conditions on the filtering sequences:

```
(6.89) 
\(\langle g_0[k-2m], \tilde{h}_1[k-2n] \rangle = 0\)
```

```
(6.90) 
\(\langle g_1[k-2m], \tilde{h}_0[k-2n] \rangle = 0\)
```

```
(6.91) 
\(\langle g_0[k-2m], \tilde{h}_0[k] \rangle = \delta_{m,0}\)
```

```
(6.92) 
\(\langle g_1[k-2m], \tilde{h}_1[k] \rangle = \delta_{m,0}\)
```

Biorthogonal wavelet design consists of finding the filter sequences that satisfy (6.89) through (6.92). Because there is quite a bit of freedom in designing the biorthogonal wavelets, there are no set ways to the design procedure. For example, one may begin with \(g_0[k]\) being the two-scale sequence of a B-spline and proceed to determine the rest of the sequences. Another way is to design biorthogonal filter