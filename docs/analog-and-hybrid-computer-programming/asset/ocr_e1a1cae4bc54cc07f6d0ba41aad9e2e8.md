= \left[ -\frac{1}{s} e^{-st} \int_{0-}^{t} x \,dt \right]_{0-}^{\infty} + \frac{1}{s} \int_{0-}^{\infty} x e^{-st} \,dt + \frac{c}{s}

= \frac{1}{s} \mathcal{L}(f(t)) + \frac{c}{s}.

The constant $\frac{c}{s}$ is the initial value of the integral.

# B.3 Further characteristics

Given two functions $f(t)$ and $g(t)$ which can be subjected to a LAPLACE transform yielding $F(s)$ and $G(s)$, the transform has the following useful characteristics:

$\mathcal{L}(\lambda f(t) + g(t)) = \lambda F(s) + G(s)$ \quad\quad (linearity)
$\mathcal{L}(f(\lambda t)) = \frac{1}{\lambda} F\left(\frac{s}{\lambda}\right)$ \quad\quad (scale factor)
$\mathcal{L}(e^{-\beta t} f(t)) = F(s + \beta)$ \quad\quad (exponential damping)
$\mathcal{L}(f(t - T) u(t - T)) = e^{-T s} F(s)$ \quad\quad (time shift)
$\mathcal{L}((f * g)(t)) = F(s) G(s)$ \quad\quad (convolution, see (C.1))

# B.4 Inverse Laplace transform

The inverse LAPLACE transform is defined as

$f(t) = \mathcal{L}^{-1}(F(s)) = \frac{1}{2\pi i} \lim_{T \to \infty} \int_{\gamma - iT}^{\gamma + iT} e^{st} F(s) \, ds$

with $\gamma \in \mathbb{R}$ denoting a vertical line in the complex number plane. $\gamma$ is chosen so that all singularities of $F(s)$ are on its left. This transform is known as the Bromwich integral, after THOMAS JOHN L'ANSON BROMWICH and is typically solved using the residue theorem.$^{160}$