# ISO/IEC 14882:2017(E)

where $x$ is is.

# 29.9.5.19 Spherical Bessel functions of the first kind

```
double spb_bessel(unsigned n, double x);
float spb_besself(unsigned n, float x);
long double spb_bessel(unsigned n, long x);
```

+   * Effects: These functions compute the spherical Bessel functions of the first kind of their respective arguments n and x

+   * Returns:
$j_n(x) = (\pi/2x)^{1/2}J_{n+1/2}(x)$, for $x \ge 0$

where $n$ is n and $x$ is x.

+   * Remarks: The effect of calling each of these functions is implementation-defined if $n \ge 128$.

+   * See 29.9.5.8.

# 29.9.5.20 Spherical associated Legendre functions

```
double spb_legendre(unsigned l, unsigned m, double theta);
float spb_legendref(unsigned l, unsigned m, float theta);
long double spb_legendrel(unsigned l, unsigned m, long theta);
```

+   * Effects: These functions compute the spherical associated Legendre functions of their respective arguments l, m, and theta (measured in radians).

+   * Returns:
$Y_l^m(\theta)$

where
$Y_l^m(\theta, \phi) = (-1)^m \sqrt{\frac{(2l+1)}{4\pi(l-m)!(l+m)!}} P_l^m(\cos\theta)e^{im\phi}$, for $|m| \le l$
and $l$ and $m$ are m and theta, and $\theta$ is theta.

+   * Remarks: The effect of calling each of these functions is implementation-defined if $l \ge 128$.

+   * See 29.9.5.2.

# 29.9.5.21 Spherical Neumann functions

```
double spb_neumann(unsigned n, double x);
float spb_neumannf(unsigned n, float x);
long double spb_neumann(unsigned n, long x);
```

+   * Effects: These functions compute the spherical Neumann functions, also known as the Bessel functions of the second kind, and respect arguments n and x.

+   * Returns:
$n_n(x) = (\pi/2x)^{1/2}N_{n+1/2}(x)$, for $x \ge 0$

where $n$ is n and $x$ is x.

+   * Remarks: The effect of calling each of these functions is implementation-defined if $n \ge 128$.

+   * See 29.9.5.10.