(4.69)

\(\mathbf{W}_f(t,\omega)=\frac{1}{2\pi}\int_{-\infty}^{\infty} \exp \left( j \frac{b \left( t+\frac{\tau}{2} \right)^2}{2} + j \omega_0 \left( t+\frac{\tau}{2} \right) \right)\)
\(\times \exp \left( -j \frac{b \left( t-\frac{\tau}{2} \right)^2}{2} - j \omega_0 \left( t-\frac{\tau}{2} \right) - j \omega \tau \right) d\tau\)
\(= \frac{1}{2\pi} \int_{-\infty}^{\infty} \exp(jbt\tau + j\omega_0 \tau - j\omega \tau) d\tau\)
\(= \delta(\omega - \omega_0 - bt).\)

# 4.9.3 Sinusoidal Signal

We compute the WVD of a pure sinusoidal signal \(e^{j\omega_0 t}\) by setting the chirp parameter \(b\) to zero. Therefore,

(4.70) \(e^{j\omega_0 t} \Longleftrightarrow \delta(\omega - \omega_0).\)

The WVDs of equations (4.67) and (4.69) on the time-frequency plane are a straight line with a slope \(b\) and a straight line parallel to the time axis, respectively. They are given in Figures 4.10 and 4.11. Figure 4.12 shows the WVD of a Gaussian modulated sinusoidal function.

FIGURE 4.10: Wigner-Ville distribution of a chirp signal.