where

M = delay length
h = the magnitude of the filter at some frequency \(\omega\)

The problem with this setup is that the pole radii are no longer the same (circular in the z plane) and we know that this produces coloration in the signal. The solution (Jot 1992) was to add a correction filter at the end of the whole system, T(z), whose magnitude is proportional to the inverse square root of the frequency-dependent reverb time, RT60(\(\omega\)). This is shown in Figure 11.34.

Finally, Figure 11.35 shows a generalized version of the FDN. It does not include the absorptive loss components (either static k values or H_LPFs) for clarity. The feedback matrix is always square, N x N, where N is the number of delay lines. Because it is square, it can be made to be unitary.

As an experiment, you can try to implement a four delay line version using the unitary matrix Equation 11.34 and gain coefficients proposed by Stautner and Puckette (1982), who were researching multichannel reverb algorithms.

```
\( G = \frac{g}{\sqrt{2}} \begin{bmatrix} 0 & 1 & 1 & 0 \\ -1 & 0 & 0 & -1 \\ 1 & 0 & 0 & -1 \\ 0 & 1 & -1 & 0 \end{bmatrix} (11.34) \)
```

where

|g| < 1.0

You can also try to de-correlate the four delay line outputs by using Jot's orthogonal matrix and set the coefficients c_N according to Equation 11.35:

```
\( C = g_2 \begin{bmatrix} 1 \\ -1 \\ 1 \\ -1 \end{bmatrix} (11.35) \)
```

where

|g_2| < 1.0

![](bbox=[0.1, 0.75, 0.9, 1.0])