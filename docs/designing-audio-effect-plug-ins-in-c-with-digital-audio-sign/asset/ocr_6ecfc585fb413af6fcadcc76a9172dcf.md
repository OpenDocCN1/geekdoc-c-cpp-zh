H(z) = a_0 \frac{1}{1 + b_1 z^{-1} + b_2 z^{-2}}
= \frac{1}{1 - 1.34z^{-1} + 0.902z^{-2}}
Let z = e^{j\omega}.
H(\omega) = \frac{1}{1 - 1.34e^{-j\omega} + 0.902e^{-j2\omega}}

Apply Euler's equation: 1

H(\omega) = \frac{1}{1 - 1.34e^{-j\omega} + 0.902e^{-j2\omega}}
H(\omega) = \frac{1}{1 - 1.34[\cos(\omega) - j\sin(\omega)] + 0.902[\cos(2\omega) - j\sin(2\omega)]}

Now evaluate for each of our four frequencies starting with DC.

# ## 5.18.1 DC (0 Hz)

H(\omega) = \frac{1}{1 - 1.34[\cos(\omega) - 1 - j0 j\sin(\omega)] + 0.902[\cos(2\omega) - j\sin(2\omega)]}
= \frac{1}{1 - 1.34[\cos(0) - j\sin(0)] + 0.902[\cos(2*0) - j\sin(2*0)]}
= \frac{1}{1 - 1.34[1 - j0] + 0.902} (5.76)
= \frac{1}{1 - 1.34 + 0.902}
= \frac{1}{0.562 + j0}

H(\omega) = \frac{1}{0.562 + j0}
|H(\omega)| = \frac{|1|}{|0.562 + j0|}
= \frac{1}{\sqrt{a^2 + b^2}} (5.77)
= \frac{1}{\sqrt{0.562^2}} = 1.78 = 5.00 \text{ dB}
\text{Arg}(H) = \text{Arg(Num)} - \text{Arg(Denom)}
= \tan^{-1}(0/1) - \tan^{-1}(0/0.562)
= 0^\circ

Remember that for magnitudes of fractions, you need to take the magnitude of the numerator and denominator separately; also for phase, the total is the difference of the Arg(num) and Arg(denom). The direct evaluation yields 5.0 dB and shows our sketch evaluation was a little off at 5.9 dB.