
# Unsteady, Non-Linear, and Chaotic Systems

# 227

![](img/6a4cb3b3bd1429197bb791c4b642651c_249_0.png)

**FIGURE 4.27** The anharmonic oscillator with cubic term in the potential (a) has stable (unstable) equilibrium positions (b) corresponding to positive (negative) curvature of the potential (c) and symmetric cusp of the potential at the equilibrium positions (d). (Figure 4.26) and cubic potential (Figure 4.27) relate to the fold or cusp catastrophe

For one parameter $a$, a plane representation is adequate. In the case of the cusp catastrophe (subsection 4.8.9) that involves two parameters, a representation in a three-dimensional space is more illuminating than its plane projections.

## 8.8.9 Two-Parameter Quartic Potential and Cusp Catastrophe

The cusp catastrophe corresponds to (problem 143) to a quartic potential (4.46a1):

```
$$\Phi(x;a,b)=-\frac{x^4}{4}+\frac{ax^2}{2}-bx; \quad x^3-ax+b=-\frac{d\Phi}{dx}=f(x;a,b)=\dot{x}, \quad (4.46a1,b)$$
```

with two parameters that both appear in the force (4.461b). Thus two parameters can be reduced to one by the re-scaling (4.462a):

```
$x,a,b,\Phi,f=\{\tilde{x},\tilde{\lambda},\tilde{a}^2,\tilde{a}^3,\tilde{b},\tilde{\lambda}^3,\tilde{f}\}$

$$\$$\Phi = -\frac{\tilde{x}^4}{4}+\frac{\tilde{a}\tilde{x}^2}{2}-b\tilde{x},\quad (4.462a,b)$$

$$-\tilde{x}^3+\tilde{a}\tilde{x}^2+\tilde{b}=\frac{d\tilde{\Phi}}{d\tilde{x}}=\tilde{f},\quad 0=-\tilde{x}^3+\tilde{a}\tilde{x}+\tilde{b},\quad (4.462c,d)$$
```

applied to the potential (4.462b), force (4.462c), and equilibrium positions (4.462d). Differentiating (4.462d) with regard to $b$ (tildes suppressed) leads to (4.463a):

```
$1=(3\tilde{x}^2-a)\frac{d\tilde{x}}{d\tilde{b}},\quad \lim_{\tilde{b}\to0}\tilde{x}=\pm\sqrt{a},\quad \frac{dx}{db}=\frac{1}{2a},\quad (4.463a-c)$
```

also (4.462d) implies (4.463c). Thus (Figure 4.28b) $\tilde{x}$ as a function of $b$ on the original vertical slope for $a=0$, positive slope for $a>0$ and negative slope for $a<0$. Thus that for a given $b$: (i) there is only one equilibrium point $\tilde{x}$ if $a<0$; and (ii) if $a>0$ there is a $b_1 < b < b_2$, of values with $b$ with a triple root for $\tilde{x}$.

The problems (4.13) of the equilibrium points $\tilde{x}$ as a function of $b$ or $\tilde{a}=$cost of the force (4.461b) corresponding to the quartic potential (4.461a) using coordinates $(x,a,b)$; this involves stretching from (4.462a) to $(x,\tilde{a},\tilde{b})$, which has different scales along the axis, but does not modify the topology. The equilibrium points, where the force vanishes, lie on the fold lines of the cusp catastrophe manifold (Figure 4.28b) and are projected on the parameter plane (Figure 4.28c) as a cusp, where the stable and unstable regions; each leading line from the cusp is a *directrix*. The name cusp catastrophe; the cross-sections $a=c$ show a hysteresis loop (Figures 4.26 and 4.10d) emerging a double fold from an unfolded surface as $a<0$ crosses the bifurcation point $a=0$ into $a>0$. The discontinuous lines on the parameter plane (Figure 4.28) are two-dimensional projections of a smooth surface in three dimensions. The three-dimensional representation (Figure 4.28b) is more illuminating than its projections (Figures 4.28a,c). Another method of investigation of this plane is using Poincaré maps (Section 4.80).

## 4.8.10 Iterated Maps and Classification of Singularities

Consider a dynamical system with isolated singularities; that is, there is a neighborhood of each singularity that does not contain other singularities. A line through a singularity, a straight line that the *directrix*, is not tangent to any

![](img/6a4cb3b3bd1429197bb791c4b642651c_251_0.png)
![](img/6a4cb3b3bd1429197bb791c4b642651c_251_1.png)
![](img/6a4cb3b3bd1429197bb791c4b642651c_251_2.png)

**FIGURE 4.28** The potential of an anharmonic oscillator with a cubic term (Figure 4.28a) leads to the equilibrium positions $\tilde{x}$ as function of the coefficient $b$ of the linear terms that (a) has three values when the coefficient $a$ of the cubic term increases. Choosing $a$ as a third coordinate orthogonal to the $(a,b)$ plane leads to a fold in the surface (b), like the hysteresis loops in Figures 4.10d, 4.24c, and 4.26. The projection on the plane $(a,b)$ of the coefficients of the potential (c) leads to a cusp at the function of the stable and unstable branches of equilibrium positions as Figure 4.27d. The point(s) where the integral curves intersect the directrix (problem 144) are ordered according to their distance from the singularity (4.46a), and their sequence forms an iterated or return map (4.46b):

$x_1 < x_2 < ... < x_{n-1} < x_n < x_{n+1} < ... \quad x_{n+1} = f(x_n). (4.464a,b)$

Five cases arise (Figure 29b): (i) if every directrix is cut at the same point (4.46a) the path is a limit cycle; (ii) if every directrix the iterated map (4.464b) tends to a fixed point (4.465b) then the path tends to a limit cycle; (iii) if every directrix (at least one directrix) the map tends to the singularity (infinity) the singularity is stable (4.465c) [unstable 4.465d]; (iv) if the iterated map covers densely the interval (4.465e) and never comes through the same point the motion is chaotic (Figure 29c):

$$\begin{aligned} n=1,2,...infty \Rightarrow x_n = x_0: & \text{limit cycle}, & (4.465a) \\ \lim_{n\to\infty} x_n = x_0: & \text{tends to limit cycle}, & (4.465b) \\ \lim_{n\to\infty} x_n = 0: & \text{stable}, & (4.465c) \\ \lim_{n\to\infty} x_n = \infty: & \text{unstable}, & (4.465d) \\ x_- < x_n < x_+: & \text{chaotic.}, & (4.465e) \end{aligned}$$

Poincaré map: a small change in the initial conditions can lead to a large change in the path over a finite time.

## 4.8.11 Comparison of Deterministic and Chaotic Systems (Ruelle & Takens 1971)

The apparently random motion of a fluid known as turbulence may be interpreted as a chaotic motion. The transition of a flow from laminar to turbulent then corresponds to the passage (problem 145) from a deterministic to a chaotic system. An infinite sequence of bifurcations could lead to chaos (Landau 1953). A more economical scenario (Ruelle-Takens 1971) observes three bifurcations: (i) from a periodic orbit with one frequency $\omega$, to a quasi-periodic orbit with frequencies $(\omega_1, \omega_2)$; (ii) another quasi-periodic orbit $(\omega_1, \omega_2, \omega_3)$ which can be perturbed into (iii) a chaotic motion. In the case of Hopf bifurcations it can be (i) all visible (Figure 4.30a), (ii) two visible (Figure 4.30b), or (iii) only visible (Figure 4.30c). Besides a sequence of bifurcations, other properties of non-linear systems can contribute to

![](img/6a4cb3b3bd1429197bb791c4b642651c_253_0.png)

**FIGURE 4.29** The Poincare map is the ordered set (b) of the points of intersection with the integral curves of a directrix, that is a straight line passing through an isolated singularity, at the origin of the phase plane. Four cases can arise: if the map stabilizes at a fixed point $x_s = x_0$ or $n \to \infty$ to a fixed point there is a limit cycle around a center (Figure 4.1g); (ii)/(iii) if the map tends to the origin $x_s \to 0$ (infinity, $x_s \to \infty$) the system is unstable (stable), or for example an inward (Figure 4.1f) [outward] spiral; or (iv) if the map $x_< < x_s$, in the sense it converges arbitrarily to any point in a finite time, the system is chaotic. The case (v) implies that a small change in initial conditions can lead to a large change in position in a finite time.

