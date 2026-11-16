\(\phi_{k,s_0}\), because of its low-pass filter characteristics, retains the lowest frequency components or the coarsest approximation of the original function.

In Equation (10.22), the choice of \(s_0\) is restricted by the order of wavelet, while the choice of \(s_M\) is governed by the physics of the problem. In applications involving electromagnetic scattering, as a rule of thumb, the highest scale \(s_M\) should be chosen such that \(1/2^{s_M+1}\) does not exceed \(0.1\lambda_0\).

The expansion of \(f\) given by (10.22) is substituted in (10.1), and the resultant equation is tested with the same set of expansion functions. This result gives a set of linear equations as

```
(10.23) \(\left[\begin{array}{cc} [A_{\phi\phi}] & [A_{\phi\psi}] \\ [A_{\psi\phi}] & [A_{\psi\psi}] \end{array}\right] \left[\begin{array}{c} [(A_{k,s_0})_k] \\ [(W_{n,s})_{n,s}] \end{array}\right] = \left[\begin{array}{c} <E_{z'}^i \phi_{k,s_0}>_{k'} \\ <E_{z'}^i \psi_{n',s'}>_{n',s'} \end{array}\right]\),
```

where

```
(10.24) \([A_{\phi\phi}] := <\phi_{k,s_0}, (L_K \phi_{k,s_0})>_{k,k'}\)
```

```
(10.25) \([A_{\phi\psi}] := <\phi_{k,s_0}, (L_K \psi_{n,s})>_{k,n,s}\)
```

```
(10.26) \([A_{\psi\phi}] := <\psi_{n',s'}, (L_K \phi_{k,s_0})>_{k,n',s'}\)
```

```
(10.27) \([A_{\psi\psi}] := <\psi_{n',s'}, (L_K \psi_{n,s})>_{n,s,n',s'}\)
```