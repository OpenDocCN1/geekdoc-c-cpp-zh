(4.56) \(|G_\phi f(b, \xi)| = \frac{1}{2\pi} |\hat{\phi}(\omega_0 - \xi)|\)

(4.57) \(|W_\psi f(b, a)| = \frac{\sqrt{a}}{2\pi} |\hat{\psi}(a\omega_0)|.\)

It is clear from (4.56) and (4.57) that \(|G_\phi f(b, \xi)|\) and \(|W_\psi f(b, \xi)|\) do not depend on \(b\). On the frequency axis, since \(|\hat{\phi}(0)| = 1\) , and assuming that \(|\hat{\phi}(\omega)| \le 1, \omega \neq 0\) , we will get the maximum magnitude of STFT at \(\xi = \omega_0\). Then there will be a band around \(\xi = \omega_0\), the width of which will depend on \(\Delta \hat{\phi}\), the radius of \(\hat{\phi}(\omega)\).

Interpretation of (4.57) is a little complicated because, unlike STFT, wavelet transform does not give a time-frequency plot directly. Let us consider a point \(\omega'\) on the frequency axis such that

(4.58) \(|\hat{\psi}(\omega')| = \max \{|\hat{\psi}(\omega)|; \omega \in (0, \infty)\}.\)

For all practical purposes, we may take \(\omega' = \omega^*\).

Now if we consider a variable \(\xi = \omega^*/a\) and rewrite (4.57) in terms of the new variable \(\xi\), we have

(4.59) \(\left| W_\psi f \left( b, \frac{\omega^*}{\xi} \right) \right| = \frac{1}{2\pi} \sqrt{\frac{\omega^*}{\xi}} \left| \hat{\psi} \left( \frac{\omega^*}{\xi} \omega_0 \right) \right|.\)