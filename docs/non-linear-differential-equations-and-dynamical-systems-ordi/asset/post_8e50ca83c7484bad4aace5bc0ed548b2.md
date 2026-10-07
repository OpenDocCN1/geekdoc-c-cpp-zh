
by a dissipation function (4.340b) that equals is the work performed by the friction force per unit time:

```
dW = j(\dot{x})dt = j(\dot{x})xd = -\Psi(\dot{x})dt. \quad (4.341)
```

If the system has a limit cycle, the energy returns to the same value after a period and the integral of the dissipation function must be:

```
0 = \int dE = \int (dE/dt)dt = -\Psi(\dot{x})dt. \quad (4.342)
```

Thus two cases are possible: (i) if there is dissipation (amplification) at least some of the time $\Psi>0$, $\Psi<0$, then (4.342) cannot be met, and a limit cycle cannot exist, that is, is **breaking (growth)** of the system to rise (away from rest); (ii) a limit cycle is possible if dissipation $\Psi>0$ and amplification $\Psi<0$ balance over a period (4.342). An example is a *self-excited oscillator*: (i) damping dominates for large velocity, so the path is bounded; (ii) amplification dominates for small velocity so it cannot come to rest. As an example with both first and second-order cases is the homopolar disk dynamo considered next (subsection 4.7.2).

## 4.7.2 Homopolar Disk Dynamo Under Uniform Rotation

The electric current J a homopolar dynamo corresponds (4.343a) to an electrical circuit with total induction L and resistance R:

```
LJ + RJ = F_c, \quad F_c = \pm\frac{\Phi_m\Omega}{2\pi}, \quad \Phi_m = Z_j, \quad (4.343a-c)
```

where the electromagnetic force is due to the magnetic flux $\Phi_m$ through the rim of the disk (4.343b) and $\Omega$ is the angular velocity; the magnetic force (4.343c) equals the current J through the mutual induction $Z$. The upper+(lower -) sign in (4.343b) corresponds to corotation (counterrotation); that is, the external wire carrying the same (opposite) direction as that of the rotation. Substituting (Figure 4.16) (4.343c) in (4.343b) specifies the electromotive force (4.344b) driving the current (4.343a)=(4.344a):

```
LJ + RJ = F_e = \pm\frac{Z\Omega}{2\pi}J; \quad J_j(t) = J_j(0)\exp\left[-R \pm\frac{Z\Omega}{2\pi}L]t\right]; \quad (4.344a, b)
```

the integral (4.344b) of (4.344a) shows that an homopolar electric disk dynamo for (problem 122) counterrotation, that is the + sign below in (4.344b) acts as a *brake* in (4.345a) since the mutual inductance and angular velocity act (4.345c)

## Unsteady, Non-Linear, and Chaotic Systems

![](img/6a4cb3b3bd1429197bb791c4b642651c_211_0.png)

**Figure 4.16**
A homopolar disk dynamo with electric current in the direction opposite $J_{-}$ to that of rotation acts (i) as a brake. If the current $J_{+}$ is in the direction of rotation, the angular velocity (ii) constant for a critical resistance; higher (lower) resistance leads to (iii) a reduced braking relative to (i) [an exponential increase in current with time (iv] without bound in the absence of rotational inertia and driving torque (see Figure 4.17)].to increase the effective resistance (4.345b), causing a faster exponential decay of the current:

$J_{-}(t) = J_{+}(0)\exp\left(-\frac{\tilde{R}}{L}t\right): \quad \tilde{R} = R+\frac{Z\Omega}{2\pi}, \quad R = \frac{Z\Omega}{2\pi} \quad (4.345a, b)

In the case (problem 123) of rotation; that is, the – sign above in (4.344b), the mutual induction and rotation oppose the resistance leading to three cases:

```
$\exp[-R-\tilde{R}t]=0 \quad \text{if} R>\tilde{R}, \quad (4.346a)$
$\lim_{t\to\infty}J_{-}(t)=J_{+}(0) \quad \text{if} R=R, \quad (4.346b)$
$\exp[-R-\tilde{R}t]=\infty \quad \text{if} R<\tilde{R}, \quad (4.346c)$
```

(i) for the critical resistance $R$ constant current; (ii) for larger resistance $R$ (iii) for smaller resistance (4.346c) the current grows with time. The preceding results assume that the angular velocity is kept constant by providing driving torque; the torque is related to the angular acceleration through the moment of inertia. Thus the preceding **electrical dynamo** (subsection 4.7.2) for consistency be complemented by mechanical effects of rotational inertia in the **electromechanical dynamo** (subsection 4.7.3).

## 4.7.3 Effects of Rotational Inertia in the Electromechanical Dynamo

The product of the angular acceleration $\dot{\Omega}$ around the axis by the moment of inertia I relative to the axis is the inertia torque (4.347a):

$I \dot{\Omega} = M = \pm (Z / 2\pi) \Omega J, \quad (4.347a–d)$ balanced by the driving torque (4.347b), equal to the product (4.347c) of the electromotive force (4.344a) by the moment arm $a$; 

The result (4.347d) can be interpreted in terms of Lorentz force (subsection 8.3.2 and note 8.10) that is proportional to the velocity and magnetic field; these are proportional respectively to the angular velocity $\Omega$ and magnetic flux (4.343c) current J. Thus the torque should scale on the product of the electric current by the angular velocity (4.347d) like the electromotive force (4.344a), and they are in a constant ratio $a$ in (4.348b) corresponding to the moment arm a. If the resistive term in (4.344a) is small compared with that due to mutual induction (4.348a), the current equation simplifies to (4.346b):

$2\pi R << Z\Omega: J = F/L = M/L = I/(L) \dot{\Omega}; \quad J/\Omega = I/L. (4.348a–e)$

The current equation (4.348b) is similar (4.348c) to the equation (4.347c) for the angular velocity, showing (4.348d) that it is in a constant ratio to the angular velocity (4.348e) if they are both zero at some initial time. Substitution (4.348e) in (4.344a) leads to the differential equation for the electric current (4.349c):

$S \equiv Z\Omega / (2\pi J) = ZL / (2\pi I): L \dot{J} = -RJ \pm SJ^2, \quad (4.349a–c)$

that involves the constant dynamo parameter (4.349a, b). Thus, the electromechanical homopolar dynamo (Figure 4.16) in the case of small resistance compared with the mutual induction (4.348a), has electric current and angular velocity in a constant ratio (4.348e) and satisfies the same non-linear equation (4.349c) with coefficient (4.349a) $\equiv (4.349b)$. The equation (4.349c) is solved next (subsection 4.7.4).

## 4.7.4 Case of Small Resistance Compared with the Induction

The non-linear differential equation of the first order (4.349c) is separable (4.350a) and can be integrated (4.350b) from the initial current $J_{\pm0}$ at time $t=0$ to the current $J_{\pm}$ at time $t$:

$-R/Lt = \int_{J_0}^{J_{\pm}} \frac{dJ}{J \pm SJ^2/R} = \int_{J_0}^{J_{\pm}} \left(\frac{1}{J} \pm \frac{1}{R/S \mp J}\right) dJ = \left[\log\left(\frac{J}{R/S \mp J}\right)\right]_{J_0}^{J_{\pm}}, (4.350a, b)$

using the partial fraction decomposition (section I.31.8; subsection 1.5.3) to obtain (4.350b) $\equiv (4.351a, b)$:

```
J_0 \equiv J_{\pm}(0):
        exp(-R/Lt) = (J_{\pm}/J_0) (R \mp J_0 S)/(R \mp J_{\pm} S). \quad (4.351a, b)
```

The equation (4.351b) specifies the electric current and angular velocity (4.348e) as a function of time:

```
I/(aL) \Omega_{\pm}(t) = J_{\pm}(0) \exp[-Rt/L] \mp J_0 S t/L]. \quad (4.352a, b)
```

If it can be checked that (4.352b) satisfies the initial condition (4.351a) at time $t=0$; the current and angular velocity also vanish (4.352b) as $t \to \infty$ showing that the retarding torque due to the Lorentz force will stop the motion unless there is a driving torque. In the preceding solution the approximation of small resistance (4.348a) was made. If the approximation had also been made in (4.349b) it would become:

```
L \dot{J} = \pm SJ^2; \pm S/Lt = \int_{J_0}^{J_{\pm}} \frac{dJ}{J^2} = 1/J_0 - 1/J_{\pm}, I/(aL) \Omega_{\pm}(t) = J_0 / [1 \mp J_0 S t/L]. \quad (4.353a–c)
```

the solution (4.353b) also confirms that $J_0$ is the initial value and that $J \to 0$ algebraically (4.353c) instead of exponentially (4.352b). Thus, the electromechanical homopolar dynamo (Figure 4.16) with small resistance compared with the mutual induction (4.348a) has electric current and angular velocity (4.348e) both decaying to zero due to the braking torque associated with the Lorentz force. The decay is exponential (4.342a, b) [algebraic (4.353a, b)] if [problem 124 (125)] the approximation (4.348a) is not made in the differential equation (4.349c) [(4.353a)]. The case when the approximation (4.348a) is not used at all, and there is no restriction of the ratio of the resistance to the mutual induction, is considered next (subsection 4.7.5).

## 4.7.5 Electromechanical Dynamo in the Phase Plane

It is possible to eliminate between the electrical (4.344a) and mechanical (4.347d) relations without making the approximation (4.348a) or any other; that is, the exact solution of the electromechanical dynamo problem satisfies:

```
d/dt (1/J dJ/dt) = d/dt (− R/L \pm ZΩ/(2πL)) = ± Z/(2πL) dΩ/dt
        = ± Z/(2πL) (± aZ/(2πL) ΩJ) = ± aZ/(2πL) (L dJ/dt + R J).      (4.354)
```
