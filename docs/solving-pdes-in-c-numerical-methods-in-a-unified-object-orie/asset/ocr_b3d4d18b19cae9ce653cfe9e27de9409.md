for some tetrahedron s ⊂ M. This way, the number of equations is indeed the same as the number of unknown coefficients, that is, three times the total number of nodes that are away from Γ_D plus the total number of tetrahedra in the mesh.

# 31.4 Linearization

In each Newton iteration, the nonlinear term

```
∭_Ω v' (∇v) w dx dy dz
```

must be linearized at the current approximate solution v. For this purpose, the above representation of v is particularly helpful. Indeed, to have the required Jacobian, we have to take the partial derivative with respect to some unknown coefficient c_j^{(k)} (j ∈ M \ Γ_D, 1 ≤ k ≤ 3). Fortunately, as in Section 27.5 above, this can be done under the integral sign. Furthermore, this can also be done under the gradient sign:

```
∂/∂c_j^{(k)} ∭_Ω v' (∇v) w dx dy dz = ∭_Ω ∂/∂c_j^{(k)} (v' (∇v)) w dx dy dz = ∭_Ω (∂/∂c_j^{(k)} v') (∇v) w dx dy dz + ∭_Ω v' (∂/∂c_j^{(k)} (∇v)) w dx dy dz = ∭_Ω (ψ_j^{(k)})' (∇v) w dx dy dz + ∭_Ω v' (∇ψ_j^{(k)}) w dx dy dz.
```

For instance, by picking

```
w ≡ ψ_l^{(m)}
```

(for some node l ∈ M \ Γ_D and some integer 1 ≤ m ≤ 3) as at the end of Section 31.3 above, the above linearized term contributes to the ((l,m),(j,k))th element in the stiffness matrix the amount

```
∭_Ω (ψ_j^{(k)})' (∇v) ψ_l^{(m)} dx dy dz + ∭_Ω v' (∇ψ_j^{(k)}) ψ_l^{(m)} dx dy dz = ∭_Ω (∇v)_{k,m} ψ_j ψ_l dx dy dz + ∭_Ω (k == m) v' ∇ψ_j ψ_l dx dy dz = Σ_{t∈M} (∇v)_{k,m} ∭_t ψ_j ψ_l dx dy dz + (k == m) ∇' ψ_j ∭_t v ψ_l dx dy dz.
```

where

```
(k == m) ≡ { 1 if k = m, 0 if k ≠ m. }
```