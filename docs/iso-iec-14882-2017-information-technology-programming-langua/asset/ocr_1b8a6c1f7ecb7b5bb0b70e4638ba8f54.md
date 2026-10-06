# ISO/IEC 14882:2017

# 29.9.5.15 Hermite polynomials [sf.cmath.hermite]

double hermite(unsigned n, double x);
float hermite(unsigned n, float x);
long double hermite(unsigned n, long x);

+   1 Effects: These functions compute the Hermite polynomials of their respective arguments n and x.

+   2 Returns:

$H_n(x) = (-1)^n e^{x^2} \frac{d^n}{dx^n} e^{-x^2}$

where n is n and x is x.

+   3 Remarks: The calling of each of these functions is implementation-defined if n >= 128.

# 29.9.5.16 Laguerre polynomials [sf.cmath.laguerre]

double laguerre(unsigned n, double x);
float laguerre(unsigned n, float x);
long double laguerre(unsigned n, long x);

+   1 Effects: These functions compute the Laguerre polynomials of their respective arguments n and x.

+   2 Returns:

$L_n(x) = \frac{e^x}{n!} \frac{d^n}{dx^n} (x^n e^{-x})$, for $x \ge 0$

where n is n and x is x.

+   3 Remarks: The calling of each of these functions is implementation-defined if n >= 128.

# 29.9.5.17 Legendre polynomials [sf.cmath.legendre]

double legendre(unsigned n, double x);
float legendre(unsigned n, float x);
long double legendre(unsigned n, long x);

+   1 Effects: These functions compute the Legendre polynomials of their respective arguments 1 and x.

+   2 Returns:

$P_l(x) = \frac{1}{2^l!} \frac{d^l}{dx^l}(x^2-1)^l$, for $|x| \le 1$

where l is l and x is x.

+   3 Remarks: The calling of each of these functions is implementation-defined if 1 >= 128.

# 29.9.5.18 Riemann zeta function [sf.cmath.emann_zeta]

double riemann_zeta(double x);
float riemann_zeta(float x);
long double riemann_zetal(long x);

+   1 Effects: These functions compute the Riemann zeta function of their respective arguments n.

+   2 Returns:

$$\zeta(x) = \sum_{k=1}^{\infty} k^{-x}$, for $x > 1$\n\sum_{k=1}^{\infty}(-1)^{k-1}k^{-k-1}$, for $0 \le x \le 1$\n2^{1-x}\sin(\frac{\pi x}{2})\Gamma(1-x)\zeta(1-x)$, for $x < 0$

§ 29.9.5.18 ©ISO/IEC 2017 - All rights reserved 1151