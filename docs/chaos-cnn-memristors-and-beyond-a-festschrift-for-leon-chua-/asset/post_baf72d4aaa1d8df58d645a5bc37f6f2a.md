
## 2.1. Equilibrium points and frequency response curves

By putting the right-hand side of Eq. (11) to zero, equilibrium point of the Eq. (11) can be found, as

```
a₀ = - r₀² / F ( ω² - (n g / ℓ) r₀^{n-2} ),
 b₀ = - r₀² / F k ω
```

and the vertical component c₀

```
c₀ = √(a₀² + b₀²)ⁿ
```

where r₀² in Eq. (13) is determined from the following relation:

```
[ k² ω² + ( ω² - (n g / ℓ) r₀^{n-2} )² ] r₀² = F²
```

It is noted that Eq. (15) represents frequency response (or resonance) characteristics of the steady-state amplitude (or radius) r₀ of a horizontal circular motion, and c₀ is the height of the circular periodic motion with equi-angular velocity.

## 2.2. Stability condition for equilibrium points

We shall determine stability conditions for the equilibrium point represented by Eq. (13). Let (ξ, η) be a small variation from the equilibrium point (a₀, b₀) and then discuss whether the variation approaches zero or not as the time t increases. The following variational equation is obtained by applying common manipulations:

```
dξ/dτ = (∂f/∂a)₀ ξ + (∂f/∂b)₀ η
 dη/dτ = (∂g/∂a)₀ ξ + (∂g/∂b)₀ η
```

where left (, right)₀ stands for a partial derivative, such as ∂f/∂a, at the equilibrium point a = a₀? b = b₀.

An application of the well-known Routh-Hurwitz criterion gives the following stability condition:

```
p = - (∂f/∂a)₀ - (∂g/∂b)₀ = k/ω > 0
 q = (∂f/∂a)₀ (∂g/∂b)₀ - (∂f/∂b)₀ (∂g/∂a)₀ = 1/(4 ω⁴)[ ω⁴ + (k² - g/ℓ n² r₀^{n-2}) ω² + g²/ℓ² n² (n-1) r₀^{2n-4} ] > 0
```

The first relation of the condition (17) answers correctly the Bendixson (Negative) Theorem for its conclusion with a positive value of k. The second relation gives vertical tangency of the frequency response (resonance) characteristics represented by Eq. (15).

## 3. Horizontal Circular Motion with Equi-angular Velocity

In the preceding section, circular motion representing steady states is obtained as

```
x₀(t) = a₀ cos ωt - b₀ sin ωt
 y₀(t) = b₀ cos ωt + a₀ sin ωt
 z₀(t) = c₀
```

By inspection it is easy to see that this steady-state solution (18) is an exact solution of Eq. (3), but non-stationary representative point of Eq. (11) shows approximate solutions which express the transient states.

The solutions represented by Eq. (18) is rewritten in terms of the amplitude r₀ and the phase φ₀ as follows:

```
x₀(t) = r₀ cos(ωt - φ₀)
 y₀(t) = r₀ sin(ωt - φ₀)
 r₀² = a₀² + b₀²
 φ₀ = arctan( -b₀ / a₀ )
```

## 4. Frequency Response Curves and Phase Portraits

Here, how curvature of nonlinearity determines outcomes is shown by numerical examples with n = 2. The following parameter values are used:

```
g/ℓ = 100,   k = 0.1,   F = 5
```

## 5. Discussions about the Jumping Mechanism

Interpretation of the above observed jumping phenomena is attempted from a physical standpoint. For that purpose, Eq. (11) is rewritten in the following form:

```
d(a² + b²)/dτ = 1/ω² (-kωr² - bF) = N(a,b)

d/dτ (-b/a) = 1/(2ω²a²) (g/ℓ nrⁿ - ω²r² - Fa) = T(a,b)  (21)
```

where

```
r² = a² + b²  (22)
```

The first equation of Eq. (21) determines the derivative of the normal component (radius direction) of the motion of the representative point, and the second equation of Eq. (21) tangential component to the circular trajectory of the motion (see the fourth equation of Eq. (19)).

### 5.1. Decomposition of operating force

When the system is in the steady state, the mass point continuing the horizontal circular motion represented by Eq. (18) or Eq. (19) is supplied with power from the rotating external force. In order to explain the situation, the force operating on the mass point is decomposed into tangential component F sin φ₀ and radial component F cos φ₀. Let us call the former Fₐ = F sin φ₀ active component and the latter Fᵣ = F cos φ₀ reactive component. Both components are on the horizontal plane.

### 5.2. Jumping-up phenomena

Jumping-up phenomenon in Fig. 3 occurs when the angular velocity ω is increased, while in Fig. 4 decreased. These phenomena occur under the mechanism that the saddle point D approaches a non-resonant point N (point N moves a little almost horizontally), and these coalesce into a node-saddle,

Fig. 3. Frequency response characteristics for the 3/2 order constrained surface.

Fig. 4. Frequency response characteristics for the 5/2 order constrained surface.

![](img/039e7d3c23390584a66737067db8b75b_458_0.png)

Fig. 5. Phase portrait for Eq. (11) with n = 3/2, F = 5, ω = 15.

![](img/039e7d3c23390584a66737067db8b75b_458_1.png)

Fig. 6. Phase portrait for Eq. (11) with n = 5/2, F = 5, ω = 15.

a higher-order equilibrium point, and then disappears. The amplitude characteristic (r0, ω) and the phase characteristic (φ0, ω) together demonstrate these states clearly. The well-known fold bifurcation occurs. By inspecting the movement of the representative point of Eq. (11), from (disappeared) ND point, representative point takes off to the right (almost on and along the a-axis) in the case of Fig. 3, while to the left in the case of Fig. 4. Moreover, phase changes from 0 to π and from π to 0. Note that the direction φ0 is taken as clockwise here.

The above implies that the failure (N(a, b) becomes positive) of the first equation of Eq. (21) predominates over the second equation of Eq. (21). This fact implies that the power supplied by the active component to the mass overflows the power consumed by dissipation. In other words, jumping-up phenomena occur via the loss of power balance between supply and consumption.

### 5.3. Jumping-down phenomena

Jumping-down phenomenon in Fig. 3 occur when the angular velocity ω is decreased, while in Fig. 4 increased. These phenomena occur under the mechanism that the saddle point D and the stable equilibrium point R approach each other by moving downward, and they coalesce into a node-saddle, a higher-order equilibrium point, almost on the b-axis, and then disappears. The well-known fold bifurcation occurs. By inspecting the movement of the representative point of Eq. (11), from

(disappeared) RD point, representative point takes off to the right (almost horizontally) in the case of Fig. 3, while to the left in the case of Fig. 4. Moreover, phase changes from π/2 to 0 and from π/2 to π.

The above implies that the failure (T(a, b) becomes non-zero) of the second equation of Eq. (21) predominates over the first equation of Eq. (21). This fact implies that the supplied reactive force to the mass loses the balance with the sum of the centrifugal force and the radial component of the constrained force. In other words, jumping-down phenomena occur via the loss of force balance among reactive, centrifugal and (horizontal component of) constrained forces.

## 6. Problems Descendent from This Study

Experimental simulation studies on Eq. (11) revealed preceding facts. Though not mentioned there, many complicated motions are observed in systems described by Eq. (3) when the amplitude F takes large values, some of which seems to be chaotic motions. These are left as open problems.

Simulation study for the case of a conic constrained surface of revolution (n = 1) showed peculiar behavior. In this case, bottom (origin of the (x, y, z)-space) becomes singular or a capture point, and interesting intermittently bursting motions are observed. No further investigation has been done, however. Several motions that caught our attention may be hidden behind the system.

Introduction of asymmetry into constrained surfaces and/or periodically rotating force will bring unexpected motions, however these are left as further open problems.

## 7. Conclusion

The qualitative and quantitative behaviors of a mass point in a rotating external force and constrained on a surface of revolution upward has been studied. The basic behavior of this system is periodic motion. Jump phenomena in the amplitude of the periodic circular motion under variation of the angular velocity of the external force almost-stationarily have been observed, and qualitative difference of the jump phenomena on the curvature of the surface of revolution is disclosed, which is separated by a parabolic surface of revolution given by \(n=2\). Moreover, mechanisms of jumping-up and -down phenomena are also clarified by the loss of power balance and reactive force balance, respectively.

## Acknowledgments

In the preparation of this dedicatory study in honor of Professor Leon O. Chua, the author was greatly supported by Professor Shin’ichi Oishi, Dean of the Graduate School of Fundamental Science and Engineering, Waseda University, who provided him splendid research environment. He was also aided by his graduated students Mr. Kenta Hosoi and Mr. Takuma Kawamura of the Future University—Hakodate, Dr. Hirofumi Ohta of the Kyoto University and Professor Ralph Abraham of the University of California Santa Cruz, who gave him valuable suggestions and good advice of all kinds. Acknowledgment must also be made to Professor Guanrong (Ron) Chen of the City University of Hong Kong, and Professor Andrew Adamatzky of the University of the West of England at Bristol, for their excellent cooperation with great patience.

As to the references of this study, there are too many good textbooks on Classical Physics and Nonlinear Dynamics or Oscillations. It seems very difficult for the author to refer to a long list of textbooks among many. The author especially appreciates many great precursors in the fields.
