+   3. Finite impulse response filters must be of approximately the same length.

+   4. There must be good stop-band behavior.

There are three approaches [17] to designing these filter banks.

# 8.4.1 Linear Phase Biorthogonal Approach

The filter $h_0$ and $g_0$ are symmetric FIR, with odd and even lengths, respectively

```
$h_0(n) = h_0(N-1-n)$,
```

```
$g_0(n) = g_0(N-1)$,
```

where $N$ is an odd number so that the half-delay condition is met. This satisfies the phase condition of (8.56); however, the filters should be designed such that spectral amplitudes are approximately the same.

# 8.4.2 Quarter-Shift Approach

In the quarter-shift (q-shift) method, the filter length $N$ of $h_0(n)$ is chosen as even and $g_0(n)$ is set to be

```
(8.57) $g_0(n) = h_0(N-1-n)$.
```

This choice clearly satisfies the magnitude condition of (8.56); however, the filters should be designed such that both have approximately the same phase characteristics.