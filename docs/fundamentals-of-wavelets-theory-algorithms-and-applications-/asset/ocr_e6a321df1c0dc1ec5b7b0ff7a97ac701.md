\(\hat{\phi}_{M,m}(\omega) = \begin{cases} \cos\left(\frac{\pi}{2} S_m\left(\frac{3}{2\pi}|\omega|-1\right)\right), & \frac{2\pi}{3} \le |\omega| \le \frac{4\pi}{3}; \\ 0, & |\omega| \ge \frac{4\pi}{3}; \\ 1, & |\omega| \le \frac{2\pi}{3}. \end{cases}\)

The scaling function in the time domain then becomes

(6.49) \(\phi_{M,m}(t) = \frac{2}{3} \frac{\sin \frac{2\pi t}{3}}{\frac{2\pi t}{3}} + \frac{2}{3} \int_0^1 \left[ \cos\left[ \frac{\pi}{2} S_m(\xi) \right] \cos\left[ \frac{2\pi}{3} (1+\xi) t \right] \right] d\xi\)

For a linear smoothing function \(m = 0\), the above integral can be easily evaluated. The result is

(6.50) \(\phi_{M,0} = \frac{2}{3} \frac{\sin \frac{2\pi t}{3}}{\frac{2\pi t}{3}} + 4 \frac{4t \sin \frac{2\pi t}{3} + \cos \frac{4\pi t}{3}}{\pi \frac{9-16t^2}{3}}\)

For higher values of \(m\), the integral in (6.49) needs to be evaluated numerically. In Figure 6.6 we show the scaling function and wavelet of Meyer for \(m = 0\) and 1.

As done before, the two-scale coefficients \(\{g_0[k]\}\) can be obtained by a \(4\pi\)-periodic extension of \(\hat{\phi}_{M,m}(\omega)\). An example of such an extension is shown in Figure 6.7.