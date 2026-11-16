
h(n) = 0 \quad \forall \ n < 0.

The z-transform of h(n) is a right-sided polynomial of $z^{-1}$

$$H(z) = h(0) + h(1)z^{-1} + h(2)z^{-2} + \cdots + h(m)z^{-m}.$$

If $H(z)$ is a causal filter, then $H(z^{-1})$ is anticausal since

$$H(z^{-1}) = h(0) + h(1)z + h(2)z^{2} + \cdots + h(m)z^{m}.$$

which is a left-sided polynomial of $z$. As a result, $H(z^{-1})$ is also anticausal since the polynomial is the same as that of $H(z^{-1})$ except the signs of odd coefficients have been changed

$$H(-z^{-1}) = h(0) - h(1)z + h(2)z^{2} - \cdots - h(m)z^{m}.$$

The last term has a negative sign if we assume $m$ is odd. To realize the anticausal FIR filter, we must delay the filter by the length of the filter to make it causal. Hence

$$-z^{-m}H(-z^{-1}) = h(m) - h(m-1)z^{-1} + \cdots + h(1)z^{-m+1} - h(0)z^{-m}$$

is a causal filter. If we choose

$$H_0(z) = H(z)$$

$$H_1(z) = -z^{-m}H_0(-z^{-1})$$

$$G_0(z) = H_1(-z)$$

$$G_1(z) = -H_0(-z),$$

we have a filter bank consisting of causal filters.

## 7.8.2.2 PR Requirements.

Perfect reconstruction demands that

$$S(z) + S(-z) = 2.$$

In terms of the low-pass filter $H_0(z)$, the equation becomes

(7.109) $$H_0(z)H_0(z^{-1}) + H_0(-z)H_0(-z^{-1}) = 2.$$

Let us consider the PR condition in (7.109). In time domain we have

(7.110) 
$$
\begin{aligned}
S(z) + S(-z) &= \sum_m h_0(n)z^{-n} \sum_m h_0(m)z^{-m} + \sum_n h_0(n)z^{-n} \sum_m (-1)^{(n+m)} h_0(m)z^{-m} \\
&= \sum_{n,m} h_0(n)h_0(m)z^{-n+m} + \sum_{n,m} (-1)^{(n+m)} h_0(n)h_0(m)z^{-n-m} \\
&= 2.
\end{aligned}
$$

Satisfaction of (7.110) requires $(m + n)$ be even, and we have

(7.111) $$\sum_{n,m} h_0(n)h_0(m)z^{-n}z^m = 1.$$

The left side of (7.111) is the $z$-transform of the auto-correlation function of the sequence $h_0(n)$. To show this relation, we denote

(7.112) $$\kappa(n) = \sum_k h_0(k)h_0(k+n) = \kappa(-n)$$

be the autocorrelation function. Its $z$-transform is written as

(7.113) 
$$
\begin{aligned}
K(z) &= \sum_n \sum_k h_0(k)h_0(k+n)z^{-n} \\
&= \sum_k h_0(k) \sum_n h_0(k+n)z^{-n} \\
&= \sum_k h_0(k) \sum_m h_0(m)z^{-(m-k)}
\end{aligned}
$$

which implies

(7.114) $$\kappa(n) = h_0(n) * h_0(-n).$$

Comparing (7.113) and (7.110) and making the substitution

$$K(z) \to S(z)$$

$$\kappa(n) \to s(n),$$

we have

$$S(z) = \sum_n \sum_k h_0(k) h_0(k+n) z^{-n}.$$

From (7.98) and the fact that $s(2n) = 0$ for all integer $n$, we have the orthonormality condition required for PR

$$\sum_k h_0(k) h_0(k+2n) = \delta_{n,0} \tag{7.115}$$

This implies the orthogonality of the filter on all its even translates. We apply the same analysis to the high-pass filter $h_1(n)$ and get the same condition for $h_1(n)$

$$\sum_k h_1(k) h_1(k+2n) = \delta_{n,0} \tag{7.116}$$

$$\sum_k h_0(k) h_1(k+2n) = 0. \tag{7.117}$$

In terms of wavelet and approximation function basis, the orthonormality conditions given above are expressed as inner products

$$\langle h_0(k), h_0(k+2n) \rangle = \delta_{n,0} \quad \langle h_1(k), h_1(k+2n) \rangle = \delta_{n,0} \quad \langle h_0(k), h_1(k+2n) \rangle = 0 \tag{7.118}$$

where the approximation basis $h_0(k)$ and the wavelet basis $h_1(k)$ are orthonormal to their even translates. They are also orthogonal to each other. If we construct an infinite matrix $[H_0]$ using the FIR sequence $h_0(n)$ such that

(7.119) 
$$[H_0] = \begin{bmatrix} h_0[0] & h_0[1] & h_0[2] & h_0[3] & 0 & 0 & 0 \\ 0 & 0 & h_0[0] & h_0[1] & h_0[2] & h_0[3] & 0 \\ 0 & 0 & 0 & h_0[0] & h_0[1] & h_0[2] & h_0[3] \\ & & & 0 & 0 & 0 & 0 \\ & & & & 0 & 0 & 0 \\ & & & & & 0 & 0 \\ & & & & & & 0 \end{bmatrix},$$

it is obvious that

(7.120) $$[H_0][H_0]^t = I$$

using the orthonormality conditions in (7.118). Therefore, $[H_0]$ is an orthogonal matrix. We define $[H_1]$ in a similar way using the FIR sequence of $h_1(n)$ and show that

(7.121) $$[H_1][H_1]^t = I.$$

In addition, the reader can also show that

(7.122) $$[H_1][H_0]^t = [H_0][H_1]^t = [0].$$

Equations in (7.118) constitute the orthogonal conditions imposed on the FIR filters. This type of filter bank is called the _orthogonal filter bank_. The processing sequences for Haar scaling function and Haar wavelets are the simplest linear phase orthogonal filter bank. Indeed, if we denote

$$h_0^H(n) = \left\{ \frac{1}{\sqrt{2}}, \frac{1}{\sqrt{2}} \right\}$$

and

$$h_1^H(n) = \left\{ \frac{1}{\sqrt{2}}, -\frac{1}{\sqrt{2}} \right\},$$

these two sequences satisfy the orthogonal conditions in (7.118). We recall that linear phase FIR filters must be either symmetric or antisymmetric, a condition not usually satisfied by orthogonal filters. This set of Haar filters is the only orthogonal set that has linear phase.

## 7.8.2.3 Two-Channel Biorthogonal Filter Bank in the Time-Domain.

We have shown in last section that the biorthogonal condition on the analysis and synthesis filters is

$$C_0(z) + C_0(-z) = H_0(z)G_0(z) + H_0(-z)G_0(-z) = 2.$$

Writing this equation in the time domain and using the convolution formula, yield the time-domain biorthogonal condition

(7.123) 
$$\sum_k h_0(k)g_0(\ell-k) + (-1)^\ell \sum_k h_0(k)g_0(\ell-k) = 2\delta_{\ell,0}.$$

The equality holds only if $\ell$ is even. This results in the biorthogonal relation between the analysis and synthesis filters

(7.124) 
$$\sum_k h_0(k)g_0(2n-k) = \langle h_0(k), g_0(2n-k) \rangle = \delta_{n,0}.$$

The biorthogonal condition can also be expressed in terms of $H_1(z)$ to yield

(7.125) 
$$\sum_k h_1(k)g_1(2n-k) = \langle h_1(k), g_1(2n-k) \rangle = \delta_{n,0}.$$

The additional biorthogonal relations are

(7.126) 
$$\langle h_1(k), g_0(2n-k) \rangle = 0, \qquad \langle h_0(k), g_1(2n-k) \rangle = 0.$$

If we consider the filters as discrete bases, we have

(7.127) 
$$\tilde{g}_m(k) = g_m(-k).$$

The biorthogonal relations become

(7.128) 
$$
\begin{aligned}
\langle h_0(k), \tilde{g}_0(k-2n) \rangle &= \delta_{n,0} \\
\langle h_1(k), \tilde{g}_1(k-2n) \rangle &= \delta_{n,0} \\
\langle h_1(k), \tilde{g}_0(k-2n) \rangle &= 0 \\
\langle h_0(k), \tilde{g}_1(k-2n) \rangle &= 0
\end{aligned}
$$

## 7.9 POLYPHASE REPRESENTATION FOR FILTER BANKS

Polyphase representation of a signal is an alternative approach to discrete signal representation other than in the spectral domain and the time domain. It is an efficient representation for computation. Consider the process of convolution and decimation by 2, we compute all the resulting coefficients and then cast out half of them. The polyphase approach decimates the input signal and then convolves with only half of the filter coefficients. This approach increases the computational efficiency by reducing the redundancy.

### 7.9.1 Signal Representation in Polyphase Domain

Let the z-transform of a discrete causal signal separated into segments of $M$ points, be written as

(7.129) 
$$
\begin{aligned}
X(z) = {} & x(0) + x(1)z^{-1} + x(2)z^{-2} + x(3)z^{-3} + \cdots + x(M-1)z^{-M+1} \\
& + x(M)z^{-M} + x(M+1)z^{-(M+1)} + x(M+2)z^{-(M+2)} + \cdots \\
& + x(2M)z^{-2M} + x(2M+1)z^{-(2M+1)} + x(2M+2)z^{-(2M+2)} + \cdots \\
& + x(3M)z^{-3M} + x(3M+1)z^{-(3M+1)} + \cdots
\end{aligned}
$$

$$\sum_{i=0}^{M-1} z^{-i} X^i(z^M), \tag{7.130}$$

where $X(z^M)$ is the z-transform of $x(n)$ decimated by $M$ ($\downarrow M$). The index $i$ indicates the number of sample shifts. For the case of $M=2$, we have

$$X(z) = X_0(z^2) + z^{-1}X_1(z^2). \tag{7.131}$$

### 7.9.2 Filter Bank in the Polyphase Domain

For a filter $H(z)$ in a two-channel setting, the polyphase representation is exactly the same as in (7.131)

$$H(z) = H_e(z^2) + z^{-1}H_o(z^2) \tag{7.132}$$

where $H_e(z^2)$ consists of the even samples of $h(n)$ and $H_o(z^2)$ has all the odd samples. The odd and even parts of the filter are used to process the odd and even coefficients of the signal separately. To formulate the two-channel filter bank in the polyphase domain, we need the help of two identities:

- 1. $(\downarrow M)G(z) = G(z^M)(\downarrow M)$
- 2. $(\uparrow M)G(z^M) = G(z)(\uparrow M).$
- (7.133)

A filter $G(z^2)$ followed by a two-point decimator is equivalent to a two-point decimator followed by $G(z)$. The second identity is useful for the synthesis filter bank.
