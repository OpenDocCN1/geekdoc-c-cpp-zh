Using Parseval identity, we have

F(t) := \int_{-\infty}^{\infty} f(t+t)\overline{f(t)}dt
= \frac{1}{2\pi} \int_{-\infty}^{\infty} |\hat{f}(\omega)|^2 e^{-j\omega t} d\omega
= \frac{1}{2\pi} \sum_{k=-\infty}^{\infty} \int_{2k\pi}^{2\pi(k+1)} |\hat{f}(\omega)|^2 e^{-j\omega t} d\omega
= \frac{1}{2\pi} \int_{0}^{2\pi} \sum_{k=-\infty}^{\infty} |\hat{f}(\omega + 2k\pi)|^2 e^{-j\omega t} d\omega.
(7.56)

It is clear the \( F(\cdot) \) is the \( k \)th Fourier coefficient of a \( 2\pi \)-periodic function \( \sum_{k=-\infty}^{\infty} |\hat{f}(\omega + 2k\pi)|^2 \). With this relation (7.55) follows directly. It is easy to show that

\int_{-\infty}^{\infty} N_m(t+k)\overline{N_m(t)}dt = N_{2m}(m+k)
(7.57)

with \( supp \ N_{2m}(t) = [0, 2m] \).

Combining (7.51), (7.53), and (7.54) and taking the inverse Fourier transform, we get

a_k = (\{\tilde{a}_n\} * p[n])(k)
(7.58)

where