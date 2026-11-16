where we have assumed $T = 2\pi$ to be the period of $f_p(t)$. Consequently, $\omega_0 = 2\pi/T = 1$, and the Fourier series representation of $f_p(t)$ is

(3.54) $$f_p(t) = \sum_{k=-\infty}^{\infty} c_k e^{jkt}$$

with the coefficient $c_k$ given by

(3.55) $$\begin{aligned} c_k &= \frac{1}{2\pi} \int_0^{2\pi} f_p(t) e^{-jkt} dt \\ &= \frac{1}{2\pi} \int_0^{2\pi} \sum_{n \in \mathbb{Z}} f(t+2\pi n) e^{-jkt} dt \\ &= \frac{1}{2\pi} \sum_{n \in \mathbb{Z}} \int_0^{2\pi} f(t+2\pi n) e^{-jkt} dt \\ &= \frac{1}{2\pi} \sum_{n \in \mathbb{Z}} \int_{2\pi n}^{2\pi(n+1)} f(\xi) e^{-jk(\xi-2\pi n)} d\xi, \end{aligned}$$

where a change of variable $\xi = t + 2\pi n$ has been used. Since the summation and the integration limits effectively extend the integration over the entire real line $\mathbb{R}$, we may write

(3.56) $$\begin{aligned} c_k &= \frac{1}{2\pi} \int_{-\infty}^{\infty} f(\xi) e^{-jk\xi} d\xi \\ &= \frac{1}{2\pi} \hat{f}(k), \end{aligned}$$