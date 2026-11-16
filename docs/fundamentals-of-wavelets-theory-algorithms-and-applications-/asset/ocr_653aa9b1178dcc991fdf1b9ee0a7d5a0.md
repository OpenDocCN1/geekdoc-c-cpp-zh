```
\langle h_0(k), \tilde{g}_0(k-2n) \rangle = \delta_{n,0}
\langle h_1(k), \tilde{g}_1(k-2n) \rangle = \delta_{n,0}
\langle h_1(k), \tilde{g}_0(k-2n) \rangle = 0
\langle h_0(k), \tilde{g}_1(k-2n) \rangle = 0 (7.128)
```

# 7.9 POLYPHASE REPRESENTATION FOR FILTER BANKS

Polyphase representation of a signal is an alternative approach to discrete signal representation other than in the spectral domain and the time domain. It is an efficient representation for computation. Consider the process of convolution and decimation by 2, we compute all the resulting coefficients and then cast out half of them. The polyphase approach decimates the input signal and then convolves with only half of the filter coefficients. This approach increases the computational efficiency by reducing the redundancy.

# 7.9.1 Signal Representation in Polyphase Domain

Let the z-transform of a discrete causal signal separated into segments of M points, be written as

```
(7.129)
X(z) = x(0) + x(1)z^{-1} + x(2)z^{-2} + x(3)z^{-3} + ... + x(M-1)z^{-M+1}
+ x(M)z^{-M} + x(M+1)z^{-(M+1)} + x(M+2)z^{-(M+2)} + ...
+ x(2M)z^{-2M} + x(2M+1)z^{-(2M+1)} + x(2M+2)z^{-(2M+2)} + ...
+ x(3M)z^{-3M} + x(3M+1)z^{-(3M+1)} + ...
```