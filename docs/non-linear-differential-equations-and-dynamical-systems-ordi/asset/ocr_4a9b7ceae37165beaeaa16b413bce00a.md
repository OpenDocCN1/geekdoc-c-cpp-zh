# Non-Linear Differential Equations and Dynamical Systems

The integral (4.242b) can be re-written in the form:

```
$$\omega_t\sqrt{1+\gamma} = \int_{0}^{x/a} \frac{y^2}{1+\gamma} \frac{\gamma}{1+\gamma} dy = \int_{0}^{x/a} \left(1-y^2\right) \left(1+\frac{\gamma}{1+\gamma} y^2\right)^{-1/2} dy,\$
$$(4.243)$
```

that coincides with the inverse elliptic since function (4.240a, b) with (4.244a-c):

```
$z=\frac{x}{a} \quad \zeta = \omega_t\sqrt{1+\gamma}\sqrt{1+\frac{\beta a^2}{2}}, \quad q^2=-\frac{\gamma}{1+\gamma}-\frac{\beta a^2}{2+\beta a^2}},$\n$$(4.244a-c)$
```

It has been that the *trajectory* of a *non-linear oscillator* (4.215a) with bicadratic potential (4.215b) is specified (problem 109) by the elliptic sine function (4.245):

```
$x=asn(\omega_t\sqrt{1+\gamma}\sqrt{-\gamma/(1+\gamma)}),$\n$$(4.245)$
```

involving: (i) the amplitude (4.220b) that is a root of (4.218d); (ii) the natural frequency (4.221c)$\equiv$ (2.54a) of the harmonic oscillator; (iii) the non-linearity parameter (4.236a) which specifies the modulus (4.244c) and modifies the variable (4.244a). In (4.245) the modulus from (4.44c) is imaginary (real) for the hard $\gamma>0$ (soft $\gamma<0$) spring. The exact oscillation frequency of the anharmonic oscillator is distinct from the natural frequency of the harmonic oscillator and depends on the amplitude (subsection 4.4.11). It is obtained from the expansion of the inverse elliptic sine as a series of circular fines (subsection 4.4.10). This leads to a series of Chebyshev polynomials of the second kind (subsection 4.4.12) which specifies exactly the trajectory of the harmonic oscillator in inverse form with time as a function of.

# 4.4.10 Inverse Elliptic Sine as a Series of Circular Sines

The changes of variable (4.246a, b) simplify the elliptic integral (4.240b; 4.244b-c):

```
$$\sin\phi=z=\frac{x}{a}; \quad \sin\psi=y=\frac{\xi}{a}; \quad \omega_t\sqrt{1+\gamma} = \int_{0}^{\sin\phi} \left|1-q^2\sin^2\psi\right|^{-1/2} d\psi$\n$$(4.244a-c)$$\n$$$x=asn(\sin\phi;q)$.
```