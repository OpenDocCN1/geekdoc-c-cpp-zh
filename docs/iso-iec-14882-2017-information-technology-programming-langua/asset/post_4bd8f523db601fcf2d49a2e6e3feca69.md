
# ISO/IEC 14882:2017(E)

- 1. If any argument of arithmetic type corresponding to a double parameter has type long double, then all arguments of arithmetic type (6.9.1) corresponding to double parameters are effectively cast to long double.
- 2. Otherwise, if any argument of arithmetic type corresponding to a double parameter has type double or an integer type, all arguments of arithmetic type corresponding to double parameters are effectively cast to double.
- 3. Otherwise, all arguments of arithmetic type corresponding to double parameters have type float. [Note: abs is exempted from these rules in order to stay compatible with C. — end note]

SEE ALSO: ISO C 7.12

## 29.9.2 Absolute values [c.math.abs]

- 1. [Note: The headers <stdlib.h> (21.2.2) and <math.h> (29.9.1) declare the functions described in this subclass. — end note]

```
int abs(int j);
long abs(long j);
long long abs(long int j);
float abs(float j);
double abs(double j);
long double abs(long double j);
```

- 2. Effects: The abs functions have the semantics in the C standard library for the functions abs, labs, fabsf, and fabsl.
- 3. Remarks: If abs() is called with an argument of type X for which is_unsigned_v<X> is true and X cannot be converted to int by integral promotion (7.6), the function is ill-formed. [Note: Arguments that can be promoted to int are permitted for compatibility with C. — end note]

SEE ALSO: ISO C 7.12.7, 7.26.1.

## 29.9.3 Three-dimensional hypoten [c.math.hypot]

```
float hypot(float x, float y, float z);
double hypot(double x, double y, double z);
long double hypot(long double x, long double y, long double z);
```

- 1 Returns: $\sqrt{x^2 + y^2 + z^2}$.

## 29.9.4 Classification / companion functions [c.math.fpclass]

- 1 The classification / comparison functions behave the same as the C macros defined in the standard library. Each function is loaded for the floating-point types.

SEE ALSO: ISO C 7.12.3, 7.12.4.

## 29.9.5 Mathematical special functions [sf.math]

- 1 If any argument value to any of the functions in this clause is NaN (Not a Number), the function shall return NaN but not report domain error. Otherwise, the function shall report domain error for argument values for:
    - (1.1) — the function description's Returns clause explicitly specifies double and those argument falls the specified domain, or
    - (1.2) — the corresponding mathematical value has nonzero imaginary component, or
    - (1.3) — the corresponding mathematical function is not defined.
- 2 Unless otherwise specified, each function is defined for all finite values, negative infinity, and for positive infinity.

### 29.9.5.1 Associated Laguerre polynomials

- 1 Effects: These functions compute the Laguerre polynomials of their respective arguments n, and x.
- 2 Returns: $L_n^m(x) = (-1)^m \frac{d^m}{dx^m} L_{n+m}(x), \quad x \ge 0$
where n is n, m is m, and x is x.
- 3 Remarks: The effect of calling each of these functions is implementation-defined if n >= 1 or m >= 1.

### 29.9.5.2 Associated Legendre functions

- 1 Effects: These functions compute the Associated Legendre functions of their respective arguments l, and x.
- 2 Returns: $P_l^m(x) = (1-x)^{m/2} \frac{d^m}{dx^m} P_l(x), \quad |x| \le 1$
where l is l, m is m, and x is x.
- 3 Remarks: The effect of calling each of these functions is implementation-defined if l > 1.

### 29.9.5.3 Beta function

- 1 Effects: These functions compute the beta function of their respective arguments x and y.
- 2 Returns: $B(x,y) = \frac{\Gamma(x)}{\Gamma(x+y)}, \quad x > 0, y > 0$
where x is x and y is y.

### 29.9.5.4 Complete elliptic integral of the first kind

```
double comp_ellint_1(double k);
float comp_ellint_1(float k);
long double comp_ellint_1(long double k);
```

- 2 A mathematical function is defined for a set of argument values (a) if it is explicitly defined for set of argument values, or (b) if its limiting value exists and does not depend on the direction of approach.
- 3 Effects: These functions compute the complete elliptic integral of the first kind of their respective arguments k.
- 4 Returns: $K(k) = F(k, \pi/2), \text{ for } |k| \le 1$
where $k$ is $k$.

### 29.9.5.5 Complete elliptic integral of the second kind [sf.cmath.comp_elliptic_2]

```
double comp_elliptic_2(double k);
float comp_elliptic_2f(float k);
long double comp_elliptic_2f(long double k);
```

- 1 Effects: These functions compute the complete elliptic integral of the second kind of their respective arguments k.
- 2 Returns: $E(k) = E(k, \pi/2), \text{ for } |k| \le 1$
where $k$ is $k$.

### 29.9.5.6 Complete elliptic integral of the third kind [sf.cmath.comp_elliptic_3]

```
double comp_elliptic_3(double k, double nu);
float comp_elliptic_3f(float k, float nu);
long double comp_elliptic_3f(long double k, long double nu);
```

- 1 Effects: These functions compute the complete elliptic integral of the third kind of their respective arguments k and nu.
- 2 Returns: $\Pi(\nu, k) = \Pi(\nu, \pi/2), \text{ for } |k| \le 1$
where $k$ is $k$ and $\nu$ is $\nu$.

### 29.9.5.7 Regular modified cylindrical Bessel functions [sf.cmath.bessel_i]

```
double cyl_bessel_i(double nu, double x);
float cyl_bessel_i(float nu, float x);
long double cyl_bessel_i(long double nu, long double x);
```

- 1 Effects: These functions compute the regular modified cylindrical Bessel functions of their respective arguments nu and x.
- 2 Returns: $I_{\nu}(x) = i^{-\nu}J_{\nu}(x) = \sum_{k=0}^{\infty} \frac{(x/2)^{\nu+2k}}{k!\Gamma(\nu+k+1)} \text{ for } x \ge 0$
where $\nu$ is $\nu$ and $x$ is $x$.
- 3 Remarks: The effect of calling each of these functions is implementation-defined if nu >= 1.

### 29.9.5.8 Cylindrical Bessel functions of the first kind

```
double cyl_bessel_j(double nu, double x);
float cyl_bessel_j(float nu, float x);
long double cyl_bessel_j(long double nu, long double x);
```

- 1 Effects: These functions compute the cylindrical Bessel functions of the first kind of their respective arguments nu and x.
- 2 Returns: $J_{\nu}(x) = \sum_{k=0}^{\infty} \frac{(-1)^k(x/2)^{\nu+2k}}{k!\Gamma(\nu+k+1)}$
where $\nu$ is $\nu$ and $x$ is $x$.
- 3 Remarks: The effect of calling each of these functions is implementation-defined if nu >= 1.

### 29.9.5.9 Irregular modified Bessel functions

```
double cyl_bessel_x(double nu, double x);
float cyl_bessel_x(float nu, float x);
long double cyl_bessel_x(long double nu, long double x);
```

- 1 Effects: These functions compute the irregular modified Bessel functions of their respective arguments nu and x.
- 2 Returns: $K_{\nu}(x) = \frac{\pi}{2} \frac{I_{\nu}(x) + I_{\nu}(-x)}{\sin(\nu\pi)}$
where $\nu$ is $\nu$ and $x$ is $x$.
- 3 Remarks: The effect of calling each of these functions is implementation-defined if nu >= 1.

### 29.9.5.10 Cylindrical Neumann functions

```
double cyl_neumann(double nu, double x);
float cyl_neumann(float nu, float x);
long double cyl_neumann(long double nu, long double x);
```

- 1 Effects: These functions compute the cylindrical Neumann functions, also as the cylindrical Bessel functions of the second kind, of their respective nu and x.
- 2 Returns: $N_{\nu}(x) = \frac{J_{\nu}(x)\cos(\nu\pi)-Y_{\nu}(x)}{\sin(\nu\pi)}$
