```
a_{k, \ell} = \frac{a_{2k, \ell+1} + a_{2k+1, \ell+1}}{2},
```

```
w_{k, \ell} = a_{2k+1, \ell+1} - a_{2k, \ell+1}.
```

As this step is repeated, it generates the approximation coefficient (the average) and wavelet coefficients (the difference) of the next lower resolution.

It is easy to see that if we wish to reconstruct the signal from level \(\ell\) to \((\ell + 1)\), we simply solve for the values of \(a_{2k, \ell+1}\) and \(a_{2k+1, \ell+1}\), using the above equations to obtain

```
(8.58) \(a_{2k+1, \ell+1} = a_{k, \ell} + \frac{w_{k, \ell}}{2},\)
```

```
(8.59) \(a_{2k, \ell+1} = a_{k, \ell} - \frac{w_{k, \ell}}{2}.\)
```

Rewriting (8.59),

```
(8.60) \(a_{k, \ell} = a_{2k, \ell+1} + \frac{w_{k, \ell}}{2},\)
```

we observe that the approximation coefficient of the lower resolution can be computed from the corresponding approximation coefficients of the higher resolution—namely the even coefficient plus half of the difference between its adjacent coefficients. Instead of computing the average and difference simultaneously, we