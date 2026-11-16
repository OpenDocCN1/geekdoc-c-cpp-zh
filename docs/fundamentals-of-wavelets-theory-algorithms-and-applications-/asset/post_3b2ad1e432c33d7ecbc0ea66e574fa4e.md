
$a_{k,2}^n$ will coincide with $c_{-2}$. The next index, $c_{k+1,2}^n$, will then lie between $c_{k+1,2}$ and $c_{k+2,2}$.

**FIGURE 8.6:** The first term of $\{a_{k,M}^n\}$ when $\{a_{k,M}\}$ starts with $k \neq 0$.

![](img/f73ae67732328dc36596b27ffe8d0152_365_0.png)

Taking all of these points into account, we can obtain $a_M^n$ from $a_M$ by following these steps:

- 1. Based on the given discretized function data, determine the starting index of $a_M^n$. Let it be $a_{l,M}^n$.
- 2. Let $a_{l,M}^n$ lie between $a_{s,M}$ and $a_{s+1,M}$.
- 3. Let $a_{l,M}^n$ be shifted from $a_{s,M}$ toward the right by $\zeta$ in time. Then starting with $r=0$, compute

```
(8.30) $a_{l,M}^n = (1 - 2^M \xi) \tilde{a}_{s+r,M} + 2^M \xi \tilde{a}_{s+1+r,M}$.
```

- 4. Increment $i, s$ by 1 and $\xi$ by $n/2^{M+N}$.
- 5. Continue (3), (4) until $1 - 2^M \xi < 0$. When $1 - 2^M \xi < 0$, increment $r$ by 1 and reset $\xi$ to $n/2^{M+N}$. Increment $i, s$ by 1.
- 6. Repeat steps (3)-(5) until $a_{s+1+r,M}$ takes the last index of $\boldsymbol{a}_M$.

For a general case, the mapping of $x_M$ to $x_M^n$ can be obtained following the method described in Sections 5.6 and 7.2. For instance, to apply the linear spline interpolatory algorithm or the cubic spline interpolatory algorithm, we need to compute the function values of $x_M \lfloor k/(2^M \alpha_n) \rfloor$ or $x_M \lfloor k/(2^{M-1} \alpha_n) \rfloor$, $k \in \mathbb{Z}$. These values can be easily determined by using any spline evaluation scheme. More precisely, we have the following:

- (i) For $m=2$ (linear splines), it is clear that

```
\begin{cases}
x_M^n(t) = \sum_k \alpha_{k,M}^n N_2(2^M \alpha_n t - k) \\
\text{with } \alpha_{k,M}^n = x_M \left( \frac{k+1}{2^M \alpha_n} \right).
\end{cases}
(8.31)
```

- (ii) For $m=4$ (cubic splines), we have

```
x_M^n(t) = \sum_k \alpha_{k,M}^n N_4(2^M \alpha_n t - k).
(8.32)
```

with

```
$$a_{k,M}^n = \sum_{n=k-2}^{k+6} v_{k+2-2n} x_M \left( \frac{n}{2^{M-1}\alpha_n} \right),$$
```

where the weight sequence \(\{v_n\}\) is given in Section 5.6.

Finally, to obtain the input coefficient sequence \(\{\tilde{a}_{k,M}^n\}\) from \(\{a_{k,M}^n\}\) for the interoctave scale algorithm (8.19), we use the same change-of-bases sequence \(r\) as in (7.47).

## 8.1.4 Examples

In this section, we present a few examples to illustrate the FIWT algorithm discussed in this chapter. The graphs shown are the centered integral wavelet transform (CIWT) defined with respect to the spline wavelet \(\psi_m\) as

```
$$(W_{\psi_m} f)(b, a) := a^{\frac{1}{2}} \int_{-\infty}^{\infty} f(t) \overline{\psi_m \left( \frac{t-b}{a} + t^* \right)} dt,$$
```

where

```
$$t^* = \frac{2m-1}{2}.$$
```

Observe that the IWT as defined by (4.32) does not indicate the location of the discontinuity of a function properly since the spline wavelets are not symmetrical with respect to the origin. The CIWT circumvents this problem by shifting the location of the IWT in the time axis by \(at^*\) toward the right.

The integral wavelet transform of a function gives local time-scale information. To get the time-frequency information, we need to map the scale parameter to frequency. There is no general way of doing so. However, as a first approximation, we may consider the following mapping,

```
(8.36) \(a \mapsto f := \frac{c}{a},\)
```

where \(c > 0\) is a calibration constant. In this book, the constant \(c\) has been determined based on the one-sided center (\(\omega_+^*\)) and one-sided radius (\(\Delta\hat{\Psi}_+\)) of the wavelet \(\hat{\psi}(\omega)\), which are defined in Chapter 4.

For the cubic spline wavelet we get \(\omega_+^* = 5.164\) and \(\Delta\hat{\Psi}_+ = 0.931\). The corresponding figures for the linear spline wavelet are 5.332 and 2.360, respectively. Based on these parameters, we choose values of \(c\) as 1.1 for cubic spline and 1.5 for linear spline cases. It is important to point out that these values of \(c\) may not be suitable for all cases. Further research in this direction is required. We have chosen \(c\) by taking the lower cut-off frequency of \(\hat{\psi}(\omega)\).

### 8.1.4.1 IWT of a Linear Function.

To compare the results obtained by the method presented in this chapter with the results obtained by evaluating the integral of (8.34), we first take the linear function, which changes slope as shown in Figure 8.7. The function is sampled with 0.25 as the step size. So for linear splines, it means that the function is mapped into $l_2$, whereas for the cubic splines, the function is mapped into $l_3$. We choose $N = 1$, which gives one additional scale between two consecutive octaves. It is clear from Figures 8.8 and 8.9 that both the FIWT algorithm and direct integration give identical results for wavelet coefficients for octave levels, but there are errors in the results for inter-octave levels as discussed before.

**FIGURE 8.7:** Linear function whose WT is shown in Figures 8.8-8.10.

![](img/f73ae67732328dc36596b27ffe8d0152_370_0.png)

**FIGURE 8.8:** IWT of the function shown in Figure 8.7, using the linear spline wavelet for \(a = 0.50\) and \(a = 0.75\). Direct integration is performed with \(f_2(t)\).

![](img/f73ae67732328dc36596b27ffe8d0152_371_0.png)

![](img/f73ae67732328dc36596b27ffe8d0152_371_1.png)

**FIGURE 8.9:** IWT of the function shown in Figure 8.7 using the cubic spline wavelet for \(a = 0.50\) and \(a = 0.75\). Direct integration is performed with \(\hat{f}_3(t)\).

![](img/f73ae67732328dc36596b27ffe8d0152_373_0.png)

![](img/f73ae67732328dc36596b27ffe8d0152_373_1.png)

The importance of the moment property becomes clear from Figures 8.8 and 8.9. In both the linear and cubic cases, when the wavelet is completely inside the smooth region of the function, the WC are close to zero since the function is linear. Wherever the function changes the slope, the WCs have larger magnitudes. We also observe the edge effects near \(t = 0\) and \(t = 50\). The edge effects can be avoided by using special wavelets near the boundaries. Such boundary wavelets will be discussed in Chapter 10. If we use the IWT instead of the CIWT, then the whole plot will be shifted toward the left, and the shift will continue to become larger for lower levels. For Figures 8.8 and 8.9, the direct evaluation of (8.34) is done with \(f_2(t)\) and \(f_3(t)\), respectively. In Figure 8.10, the direct integration is done with \(f_{3,1}(t)\), which indicates that for interoctave levels also, the FIWT algorithm gives identical results if compared with the corresponding approximation function.

**FIGURE 8.10:** IWT of the function shown in Figure 8.7 using cubic spline wavelet for \(a = 0.75\). Direct integration is performed with \(f_{3,1}(t)\); the approximation of the function of Figure 8.7 is \(s = 3\), \(n = N = 1\).

![](img/f73ae67732328dc36596b27ffe8d0152_375_0.png)

For Figure 8.9, 440 wavelet coefficients have been computed. The direct integration takes about 300 times the CPU time of the FIWT algorithm. We wish to emphasize that the ratio of 300 : 1 is minimal, since with the increase in scale parameter \(a\), the complexity of the direct integration method increases exponentially, while for the FIWT it remains almost constant. Furthermore, in the FFT-based algorithm also, the complexity increases with \(a\).

### 8.1.4.2 Crack Detection.

As a further example to highlight the importance of the IWT in identifying the change in function behavior, we consider the following function:

For \(y := 2t - 1\)

$$
f(t) := \begin{cases} 
-\frac{3}{117}y(4y^2+16y+13) \quad t \in [0, 1/2] \\ 
-\frac{1}{6}y(y-1)(y-2) \quad t \in (1/2, 1]. 
\end{cases} \quad \text{(8.37)}
$$

Figure 8.11 shows the function and its WC for linear and cubic spline cases. The edge effect has not been shown. Once again, here we observe that for the cubic spline case, the WC are close to zero in the smooth region of the function; however, for the linear spline case, the WC are nonzero in this region since the function is of degree three in both intervals. This example shows that even a physically unnoticeable discontinuity can be detected using the wavelet transform.

**FIGURE 8.11:** The function given by (8.37) and its IWT using linear and cubic spline wavelets for \(\alpha = 1/128\).
