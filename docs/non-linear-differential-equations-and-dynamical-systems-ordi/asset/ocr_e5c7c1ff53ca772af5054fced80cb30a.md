# Non-Linear Differential Equations and Dynamical Systems

It is clear that a particular solution of (4.7b) is (4.8a); a straight line (4.8b):

```
$z = kx; \quad y = k; \quad 0 = g(k) = bk^2 + (a-d)k - c, \quad (4.8a-c)$
```

whose k is a root of (4.8c); the binomial (4.8b) is related to the characteristic polynomial of the system of coupled first-order linear differential equations with constant coefficients:

```
$\frac{dx}{dt} = ax + by, \quad \frac{dy}{dt} = cx + dy, \quad (4.9a, b)$
```

obtained from (4.1a, b) by linearization (4.4b) at the stagnation point of degree unity at the origin; the characteristic polynomial appears in the theory (subsection 4.2.1). Since (4.8c) is a quadratic equation with real coefficients, three cases arise; (i) a real double root (subsection 4.1.4); (ii) two distinct real roots (subsections 4.1.5–4.1.7); and (iii) a pair of complex conjugate roots (subsections 4.1.8–4.1.9).

# 4.1.4 One Principal Line and Point Contact

The differential equation (4.7b), involving the quadratic expression (4.8c), is separable:(4.10a):

```
$\frac{dx}{x} = -\frac{a+b}{g(z)}dz, \quad \log x = C - \int^{y/x} \frac{a+b}{g(z)}dz, \quad (4.10a, b)$
```

and has solution (4.10b) where C is an arbitrary constant of integration. The integration in (4.10b) depends on the form of the quadratic function (4.8c); in the case (i) of a double real root the discriminant (4.11a) is zero:

```
$\Delta = (a-d)^2 + 4cb = 0; \quad g(z) = b(z-\alpha)^2, \quad \alpha = \frac{d-a}{2b}, \quad y = \alpha x, \quad (4.11a–d)$
```

and the double root (4.11b) of (4.8c) is (4.11c) and specifies one principal line (4.11d) that is a straight line, satisfying the differential equation (4.5b). The complete set are solutions of integral curves of (4.10b; 4.11b):

```
$x = C\exp(-\int^{y/x} \frac{z+a/b}{(z-\alpha)^2}dz) \n=C\exp(-\int \frac{1}{z-\alpha}\frac{\alpha+a/b}{(z-\alpha)^2}dz) \n=\frac{C}{y/x-\alpha}\exp(\frac{\alpha+a/b}{y/x-\alpha}); \quad (4.12)$
```