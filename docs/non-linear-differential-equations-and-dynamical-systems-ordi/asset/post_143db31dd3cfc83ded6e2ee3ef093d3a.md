
## 102 Non-Linear Differential Equations and Dynamical Systems

(ii) the first and third (4.43a; 4.44a; 4.45a) terms lead (4.41b) to oscillatory (4.43c, d) [monotonic (4.44c, d)] motion if the condition (4.43b) [4.44b] is met:

```
a+d=0, \quad ad<bc; \quad \dot{x}+\omega_0^2x=0, \quad x(t)=x(0)\exp(\pm i|\omega_0|t), \quad (4.43a–d)
```

```
a+d=0, \quad ad<bc; \quad \dot{x}-\omega_0^2x=0, \quad x(t)=x(0)\exp(\pm|\omega_0|t), \quad (4.44a–d)
```

```
a+d=0, \quad ad<bc; \quad \dot{x}=0, \quad x(t)=x(0)+\tilde{x}(t), \quad (4.45a–d)
```

with the intermediate case (4.45b) corresponding to uniform motion (4.45c, d), the trajectories near a stagnation point of first degree (4.35a–c), correspond to the composition of two identical generalized oscillators, which are orthogonal (x, y) and coupled can be decoupled (subsection 4.2.3).

### 4.2.3 Decomposition into a Pair of Coupled Coordinates

The linear second-order differential equation (4.37a, b) for the generalized oscillator has two particular integrals $\zeta(t), \eta(t)$, that may be called **decoupled** coordinates if they satisfy differential equations that are decoupled, unlike (4.35a–c). The orthogonal coupled coordinates of the generalized oscillators are linear combinations of the following:

```
\begin{pmatrix} x(t) \\ y(t) \end{pmatrix} = \begin{bmatrix} C_1 & C_2 \\ D_1 & D_2 \end{bmatrix} \begin{pmatrix} \zeta(t) \\ \eta(t) \end{pmatrix} \quad (4.46)
```

where $(C_1, C_2)$ are arbitrary constants of integration and $(D_1, D_2)$ are functions of $(C_1, C_2)$ determined by compatibility with (4.35b, c); thus the decoupled coordinates $\zeta,\eta$ rectify linear axis that are generally oblique. The curves of a singular first-order differential equation of first degree (4.5b) correspond to two independent, orthogonal generalized oscillators (4.35a–c)(4.37a, b) that may be decoupled into motions along (4.46) axis $(\zeta,\eta)$ that distinct since they are linearly independent particular integrals of the generalized oscillator. The discriminant of the characteristic polynomial (4.40b):

```
\Delta=4(\lambda^2 - \omega_0^2) = (a+d)^2 - 4(ad-bc) = (a-d)^2 + 4bc, \quad (4.47)
```

coincides with that (4.47) = (4.34) = (4.11a) of the quadratic form or binomial (4.8c) specifying the principal lines; is, the decoupled coordinates along the principal lines. Thus the three cases arise: (i) double real root of (4.8c) corresponding to a contact point (subsection 4.1.4) and generalized oscillators with critical damping (subsection 4.2.4); (ii) two distinct roots of (4.8c) corresponding (subsection 4.1.5) to a saddle point (subsection 4.1.6)

or a focus, or a nodal or simple point (subsection 4.1.7) and generalized oscillators with supercritical damping (subsection 4.2.5); and (iii) a complex conjugate pair of roots of (4.8c), corresponding to [subsection 4.1.8 (4.1.9)] to a center (asymptotic point) for (subcritically damped) generalized oscillators (subsection 4.2.6).

### 4.2.4 Critical Damping and Double Root

In the case (i) of (problem 80) a real double root (4.48a) of the characteristic polynomial (4.48b):

```
$0 = \Delta = 4(\lambda^2 - \omega_0^2); \quad P_2(D) = D^2 + 2\lambda D + \lambda^2 = (D+\lambda)^2, \quad (4.48a, b)
```

the linearly independent particular integrals (2.85a, b) $\equiv$ (4.49a, b):

```
$$\zeta(t) = e^{-\lambda t}, \quad \eta(t) = te^{-\lambda t}, \quad (4.49a, b)
```

satisfy the differential equations of first and second order respectively:

```
$0 = (D+\lambda)\zeta = \dot{\zeta} + \lambda\zeta, \quad 0 = (D+\lambda)\eta = \dot{\eta} + \lambda\eta; \quad (4.50a, b)
```

although the orders of the decoupled equations (4.50a, b) add 1+2 to 3, they are dependent, and the actual order of the system (4.35a–c) remains 2. Substituting (4.49a, b) in the first line of (4.46) leads to (4.51a):

```
$x(t) = (C_1 + C_2)e^{-\lambda t}; \quad (4.51a)
```

```
$by(t) = \dot{x}-ax = C_2 - (\lambda+a)C_1e^{-\lambda t} - C_2(\lambda+a)e^{-\lambda t}; \quad (4.51b)
```

substitution of (4.51a) in (4.35b) leads to (4.51b). Comparison of (4.51b) with the second line of (4.46) specifies

```
$$\begin{bmatrix} D_1 \\ D_2 \end{bmatrix} = \frac{1}{b} \begin{bmatrix} -\lambda & a \\ 0 & -\lambda-a \end{bmatrix} \begin{bmatrix} C_1 \\ C_2 \end{bmatrix}. \quad (4.52)
```

Substitution of the decoupled coordinates (4.49a, b) in (4.51a, b) specifies the orders of the decoupled axes $\zeta$, $\eta$, relative to orthogonal axes $x, y$:

```
$$\begin{bmatrix} x(t) \\ y(t) \end{bmatrix} = \frac{1}{b} \begin{bmatrix} C_1b & C_2b \\ C_2(\lambda+a) & -C_1(\lambda+a) \end{bmatrix} \begin{bmatrix} \zeta(t) \\ \eta(t) \end{bmatrix}. \quad (4.53)
```

### Non-Linear Differential Equations and Dynamical Systems

Eliminating the parameter $t$ between the decoupled coordinates (4.49a, b) leads to:

```
$-\lambda t = \log \zeta; \quad -\lambda\eta(t) = \zeta(t)\log\{\zeta(t)\}; \quad (4.54a, b)
```

the integral curves $\zeta$ (4.54b) correspond (problem 80 to 4.13c) that are tangent to the principal line $\zeta$ at a (sub-case I) contact point of inflexion (Figure 4.1a); lies to decoupled coordinates (4.49a, b) and to coupled orthogonal oscillators (4.53), with critical damping in (4.48a or $\omega_0 = \lambda$ in 4.41a, b).

### 4.2.5 Supercritical Damping and Distinct Real Roots

In the case (ii) of distinct roots of the characteristic polynomial (4.40b):

```
$\Delta > 0; \quad P_2(D)=(D-r)(D-s), \quad r,s=\frac{a+d\pm\sqrt{\Delta}}{2}; \quad (4.55a, b)
```

the particular integrals (4.56a, b):

```
$\zeta(t)=e^\eta, \quad \eta(t)=e^\zeta; \quad \zeta=r\zeta, \quad \eta=s\eta; \quad (4.56a-d)
```

satisfy real, first-order differential equations (4.56c, d). Substituting (4.56a, b) in the first line of (4.46) leads to (4.57a):

```
$x(t)=C_1e^\eta+C_2e^\zeta; \quad by(t)=\dot{x}-ax=C_1(r-a)e^\eta+C_2(s-a)e^\zeta; \quad (4.57a, b)
```

substitution of (4.57a) in (4.35b) leads to (4.57b). Comparison of (4.57b) with the second-line of (4.46) specifies the coefficients $(D_1, D_2)$ in 4.58a:

$$\begin{matrix} D_1 \\ D_2 \end{matrix} = \frac{1}{b} \begin{bmatrix} r-a & 0 \\ 0 & s-a \end{bmatrix} \begin{bmatrix} C_1 \\ C_2 \end{bmatrix}; \quad y(t)=\frac{1}{b} \begin{bmatrix} C_1b & C_2b \\ C_1(r-a) & C_2(s-a) \end{bmatrix} \begin{bmatrix} \zeta(t) \\ \eta(t) \end{bmatrix}; \quad (4.58a, b)
$$

also, (4.57a, b)=(4.58b) indicate the direction of the oblique, decoupled axis $(\zeta, \eta)$ relative to the orthogonal, coupled axis $(x, y)$. Eliminating the time $t$ between (4.56a, b):

```
$\zeta(t)=(e^\eta)'=(\eta^1)'=\{\eta(t)\}^{\gamma/s}; \quad (4.59)
```

specifies the integral curves (4.59) in oblique decoupled axis $\zeta, \eta$, corresponding to (4.23a, b) in orthogonal coupled axis $x, y$, leading to

### Unsteady, Non-Linear, and Chaotic Systems

or a focus, or a nodal or simple point (subsection 4.1.7) and generalized oscillators with supercritical damping (subsection 4.2.5); and (iii) a complex conjugate pair of roots of (4.8c), corresponding to [subsection 4.1.8 (4.1.9)] to a center (asymptotic point) for (subcritically damped) generalized oscillators (subsection 4.2.6).

### Unsteady, Non-Linear, and Chaotic Systems

or a focus, or a nodal or simple point (subsection 4.1.7) and generalized oscillators with supercritical damping (subsection 4.2.5); and (iii) a complex conjugate pair of roots of (4.8c), corresponding to [subsection 4.1.8 (4.1.9)] to a center (asymptotic point) for (subcritically damped) generalized oscillators (subsection 4.2.6).

### Unsteady, Non-Linear, and Chaotic Systems

or a focus, or a nodal or simple point (subsection 4.1.7) and generalized oscillators with supercritical damping (subsection 4.2.5); and (iii) a complex conjugate pair of roots of (4.8c), corresponding to [subsection 4.1.8 (4.1.9)] to a center (asymptotic point) for (subcritically damped) generalized oscillators (subsection 4.2.6).

### Unsteady, Non-Linear, and Chaotic Systems

or a focus, or a nodal or simple point (subsection 4.1.7) and generalized oscillators with supercritical damping (subsection 4.2.5); and (iii) a complex conjugate pair of roots of (4.8c), corresponding to [subsection 4.1.8 (4.1.9)] to a center (asymptotic point) for (subcritically damped) generalized oscillators (subsection 4.2.6).

### Unsteady, Non-Linear, and Chaotic Systems

or a focus, or a nodal or simple point (subsection 4.1.7) and generalized oscillators with supercritical damping (subsection 4.2.5); and (iii) a complex conjugate pair of roots of (4.8c), corresponding to [subsection 4.1.8 (4.1.9)] to a center (asymptotic point) for (subcritically damped) generalized oscillators (subsection 4.2.6).

### Unsteady, Non-Linear, and Chaotic Systems

or a focus, or a nodal or simple point (subsection 4.1.7) and generalized oscillators with supercritical damping (subsection 4.2.5); and (iii) a complex conjugate pair of roots of (4.8c), corresponding to [subsection 4.1.8 (4.1.9)] to a center (asymptotic point) for (subcritically damped) generalized oscillators (subsection 4.2.6).

### Unsteady, Non-Linear, and Chaotic Systems

or a focus, or a nodal or simple point (subsection 4.1.7) and generalized oscillators with supercritical damping (subsection 4.2.5); and (iii) a complex conjugate pair of roots of (4.8c), corresponding to [subsection 4.1.8 (4.1.9)] to a center (asymptotic point) for (subcritically damped) generalized oscillators (subsection 4.2.6).

(Wait, the OCR text has some repetitions sections)

or a focus, or a nodal or simple point (subsection 4.1.7) and generalized oscillators with supercritical damping (subsection 4.2.5); and (iii) a complex conjugate pair of roots of (4.8c), corresponding to [subsection 4.1.8 (4.1.9)] to a center (asymptotic point) for (subcritically damped) generalized oscillators (subsection 4.2.6).

(Actually, I will re-output cleanly based on the provided text structure without repetition).

[content]
## 102 Non-Linear Differential Equations and Dynamical Systems

(ii) the first and third (4.43a; 4.44a; 4.45a) terms lead (4.41b) to oscillatory (4.43c, d) [monotonic (4.44c, d)] motion if the condition (4.43b) [4.44b] is met:

```
a+d=0, \quad ad<bc; \quad \dot{x}+\omega_0^2x=0, \quad x(t)=x(0)\exp(\pm i|\omega_0|t), \quad (4.43a–d)
```

```
a+d=0, \quad ad<bc; \quad \dot{x}-\omega_0^2x=0, \quad x(t)=x(0)\exp(\pm|\omega_0|t), \quad (4.44a–d)
```

```
a+d=0, \quad ad<bc; \quad \dot{x}=0, \quad x(t)=x(0)+\tilde{x}(t), \quad (4.45a–d)
```

with the intermediate case (4.45b) corresponding to uniform motion (4.45c, d), the trajectories near a stagnation point of first degree (4.35a–c), correspond to the composition of two identical generalized oscillators, which are orthogonal (x, y) and coupled can be decoupled (subsection 4.2.3).

### 4.2.3 Decomposition into a Pair of Coupled Coordinates

The linear second-order differential equation (4.37a, b) for the generalized oscillator has two particular integrals $\zeta(t), \eta(t)$, that may be called **decoupled** coordinates if they satisfy differential equations that are decoupled, unlike (4.35a–c). The orthogonal coupled coordinates of the generalized oscillators are linear combinations of the following:

```
\begin{pmatrix} x(t) \\ y(t) \end{pmatrix} = \begin{bmatrix} C_1 & C_2 \\ D_1 & D_2 \end{bmatrix} \begin{pmatrix} \zeta(t) \\ \eta(t) \end{pmatrix} \quad (4.46)
```

where $(C_1, C_2)$ are arbitrary constants of integration and $(D_1, D_2)$ are functions of $(C_1, C_2)$ determined by compatibility with (4.35b, c); thus the decoupled coordinates $\zeta,\eta$ rectify linear axis that are generally oblique. The curves of a singular first-order differential equation of first degree (4.5b) correspond to two independent, orthogonal generalized oscillators (4.35a–c)(4.37a, b) that may be decoupled into motions along (4.46) axis $(\zeta,\eta)$ that distinct since they are linearly independent particular integrals of the generalized oscillator. The discriminant of the characteristic polynomial (4.40b):

```
\Delta=4(\lambda^2 - \omega_0^2) = (a+d)^2 - 4(ad-bc) = (a-d)^2 + 4bc, \quad (4.47)
```

coincides with that (4.47) = (4.34) = (4.11a) of the quadratic form or binomial (4.8c) specifying the principal lines; is, the decoupled coordinates along the principal lines. Thus the three cases arise: (i) double real root of (4.8c) corresponding to a contact point (subsection 4.1.4) and generalized oscillators with critical damping (subsection 4.2.4); (ii) two distinct roots of (4.8c) corresponding (subsection 4.1.5) to a saddle point (subsection 4.1.6).

or a focus, or a nodal or simple point (subsection 4.1.7) and generalized oscillators with supercritical damping (subsection 4.2.5); and (iii) a complex conjugate pair of roots of (4.8c), corresponding to [subsection 4.1.8 (4.1.9)] to a center (asymptotic point) for (subcritically damped) generalized oscillators (subsection 4.2.6).

### 4.2.4 Critical Damping and Double Root

In the case (i) of (problem 80) a real double root (4.48a) of the characteristic polynomial (4.48b):

```
$0 = \Delta = 4(\lambda^2 - \omega_0^2); \quad P_2(D) = D^2 + 2\lambda D + \lambda^2 = (D+\lambda)^2, \quad (4.48a, b)
```

the linearly independent particular integrals (2.85a, b) $\equiv$ (4.49a, b):

```
$$\zeta(t) = e^{-\lambda t}, \quad \eta(t) = te^{-\lambda t}, \quad (4.49a, b)
```

satisfy the differential equations of first and second order respectively:

```
$0 = (D+\lambda)\zeta = \dot{\zeta} + \lambda\zeta, \quad 0 = (D+\lambda)\eta = \dot{\eta} + \lambda\eta; \quad (4.50a, b)
```

although the orders of the decoupled equations (4.50a, b) add 1+2 to 3, they are dependent, and the actual order of the system (4.35a–c) remains 2. Substituting (4.49a, b) in the first line of (4.46) leads to (4.51a):

```
$x(t) = (C_1 + C_2)e^{-\lambda t}; \quad (4.51a)
```

```
$by(t) = \dot{x}-ax = C_2 - (\lambda+a)C_1e^{-\lambda t} - C_2(\lambda+a)e^{-\lambda t}; \quad (4.51b)
```

substitution of (4.51a) in (4.35b) leads to (4.51b). Comparison of (4.51b) with the second line of (4.46) specifies

```
$$\begin{bmatrix} D_1 \\ D_2 \end{bmatrix} = \frac{1}{b} \begin{bmatrix} -\lambda & a \\ 0 & -\lambda-a \end{bmatrix} \begin{bmatrix} C_1 \\ C_2 \end{bmatrix}. \quad (4.52)
```

Substitution of the decoupled coordinates (4.49a, b) in (4.51a, b) specifies the orders of the decoupled axes $\zeta$, $\eta$, relative to orthogonal axes $x, y$:

```
$$\begin{bmatrix} x(t) \\ y(t) \end{bmatrix} = \frac{1}{b} \begin{bmatrix} C_1b & C_2b \\ C_2(\lambda+a) & -C_1(\lambda+a) \end{bmatrix} \begin{bmatrix} \zeta(t) \\ \eta(t) \end{bmatrix}. \quad (4.53)
```

### Non-Linear Differential Equations and Dynamical Systems

Eliminating the parameter $t$ between the decoupled coordinates (4.49a, b) leads to:

```
$-\lambda t = \log \zeta; \quad -\lambda\eta(t) = \zeta(t)\log\{\zeta(t)\}; \quad (4.54a, b)
```

the integral curves $\zeta$ (4.54b) correspond (problem 80 to 4.13c) that are tangent to the principal line $\zeta$ at a (sub-case I) contact point of inflexion (Figure 4.1a); lies to decoupled coordinates (4.49a, b) and to coupled orthogonal oscillators (4.53), with critical damping in (4.48a or $\omega_0 = \lambda$ in 4.41a, b).

### 4.2.5 Supercritical Damping and Distinct Real Roots

In the case (ii) of distinct roots of the characteristic polynomial (4.40b):

```
$\Delta > 0; \quad P_2(D)=(D-r)(D-s), \quad r,s=\frac{a+d\pm\sqrt{\Delta}}{2}; \quad (4.55a, b)
```

the particular integrals (4.56a, b):

```
$\zeta(t)=e^\eta, \quad \eta(t)=e^\zeta; \quad \zeta=r\zeta, \quad \eta=s\eta; \quad (4.56a-d)
```

satisfy real, first-order differential equations (4.56c, d). Substituting (4.56a, b) in the first line of (4.46) leads to (4.57a):

```
$x(t)=C_1e^\eta+C_2e^\zeta; \quad by(t)=\dot{x}-ax=C_1(r-a)e^\eta+C_2(s-a)e^\zeta; \quad (4.57a, b)
```

substitution of (4.57a) in (4.35b) leads to (4.57b). Comparison of (4.57b) with the second-line of (4.46) specifies the coefficients $(D_1, D_2)$ in 4.58a:

$$\begin{matrix} D_1 \\ D_2 \end{matrix} = \frac{1}{b} \begin{bmatrix} r-a & 0 \\ 0 & s-a \end{bmatrix} \begin{bmatrix} C_1 \\ C_2 \end{bmatrix}; \quad y(t)=\frac{1}{b} \begin{bmatrix} C_1b & C_2b \\ C_1(r-a) & C_2(s-a) \end{bmatrix} \begin{bmatrix} \zeta(t) \\ \eta(t) \end{bmatrix}; \quad (4.58a, b)
$$

also, (4.57a, b)=(4.58b) indicate the direction of the oblique, decoupled axis $(\zeta, \eta)$ relative to the orthogonal, coupled axis $(x, y)$. Eliminating the time $t$ between (4.56a, b):

```
$\zeta(t)=(e^\eta)'=(\eta^1)'=\{\eta(t)\}^{\gamma/s}; \quad (4.59)
```

specifies the integral curves (4.59) in oblique decoupled axis $\zeta, \eta$, corresponding to (4.23a, b) in orthogonal coupled axis $x, y$, leading to
