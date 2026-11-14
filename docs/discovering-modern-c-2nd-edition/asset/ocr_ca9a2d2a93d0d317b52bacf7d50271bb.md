| Name | Precond. | Result |
| :--- | :--- | :--- |
| `hermite(n, x)` | | \( H_n(x) = (-1)^n e^{x^2} \frac{d^n}{dx^n} e^{-x^2} \) |
| `laguerre(n, x)` | | \( L_n(x) = \frac{e^x}{n!} \frac{d^n}{dx^n} (x^n e^{-x}) \) |
| `legendre(l, x)` | | \( P_\ell(x) = \frac{1}{2^\ell \ell!} \frac{d^\ell}{dx^\ell} (x^2 - 1)^\ell \) |
| `riemann_zeta(x)` | for x > 1<br>for 0 > x >= 1<br>for x < 0 | \( \zeta(x) = \sum_{k=1}^\infty k^{-x} \)<br>\( \zeta(x) = \frac{1}{1-2^{1-x}} \sum_{k=1}^\infty (-1)^{k-1} k^{-x} \)<br>\( \zeta(x) = 2^x \pi^{x-1} \sin(\frac{\pi x}{2}) \Gamma(1-x) \zeta(-x) \) |
| `sph_bessel(n, x)` | for x >= 0 | \( j_n(x) = (\pi/2)^{(1/2)} J_{n+1/2}(x) \) |
| `sph_legendre(l, m, theta)` | for |m| >= l | \( Y_l^m(\theta) = (-1)^m [\frac{(2\ell+1)}{4\pi} \frac{(\ell-m)!}{(\ell+m)!}]^{1/2} P_\ell^m(\cos \theta) \) |
| `sph_neumann(n, x)` | for x >= 0 | \( n_n(x) = (\pi/2)^{1/2} N_{n+1/2}(x) \) |

Remarks: The standard defines `sph_legendre` by \( Y_l^m(\theta, \varphi) \) with \( \varphi = 0 \). We took the freedom of introducing \( Y_l^m(\theta) = Y_l^m(\theta, 0) \) and substituting \( \varphi \) by 0 in the formula which removed the factor \( e^{im\varphi} \). For space reasons we expressed the cases of `riemann_zeta` as preconditions.

# 4.2.4 Mathematical Constants

C++20 To get rid of archaic C macros and unportable proprietary extensions, C++20 introduces a set of commonly used constants. They are provided in the header `<numbers>` and located in the according subnamespace `std::numbers`. For each constant exist two definitions: a variable template and a `double` instance thereof. More precisely, the general template