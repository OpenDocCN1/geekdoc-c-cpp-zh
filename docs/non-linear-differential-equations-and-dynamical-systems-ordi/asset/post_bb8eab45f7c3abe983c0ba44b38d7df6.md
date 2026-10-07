
This is a second-order non-linear differential equation (4.355b) involving the constant coefficient (4.355a):

```
$b = \frac{aZ}{2\pi J}; \quad \dot{j} - \left(\pm bj\right)j \pm \frac{R}{L}j^2 = 0. \quad (4.355a, b)$
```

The corresponding autonomous system of first-order differential equations (4.355b) $\equiv$ (4.356a, b) is:

```
$j = G, \quad \dot{G} = \frac{G^2}{J} \pm bj(G+\frac{R}{L}); \quad (4.356a, b)$
```

using (4.357a) leads to the path (4.357b) in the phase plane $(J, j)$:

```
$\dot{G} = \frac{dG}{dt}\frac{dJ}{dt} = G\frac{dG}{dJ}; \quad \dot{j} = \frac{dG}{dJ} \pm bj(1+\frac{RJ}{LG}); \quad (4.357a, b)$
```

The latter (4.357b) becomes (section 3.7) a separable equation (4.358b) using the homogeneous change of variable of (4.358a):

```
$H = \frac{G}{J} = \frac{d}{dJ}(\log J); \pm bj(1+\frac{R}{LH}) = -H + \frac{d}{dJ}\frac{dH}{dJ}. \quad (4.358a, b)$
```

The integration of (4.358b) leads to:

```
$\pm bj^2 = \int \frac{LdH}{R+L}H = \int(1-\frac{R}{R+H})dH = H - \frac{R}{L}\log(R+H) + C, \quad (4.359)$
```

where C is a constant, substituting (4.356a, 4.358a) in (4.359) yields:

```
$\pm bj^2 = j-J-\frac{R}{L}\log(\frac{j}{J}+R)+CJ. \quad (4.360)$
```

When $J \to 0$ follows: from (4.360) that $j \to 0$; $H = j/J \to const$; from (4.355b) that $J \to 0$. Since $(J,j)$ vanish simultaneously there is a steady state of zero current. The electromechanical homopolar dynamo (Figure 4.16), while the relative importance of the resistance and mutual induction in (4.355a, b), always leads (4.359; 4.360) to a zero electric current if (problem 126) the braking torque of the Lorentz force is not balanced by an external driving torque. The electrochemical homopolar dynamo is reconsidered (subsection 4.7.6) in the presence of a driving torque balancing the torque of the Lorentz magnetic.

# Unsteady, Non-Linear, and Chaotic Systems

## 4.7.6 Dynamo with Driving Torque Balancing the Joule Dissipation

In the presence of a driving torque the equation (4.347d) for the angular velocity becomes (4.361a):

```
$$\Omega = M \pm \frac{aZ}{2\pi}\Omega J; \quad M\Omega = RJ^2. \quad (4.361a, b)$
```

For a steady motion, the work performed by the driving torque should balance electrical dissipation by the Joule effect (4.361b). For a general driving torque, elimination between (4.361a) and (4.344b), in (4.354), leads to:

```
$$\frac{d}{dt} \left[ \frac{1}{J} \frac{dJ}{dt} \right] = \pm \frac{Z \Omega}{2\pi L} = \pm \frac{aZ}{2\pi L} \left( \frac{a}{L} \Omega J + \frac{M}{I} \right) = \pm \frac{aZ}{2\pi IL} \left( \frac{dJ}{dt} + RJ + \frac{M}{a} \right), \quad (4.362)$
```

that has an extra term compared with (4.354). The driving torque differs the differential equation, specifying the variation with time of the electric current of the electromechanical homopolar dynamo from (4.354) = (4.355a, b) to (4.362) = (4.363):

```
$$\tilde{j} - \left( \frac{1}{J} \pm bj \right) j \left( \frac{R}{L} + \frac{M}{aL} \right) = 0. \quad (4.363)$
```

The solution of (4.363) depends on relation $(\Omega, J)$ between the driving torque, angular velocity, and electric current; if the driving torque is constant the last term in (4.363) includes a linear amplification (oscillation) for the upper — lower sign. The simplest case is the driving torque (4.361b) balancing the torque due to the Lorentz force (4.361a), leading to steady state (4.364a), the latter implies by (4.361b) a steady electric current (4.364b). In this case (4.344a) steadies the constant angular velocity $\Omega$ at (4.364c):

```
$$\Omega = 0, j = \pm \frac{2\pi R}{Z}; \quad J = \pm \frac{M\Omega}{RJ} = \pm \frac{aZ^2}{2\pi R} = \mp \frac{2\pi Ra}{Z}, \quad (4.364a–d)$
```

then (4.36b) steadies the steady electric current (4.36). Thus an electromechanical homopolar dynamo (Figure 4.16) with total induction $L$, resistance, and at constant angular velocity $\Omega$ in (4.344a) acts (problem 122) by a (4.345a–c) if the winding is to the direction of rotation, $J_-$ in Figure 4.16; (problem 123) if the winding is in the direction of current, the current is constant (4.36b) = (4.36) and decreases (exponentially) with time (4.36a) for smaller $\Omega < \Omega$ (larger $\Omega$). Taking into account the retarding torque due to the Lorentz force (4.37a–d) and the rotational moment of inertia I leads to (problem 125) an algebraic decay of the current (4.53) if the effect of resistance is small compared with that of mutual inductance; in this case the electric current is proportional to the angular velocity, and (problem 124) including the electrical resistance only leads to an exponential decay (4.52a, b). If the approximation (4.48a) is not made the equations (4.44b; 4.7d) for the electromechanical dynamo lead to (4.55a, b), whose paths in the phase plane are specified by (4.36) and include a steady state of zero. The steady rotation (4.64a, c) is compatible (4.44b) with a steady electric current (4.6b, d) if there is a driving torque balancing the torque due to the Lorentz force (4.6a) such that the mechanical work of driving torque equals electrical dissipation by the Joule effect (4.6b).

## 4.7.7 The Self-Excited Dynamo and Magnetic Field

A simple example of a first-order equation with steady solution is (4.5c) that balances the inertia force against:
(i) a quadratic damping (second term on the r.h.s.);
(ii) a linear amplification (damping) if the upper + (lower) sign is chosen in the first term on the r.h.s.:

```
a > 0 < b: m v̇ = \pm b v \pm a v^2.
```

The r.h.s. of (4.5c) with (4.5a, b) is the reverse of (4.9c) that involves linear damping or amplification. The two signs in (4.5c) lead (Figure 4.17) to two cases:
(i) in case I of the lower sign in (4.5c), the steady solution (4.6a) in the presence of linear and non-linear damping (4.6b) can only be an asymptotic decay to zero (4.6c):

```
v₋ = 0: 0 = v₋ (b + a v₋)  ⇒ \lim_{t\to\infty} v₋(t) = 0; (4.6a–c)
```

```
v₊ = 0: 0 = v₊ (−b + a v+)  ⇒ \lim_{t\to\infty} v₊(t) = b/a, (4.6a–c)
```

# FIGURE 4.17

An electromechanical homopolar disk dynamo (Figure 4.16), including rotational inertia and driving torque can lead either to a zero v�� or a constant v₊ asymptotic velocity or current. In the presence of both linear and quadratic damping there is a decay v�� to zero. In the presence of a linear amplification and non-linear damping, both decay and growth are limited, and there is an asymptotic steady state of equilibrium v₊ with a non-zero value.

![](img/6a4cb3b3bd129197bb791c4b642651c_216_0.png)

# Unsteady, Non-Linear, and Chaotic Systems

(ii) in the case II of the upper sign in (4.5c), the steady solution (4.7c) corresponds to a balance between linear amplification and quadratic damping. These expectations can be checked by solving the first order differential equation (4.5c) which is separable, and can be integrated:

```
$$\pm\frac{b}{m}t = \int_{v_0}^v \frac{dv}{v \pm av^2} = \int_{v_0}^v(\frac{1}{v} \pm \frac{a}{b})dv$$
$$= \log\left[\frac{v}{b \pm av}\right]_{v_0}^v = \log(\frac{v}{b \pm av} / \frac{v_0}{b \pm av_0}) \quad (4.8)$$
```

using a partial decomposition (section 1.39). The integrations (4.5a, b; 4.5a, b) and (4.8) are similar with the following:

```
$$\frac{R}{L} \leftrightarrow \frac{b}{m'}, \quad v \leftrightarrow L, \quad \frac{S}{R} \leftrightarrow \frac{a}{b'} \quad (4.9a–c)$$
```

The r.h.s. of (4.5c) with (4.5a, b) is the reverse of (4.9c) that involves linear damping or amplification. The two signs in (4.5c) lead (Figure 4.17) to two cases:
(i) in case I of the lower sign in (4.5c), the steady solution (4.6a) in the presence of linear and non-linear damping (4.6b) can only be an asymptotic decay to zero (4.6c):

```
v₋ = 0: 0 = v₋ (b + a v₋)  ⇒ \lim_{t\to\infty} v₋(t) = 0; (4.6a–c)
```

```
v₊ = 0: 0 = v₊ (−b + a v+)  ⇒ \lim_{t\to\infty} v₊(t) = b/a, (4.6a–c)
```
