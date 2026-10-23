
associated with a piecewise constant basis function with the value 1 in one tetrahedron and 0 in all the other tetrahedra.

Finally, the scalar functions p_k defined in Γ_k (1 ≤ k ≤ 4) can be approximated by functions that are constant in each individual triangle in Γ_k. This way, the number of degrees of freedom in p_k is the same as the number of triangles in Γ_k (1 ≤ k ≤ 4). In fact, each degree of freedom is associated with a piecewise constant basis function defined in Γ_k with the value 1 in one triangle and 0 in all the other triangles.

Once restricted to these basis functions, the original weak formulation of the Maxwell equations introduced in Section 29.9 takes the form of a discrete linear system of algebraic equations, with the rectangular coefficient matrix of the form

```
( A \n Z )
```

where the square matrix A approximates the bilinear form a((E, B),(Ẽ, B̃)) associated with the first and second equation (the curl equations) in the weak form in Section 29.9, and the rectangular matrix Z discretizes the (weak) constraint equations.

As discussed in the previous section, we only need to consider vector functions Ẽ and B̃ for which the constraints vanish (weakly). It is not easy, however, to pick such functions only. To avoid this difficulty, we resort to the original Lagrange-multiplier setting introduced in Sections 29.2–29.4 above.

Note that each row ẑ in the rectangular matrix Z represents the linear functional (ẑ,·) obtained by taking the inner product of ẑ with a vector. The gradient of this functional is just the column vector ẑ^t obtained from the transpose of this row. As discussed in Section 29.7, we can thus extend the above algebraic system back into its original Lagrange-multiplier form, with the square coefficient matrix

```
( A  Z^t \n Z  0 )
```

and the extra unknown functions λ_k, which have the same number of degrees of freedom as the corresponding functions p_k (1 ≤ k ≤ 6). In this setting, Ẽ and B̃ no longer need to satisfy any homogeneous constraint, so the implementation is much easier.

## 29.11 Hermitization

Let us now return to the original weak form of the Maxwell equations in Section 29.9. In the sequel, we assume that

```
Γ_3 = Γ_4 = ∅
```

so

```
∂Ω = Γ_1 ∪ Γ_2
```

Using Green’s curl formula

```
∫_Ω (∇ × B)·Ẽ dΩ − ∫_Ω B·(∇ × Ẽ) dΩ = ∫_{∂Ω} (ñ × B)·Ẽ ds = − ∫_{∂Ω} B·(ñ × Ẽ) ds
```

[21], it then follows from the natural boundary conditions for B on Γ₂ and the homogeneous boundary conditions for Ē on Γ₁ that

```
∫_Ω (∇ × B) · Ē dΩ
= ∫_Ω B · (∇ × Ē) dΩ + ∫_{Γ₁∪Γ₂} (n̂ × B) · Ē ds
= ∫_Ω B · (∇ × Ē) dΩ + ∫_{Γ₂} (n̂ × B) · Ē dΓ₂ − ∫_{Γ₁} B · (n̂ × Ē) dΓ₁
= ∫_Ω B · (∇ × Ē) dΩ.
```

Let us now use this result to substitute for the second term (the curl term) in the first equation in the weak form in Section 29.9. Using also the fact that both Ē and B̃ are independent of the time variable t, we have

```
1/c ∂/∂t ∫_Ω E · Ē dΩ − ∫_Ω B · (∇ × Ē) dΩ = −4π/c ∫_Ω J · Ē dΩ,
∫_Ω (∇ × E) · B̃ dΩ + 1/c ∂/∂t ∫_Ω B · B̃ dΩ = 0.
```

Upon applying the Fourier transform to these equations, the partial derivation with respect to t is replaced by multiplication by iω. Furthermore, upon multiplying the equations by the constant factor −i and adding them to each other, the bilinear form a defined by the left-hand side of this sum is Hermitian in the sense that

```
a((E, B), (Ē, B̃)) = a((Ē, B̃), (E, B)).
```

As a result, the matrix A (Section 29.10) is Hermitian as well, in the sense that

```
A_{i,j} = Ā_{j,i}.
```

Note that, under the present assumptions, the linear operators L₃ and L₄ are unnecessary. Furthermore, since the natural boundary conditions on Γ₁ and Γ₂ have already been used in Green’s formula above, they don’t need to be used again as constraints, so L₁ and L₂ are unnecessary as well. Thus, the rectangular matrix Z of Section 29.10 should contain only those rows associated with L₅ and L₆, the divergence operators.

## 29.12 The Reduced Electricity Equations

The first equation in the modified weak form in Section 29.11 can be written in the form

```
∫_Ω B · (∇ × Ē) dΩ = 1/c ∂/∂t ∫_Ω E · Ē dΩ + 4π/c ∫_Ω J · Ē dΩ.
```

The second equation, on the other hand, can be simplified by substituting ∇ × Ē for B̃:

```
∫_Ω (∇ × E) · (∇ × Ē) dΩ + 1/c ∂/∂t ∫_Ω B · (∇ × Ē) dΩ = 0,
```

or, using the above equation,

$$\int_{\Omega}(\nabla\times E)\cdot(\nabla\times\widetilde{E})\,d\Omega+\frac{1}{c^2}\frac{\partial^2}{\partial t^2}\int_{\Omega}E\cdot\widetilde{E}\,d\Omega=-\frac{4\pi}{c^2}\frac{\partial}{\partial t}\int_{\Omega}J\cdot\widetilde{E}\,d\Omega.$$

Fortunately, both $B$ and $\widetilde{B}$ are missing in this equation. Thus, the original system in $E$ and $B$ has been reduced to an equation in $E$ alone. Furthermore, the bilinear form $a(E,\widetilde{E})$ defined by the first term in the equation (the curl term) is Hermitian, and the quadratic form associated with it is nonnegative, and can even be coercive if the boundary conditions are properly designed [21]. Thus, the equation has the same nature as the wave equation in Section 22.1.

As a result, the square finite-element matrix $A$ obtained from this bilinear form by writing the scalar functions in $E$ and $\widetilde{E}$ in terms of piecewise linear basis functions is Hermitian and positive definite as well. The rectangular matrix $Z$ that should be used in conjunction with it (see Section 29.10) should contain only those rows associated with the linear operator $L_6$, the divergence of $E$.

The above equation can be discretized in the time variable $t$ by either explicit or (semi) implicit time marching. Alternatively, the Fourier transform can be used to replace each partial derivation with respect to $t$ with multiplication by iω.

Once $E$ has been solved for, it can be used in the original Maxwell system to solve for the magnetic field $B$ as well. Alternatively, the same approach as above can be used to obtain an equation for $B$ alone, and solve it independently of $E$.

## 29.13 The Nonlinear Maxwell Equations

In the nonlinear Maxwell equations, the term $E_1$ in the systems in Sections 29.9 and 29.11 is replaced by

$$(E+Q+|E|^2E)_t,$$

where the unknown field $Q$ satisfies

$$\frac{1}{t^2}Q_{tt}+\frac{1}{t}Q_t+Q=E.$$

The reduced electricity equation in Section 29.12 then takes the form

$$\int_{\Omega}(\nabla\times E)\cdot(\nabla\times\widetilde{E})\,d\Omega+\frac{1}{c^2}\frac{\partial^2}{\partial t^2}\int_{\Omega}(E+Q+|E|^2E)\cdot\widetilde{E}\,d\Omega=-\frac{4\pi}{c^2}\frac{\partial}{\partial t}\int_{\Omega}J\cdot\widetilde{E}\,d\Omega.$$

## 29.14 Exercises

introduced in Section 21.7. The nonlinear term |E|² E is handled by Newton’s iteration as in Sections 9.14 and 27.7. In this context, the solution on the previous time level serves as an initial guess for Newton’s iteration on the current time level.

- 1. Assume that the electric field E has already been found by solving the reduced electricity equations in Section 29.12. Rewrite the original Maxwell system as a system for the magnetic field B alone by throwing the terms that contain the known field E to the right-hand side.
- 2. Alternatively, use the same technique used to obtain the reduced electricity equations to reduce the original Maxwell system to a reduced magnetics equations in B alone, independent of E.
- 3. Show that the reduced electricity equations can be written as a system of three equations, each of which uses a field Ē with only one nonzero component: Ē₁ ≠ 0 and Ē₂ ≡ Ē₃ ≡ 0 in the first equation, Ē₂ ≠ 0 and Ē₁ ≡ Ē₃ ≡ 0 in the second equation, and Ē₃ ≠ 0 and Ē₁ ≡ Ē₂ ≡ 0 in the third equation. (Indeed, the sum of these three equations produces the original equation.) This way, the system can be viewed as a 3 × 3 system, whose (i, j)th element (1 ≤ i, j ≤ 3) uses Ēᵢ and Eⱼ.
- 4. Show that, for any two vector fields B and E, the inner product of their curl is
  (∇ × B)·(∇ × E) = Σᵢ=1³ Σₖ=1³ (∇×)ᵢ,ₖ Bₖ Σⱼ=1³ (∇×)ᵢ,ⱼ Ēⱼ
  = Σⱼ,ₖ=1³ Σᵢ=1³ (∇×)ᵢ,ₖ Bₖ (∇×)ᵢ,ⱼ Ēⱼ
  = Σⱼ,ₖ=1³ (Bⱼ)ₓₖ (Ēⱼ)ₓₖ − Σⱼ,ₖ=1³ (Bₖ)ₓⱼ (Ēⱼ)ₓₖ
  = trace((∇B)ᵗ(∇Ē)) − trace((∇B)(∇Ē)),
  where (∇×) is the curl matrix in Section 21.1, and the trace of a matrix is the sum of its main-diagonal elements. Note that, thanks to bilinearity, it is sufficient to prove the above for B and E with only one nonzero component, say B₁ ≠ 0 and E₁ ≠ 0 but B₂ = B₃ = E₂ = E₃ ≡ 0, or B₁ ≠ 0 and E₂ ≠ 0 but B₂ = B₃ = E₁ = E₃ ≡ 0.
- 5. Show that, for any vector field B, the following 3 × 3 matrices (or linear operators) are the same:
  (∇B)ᵗ − ∇B = (∇ × B) ×.
  Use this formula, the previous exercise, the formula at the end of Section 21.1, and Green’s divergence formula to prove Green’s curl formula for the divergence-free vector field ∇ × B and the vector field E.
