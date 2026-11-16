Therefore the maximum value of the wavelet transform (4.57) will occur at $\zeta = \omega 0$ with a band around $\zeta = \omega 0$, depending on the radius $\Delta_{\psi}^{\frac{1}{2}}$ of the wavelet $\tilde{\psi}(\omega)$.

As our next example, let $f(t) = \delta(t - t_0)$. Since this function has all the frequency components, we should expect a vertical line in the time-frequency plane, at $t = t_0$. Substituting $f(t) = \delta(t - t_0)$ in (4.7) and (4.32), we obtain

\(|G_{\phi}f(b, \xi)| = |\phi(t_0 - b)|.\) (4.60)

\(|W_{\psi}f(b, a)| = \frac{1}{\sqrt{a}} \left|\psi(\frac{t_0 - b}{a})\right|.\) (4.61)

Explanation of the STFT is straightforward. As expected, it does not depend on $\zeta$. We get a vertical line parallel to the frequency axis near $b = t_0$ with the time-spread determined by $\Delta_{\phi}$. For wavelet transform, we observe that it depends upon the scale parameter $a$. Rewriting (4.61) in terms of the new variable $\xi$, we have

\(\left|W_{\psi}f\left(b, \frac{\omega^*_{\psi}}{\xi}\right)\right| = \sqrt{\frac{\xi}{\omega^*_{\psi}}} \left|\psi\left(\frac{\xi}{\omega^*_{\psi}}(t_0 - b)\right)\right|.\) (4.62)

Although all the frequency contents of the delta function in time are indicated by (4.62), it is clear that as we reduce $\xi$, the time-spread increases. Furthermore, the location of the maximum will depend on the shape of $\psi(t)$. Readers are referred to [4] for more information on the interpretation of time-frequency plots.