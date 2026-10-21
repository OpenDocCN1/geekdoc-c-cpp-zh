
![](img/c92a9d81ba7f671c83a4c600d27389fb_62_0.png)

FIGURE 3. Evolution of a KdV ring by NV at positive energy

![](img/c92a9d81ba7f671c83a4c600d27389fb_62_1.png)

FIGURE 4. L₂ norm of the NV solution at positive energy

written in terms of the hyperbolic tangent function. Moreover, the hyperbolic tangent function is a solution to the Riccati equation, φ' = l₀ + φ², for l₀ < 0 for certain initial conditions. The ubiquity of the hyperbolic functions as traveling wave solutions naturally leads to the idea of expansion methods for solving soliton equations.

Solutions in the literature to the NV equation include the solutions from the inverse scattering transform [44–46, 64], the classic hyperbolic secant and cnoidal solutions [60], and rational solutions derived using Darboux transformations that lead to finite time blow-up (see [88] and references therein). In this section we present new solutions to the NV equation using Hirota's bilinear method and the Extended Mapping Approach (EMA). New multiple traveling wave solutions using the Modified Extended Tanh-Function Method can be found in [14]. This approach results in closed-form solutions, most of which contain singularities. We note that the solutions found by Hirota's method are plane-wave solutions, that is, KdV-type solutions, while the EMA-derived solutions are not.

## 4.2.1. Hirota's Method.

Following the pioneering work of Hirota [31], multisoliton solutions can be derived using Hirota's bilinear method. This method yields multisoliton solutions as a sum of polynomials of exponentials and was used in [94] to find multisoliton solutions to the Nizhnik-Novikov-Veselov equation

```
q̇ = −a qₓₓₓ + b qᵧᵧᵧ − 3a(q u₁)ₓ − 3b(q u₂)ᵧ
qₓ = (u₁)ᵧ
qᵧ = (u₂)ₓ
```

The main idea is to reduce the nonlinear equation to a bilinear form through a transformation involving the logarithmic function. To express the wave velocity c in terms of the dispersive coefficients, assume u is a plane wave solution with k₁ = k₂ = k, u = e^{k x + k y − c t}, and substitute u into (2.1). This results in c = −k³/2. Under the transformations q = R(ln(f))ₓₓ, v = R(ln(f))ₓᵧ, and w = R(ln(f))ᵧᵧ where f(x, y, t) = 1 + C e^{k x + k y + k³/2 t} and C is an arbitrary constant, one can algebraically solve for R to find a bilinear form (one finds R = 2). This method results in the soliton solution

```
(4.5) q(x, y, t) = u₁(x, y, t) = u₂(x, y, t) = \frac{2 C k² e^{k (2 x + 2 y + k² t)/2}}{\left(1 + e^{k (2 x + 2 y + k² t)/2}\right)²}.
```

Choosing

```
f(x, y, t) = 1 + e^{θ₁} + e^{θ₂} + a₁₂ e^{θ₁ + θ₂},
```

where θᵢ = kᵢ x + kᵢ y + ½ kᵢ³ t, i = 1, 2, in the logarithmic transformations above results in the two-soliton solution with a₁₂ given in terms of k₁ and k₂ by a₁₂ = (k₁ − k₂)²/(k₁ + k₂)²

```
q(x, y, t) = \frac{2\left(k₁² e^{θ₁} + k₂² e^{θ₂} + (k₁ − k₂)² e^{θ₁ + θ₂}\right)}{1 + e^{θ₁} + e^{θ₂} + \frac{(k₁ − k₂)²}{(k₁ + k₂)²} e^{θ₁ + θ₂}} − \frac{2\left(k₁ e^{θ₁} + k₂ e^{θ₂} + \frac{(k₁ − k₂)²}{k₁ + k₂} e^{θ₁ + θ₂}\right)²}{\left(1 + e^{θ₁} + e^{θ₂} + \frac{(k₁ − k₂)²}{(k₁ + k₂)²} e^{θ₁ + θ₂}\right)²}. (4.6)
```

The evolution of the two-soliton solution is plotted in Figure 5. Further details and a three-soliton solution are found in [14].

![](img/c92a9d81ba7f671c83a4c600d27389fb_64_0.png)

FIGURE 5. Time snapshots of the evolution of a 2-soliton solution derived Hirota’s bilinear method.

## 4.2.2. Extended Mapping Approach.

The extended mapping approach (EMA) was presented formally by Zheng [97] and extends results by Lou and Ni [47]. The method is designed to find mappings between nonlinear PDE’s. In this approach, q, v, w are expanded in terms of a function φi that satisfies the Riccati equation

\frac{d\phi}{dR} = \ell_0 + \phi^2,

where R = R(x, y, t). Thus, q(x, y, t) = \sum_{i=0}^n a_i \phi^i, v(x, y, t) = \sum_{i=0}^m b_i \phi^i, and w(x, y, t) = \sum_{i=0}^k c_i \phi^i, where the values of n, m and k are determined by balancing the highest order derivative terms with the nonlinear terms of the PDE. The method is described nicely in [78]. The balancing method results in n = m = k = 2. Substituting these expansions into the NV equation and equating coefficients of the resulting polynomial in φ results in a system of thirteen PDE’s from which

we need to solve for the coefficients $a_i(x,y,t)$, $b_i(x,y,t)$, and $c_i(x,y,t)$, $i = 1,2$. Using a separation technique for $R$, namely, $R(x,y,t) = p(x,t) + q(y,t)$ results in $sech^2$ solutions, static (time-independent) solutions, and breather-type solutions of the NV equation. Further details, including the choices of $\phi$ are found in [14]. A time-independent solution is given by

$q(x,y,t) = \frac{-1728 y^6 + (-96 + 1728 C) y^4 + (-40 + 288 C) y^2 - 36 C + 5}{432 y^4 - 36 y^2} - 4 \tanh(x + y^2) + (2 + 8 y) \tanh^2(x + y^2)$

$v(x,y,t) = \frac{144 y^4 + (-12 + 432 C) y^2 - 36 C + 5}{36 y^2} + 4 \tanh(x + y^2) + (2 - 8 y) \tanh^2(x + y^2)$

$w(x,y,t) = 8 y - 8 y \tanh^2(x + y^2)$

where $C$ is an arbitrary constant. See Figure 6 for a plot of the solution $q$ with $C = 1.$

![](img/c92a9d81ba7f671c83a4c600d27389fb_65_0.png)

FIGURE 6. A static solution to the NV equation

Breather solutions are solutions with a type of periodic back-and-forth motion in time. One particular breather solution from [14] is

```
q(x, y, t) = [-1728 y^6 + (-96 + 1728 C) y^4 + (-40 + 288 C) y^2 - 36 C + 5] / [432 y^4 - 36 y^2] - 4 tanh(1 + x + y^2 + 4 cos t) + (2 + 8 y^2) tanh^2(1 + x + y^2 + 4 cos t)
```

```
v(x, y, t) = [-192 sin(t) y^2 + 144 y^4 + (-12 + 432 C) y^2 - 36 C + 5] / [36 y^2] + 4 tanh(1 + x + y^2 + 4 cos t) + (2 - 8 y^2) tanh^2(1 + x + y^2 + 4 cos t)
```

```
w(x, y, t) = 8 y - 8 y tanh^2(1 + x + y^2 + 4 cos t).
```

Several time snapshots are shown in Figure (7). For multisoliton solutions the reader is referred to [14].

For multisoliton solutions the reader is referred to [14]

## 4.3. Scattering transform of the ring soliton at time zero.

In this section we compute numerically the scattering transform of the KdV ring soliton discussed in example 4.3 and illustrated in Figure 2. Since the initial potential is supercritical, we expect the scattering transform to have a singularity. Since the initial potential is real-valued and rotationally symmetric in the z-plane, also the scattering transform is real-valued and rotationally symmetric in the k-plane. See [56, Appendix A] for a proof. Therefore it is enough to compute t(k) only for real and positive k.

We use both the LS and the DN methods described in Section 3.2 and compare the results to verify accuracy. The values in the range 0.1 ≤ |k| ≤ 4 are reliable as the results of both NV and LS methods closely agree there. However, the DN method does not give reliable results for |k| > 4.

To assure accuracy for |k| > 4, we compare the results of the LS method with two different grids in the z-domain. The coarser grid has 4096 × 4096 points, and the finer grid has 8192 × 8192 points. The coarser grid is not a subset of the finer grid. We remark that both of these grids are significantly finer than those we typically use for computing scattering transforms for conductivity-type potentials. Due to high memory requirements, we used a liquid-cooled HP Z800 Workstation with 192 GB of memory. Even with that powerful machine, the evaluation of one point value using the finer grid takes more than 11 hours. The LS method gives closely matching results in the regions 3 ≤ |k| ≤ 5 and |k| > 9.

Figure 8 shows the profile of the scattering transform. In the interval 5 < |k| < 9 the numerical computation does not converge, resulting either in inaccurate evaluation of the point values of the scattering transform or in complete failure of the algorithm due to using up all the memory. We suspect that the observed numerical divergence arises from the existence of at least one exceptional circle in the interval 5 < |k| < 9.

## THE NOVIKOV-VESELOV EQUATION

![](img/c92a9d81ba7f671c83a4c600d27389fb_67_0.png)

FIGURE 7. Time snapshots of a breather solution derived using the EMA.

## 5. Zero-energy exceptional points

The inverse scattering method for the solution of the Novikov-Veselov equation is based on the complex geometrical optics (CGO) solutions ψ of the Schrödinger equation (2.8). The function ψ(z,k) is asymptotically close to the exponential function e^{ikz} in the sense of formula (2.9); the point is that ψ can be used to define a nonlinear Fourier transform t(k) specially designed for linearizing the NV equation. See diagram (1.5) above.

However, there is a possible difficulty in using ψ and t. Even in the case of a smooth and compactly supported potential q ∈ C₀^∞, there may exist complex numbers k ≠ 0 for which equation (2.8) does not have a unique solution satisfying the asymptotic condition (2.9). Such k are called exceptional points of q. It is shown in [56] that exceptional points of q come in circles centered at the origin and that the scattering transform has a strong
