
![](img/1f293b0ceb2de964310ea7f941a1b580_559_0.png)

coordinates. Thus, the mapping from the square reference element in Figure 22.2 to these nonlinear finite elements can be used to assemble the stiffness matrix. Here, however, the situation is not as straightforward as in Chapter 12, Section 5: because the mapping is no longer constant. Therefore, numerical integration may be necessary in some cases.

In this approach, the circular boundary on the right is approximated better than before. As discussed above, the circular shape is essential for the correct modeling of the physical phenomenon. Therefore, the nonlinear finite-element mesh may be more accurate and adequate. (Of course, a suitable nonlinear finite-element mesh must use a meshsize much smaller than in Figure 22.6 to guarantee adequacy. This can be achieved by adding more internal half-circles and radial lines in the mesh.)

In the rest of this chapter, we show that the Helmholtz equation can also be derived from the Maxwell equations that govern the connection between electric and magnetic fields.

The phenomenon of electromagnetic waves is described using the Maxwell equations. which govern the connection between electric and magnetic fields. In this system, the unknowns are the electric vector field E and the magnetic vector field B. These vector functions depend on the three spatial variables x, y, and z, as well as the time variable t. The given data in the right-hand side of the system are the scalar function ρ(t,x,y,z) representing the density of electric charges and the vector function J(t,x,y,z) representing the vector current density (the amount of current that flows through a unit area in unit time in the direction perpendicular to that area.)

We use here the cgs system of units (centimeters, grams, seconds). In this system, the constant c that represents the speed of light is 3 × 10^{10} cm/s.

Note that the Nabla operator used below contains only the spatial derivatives as in Chapter 21, Section 1, whereas the time derivative is represented by a subscript t.

The Maxwell equations give the unknown electric and magnetic fields in terms of the given data about the charge and current densities:

## 22.11. The Maxwell Equations

```
∇ · E(t,x,y,z) = 4π ρ(t,x,y,z),
∇ × E(t,x,y,z) = -1/c B(t,x,y,z)_t,
∇ · B(t,x,y,z) = 0,
∇ × B(t,x,y,z) = 4π/c J(t,x,y,z) + 1/c E(t,x,y,z)_t .
```

The drawback in this setting is that it contains more equations than unknowns. Indeed, it has two vector unknowns, E and B, which can be viewed as six scalar unknowns. The number of equations, however, is greater than six: there are two vector equations (the second and fourth) and two scalar equations (the first and third), which amount to eight scalar equations. In what follows, we reduce the system to an equivalent system in which the number of equations is the same as the number of unknowns.

Let us use the facts mentioned at the end of Chapter 21, Section 1, to introduce scalar and vector potential functions for the electric and magnetic fields. From the third equation in the Maxwell system, we have that the magnetic field B has zero divergence at every given time and every spatial point. Therefore, there exists a vector potential function V(t,x,y,z) such that B = ∇ × V at every fixed time t and every spatial point.

```
B = ∇ × V
```

```
∇ × (E + 1/c V_t) = 0.
```

Thus, at every given time, the vector field E + V_t/c is conservative, and, hence, has a scalar potential function Φ(t,x,y,z) for which E + 1/c V_t = -∇Φ at every fixed time t and every spatial point.

```
-ΔΦ - 1/c ∇·V_t = 4πρ(t,x,y,z).
```

Let us now take the time derivative of the previous equation: E_t + 1/c V_tt = -∇Φ_t .

```
E_t + 1/c V_tt = -∇Φ_t .
```

By substituting this result in the fourth equation in the Maxwell system, we have ∇ × ∇ × V = 4π/c J(t,x,y,z) - 1/c (1/c V_tt + ∇ Φ_t ).

```
∇ × ∇ × V = 4π/c J(t,x,y,z) - 1/c (1/c V_tt + ∇ Φ_t ).
```

```
( -Δ + (∇∇· + 1/c² ∂²/∂t²) ) V + 1/c ∇Φ_t = 4π/c J(t,x,y,z).
```

Thus, the original Maxwell system has been reduced to an equivalent system of two equations:

−ΔΦ − 1/c ∇·V_t = 4πρ(t,x,y,z),

(−Δ + (∇∇·)^t + 1/c² ∂²/∂t²) V + 1/c ∇Φ_t = 4π/c J(t,x,y,z).

This system can also be written more compactly as

⎛ −Δ      −1/c ∇·∂/∂t ⎞ ⎛ Φ ⎞   ⎛ 4πρ ⎞
⎝ 1/c ∇∂/∂t  −Δ+(∇∇·)^t+1/c² ∂²/∂t² ⎠ ⎝ V ⎠ = ⎝ 4π/c J ⎠.

We refer to this system as the reduced Maxwell system. In this system, the number of equations is the same as the number of unknowns. Indeed, it contains two equations (a scalar equation and a vector equation) and requires two unknowns (a scalar function and a vector function).

Let us now apply the Fourier transform in the time variable t, as in Section 22.1. Let the subscript ω denote the Fourier coefficient of frequency ω in the Fourier expansion of the corresponding function. Because the time derivative is replaced by multiplication by iω in the transformed system, we have

⎛ −Δ      −iω/c ∇· ⎞ ⎛ Φ_ω ⎞   ⎛ 4πρ_ω ⎞
⎝ iω/c ∇  −Δ+(∇∇·)^t−ω²/c² ⎠ ⎝ V_ω ⎠ = ⎝ 4π/c J_ω ⎠.

In the next section, we use one extra assumption to reduce further the reduced Maxwell system into a system of four independent scalar Helmholtz equations.

## 22.12 Reduction to Three-Dimensional Helmholtz Equations

Here we further reduce the above reduced Maxwell system to a system of four decoupled scalar Helmholtz equations that can in fact be solved independently of each other. For this purpose, however, we need to assume that

∇·V = −1/c Φ_t

and that this function has continuous derivatives in space. The reduction is displayed schematically in Figure 22.7.

Using this assumption in the reduced Maxwell system, one can see immediately that certain terms are canceled, and we get

⎛ −Δ+1/c² ∂²/∂t²   0 ⎞ ⎛ Φ ⎞   ⎛ 4πρ ⎞
⎝ 0   −Δ+1/c² ∂²/∂t² ⎠ ⎝ V ⎠ = ⎝ 4π/c J ⎠.

![](img/1f293b0ceb2de964310ea7f941a1b580_562_0.png)

Figure 22.7. The wave and Maxwell equations can be reduced to the Helmholtz equation by a Fourier transform in the time variable t and the assumption ∇ · V = -1/c Φ_t, respectively.

Using the Fourier transform as at the end of Section 22.11 above, we have

```
\begin{pmatrix} -\Delta - \frac{\omega^2}{c^2} & 0 \\ 0 & -\Delta - \frac{\omega^2}{c^2} \end{pmatrix} \begin{pmatrix} \Phi_\omega \\ V_\omega \end{pmatrix} = \begin{pmatrix} 4\pi \rho_\omega \\ \frac{4\pi}{c} J_\omega \end{pmatrix}.
```

Note that the second equation is a vector equation that contains three independent scalar Helmholtz equations. Thus, the original Maxwell system has been reduced to the Helmholtz equation in the three spatial dimensions x, y, and z.

The Helmholtz equation in three dimensions and its numerical solution are discussed further in Chapters 25 and 27 below.

## 22.13 Exercises

- 1. Use the "dynamicMatrix" and "difference2" objects in Section 3.14 and Section A.10 of the Appendix to implement the finite-difference discretization of the Helmholtz equation (Section 22.3). The discrete boundary conditions are incorporated in the coefficient matrix as in Chapter 7, Section 4. Because the boundary conditions on the right edge are complex, you actually need "dynamicMatrix<complex>" and "difference2<complex>" objects.

- 2. Use the above objects to implement the bilinear finite-element discretization of the Helmholtz equation (Section 22.5). Calculate the stiffness matrix according to the guidelines in Chapter 12, Section 5, with the required changes. In particular, keep in mind that square elements are used here rather than triangles.

- 3. Apply your finite-difference and bilinear finite-element codes to the model problem in Section 22.6. Compare the discretization errors and levels of adequacy in the two methods.

- 4. Apply your finite-difference and bilinear finite-element codes to the measuring problem in Section 22.8. Use fictitious grid points above and below the slit to complete the grid into a rectangular computational grid.

- 5. Construct the initial, coarse triangulation that poorly approximates the domain in Figure 22.5. The solution can be found in Section A.22 of the Appendix.

- 6. Assemble the stiffness matrix for the Helmholtz equation on the above mesh. Use the code in Chapter 16, Section 5, with the required changes. In particular, use the "polynomial" object in Chapter 5, Sections 13 and 14, to calculate the contribution from the Helmholtz term.

- 7. Repeat the above exercise, only this time modify the code in Chapter 16, Section 5, to assemble the contribution from the mixed boundary conditions. Note that, because these boundary conditions are complex, you must use a "sparseMatrix<complex>" object to store the stiffness matrix.

- 8. Use your answer to the previous exercise to implement the adaptive-refinement algorithm to refine the above coarse mesh. Remember to use automatic boundary refinement only at boundary edges that lie next to the circular boundary segment. To loop over refinement levels, use the code in Section A.21 with the required changes. Because the boundary conditions are complex, you need "dynamicVector<complex>", "sparseMatrix<complex>", and "multigrid<complex>" objects. (The implementation of triangles and meshes can remain the same as before.)
