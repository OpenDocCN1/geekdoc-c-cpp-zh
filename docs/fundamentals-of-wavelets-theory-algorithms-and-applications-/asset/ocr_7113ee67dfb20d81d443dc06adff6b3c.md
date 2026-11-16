# 3.2 EXAMPLES

# 3.2.1 Rectified Sine Wave

Consider a function \( p(t) = |\sin t| \), as shown in Figure 3.1, with the period \( T = \pi \) and \( \omega_0 = 2\pi/T = 2 \, \text{rad/s} \). Since the function \( p(t) \) is an even function with respect to \( t = 0 \), i.e., \( p(-t) = p(t) \), \( b_k = 0 \) for all \( k \). The coefficients \( \{a_k\} \) are computed as

```
a_k = \frac{2}{\pi} \int_0^\pi \sin t \cos(2kt) dt
= \frac{1}{\pi} \int_0^\pi [\sin(1-2k)t + \sin(1+2k)t] dt
= -\frac{1}{\pi} \left[ \frac{\cos(1-2k)t}{1-2k} \right]_0^\pi + \frac{1}{\pi} \left[ \frac{\cos(1+2k)t}{1+2k} \right]_0^\pi
= -\frac{4}{\pi} \frac{1}{4k^2 - 1}.
(3.9)
```

# FIGURE 3.1: Rectified sine wave.

![](bbox=[0.14, 0.64, 0.82, 0.82])

Hence the Fourier series of \( p(t) \) is given as