Of course, realistic examples require more than two integration points for precision.

We write our coupled equations (26.8) in the matrix form as

```
[H][ψₙ] = Eₙ[ψₙ]  (26.9)
```

or as explicit matrices

```
⎛ k₁²/(2μ) + 2/π V(k₁,k₁)k₁²w₁   2/π V(k₁,k₂)k₂²w₂   …   2/π V(k₁,k_N)k_N²w_N ⎞
⎜ 2/π V(k₂,k₁)k₁²w₁   2/π V(k₂,k₂)k₂²w₂ + k₂²/(2μ)   …   … ⎟
⎜   ⋱                ⋱                ⋱                ⋱ ⎟
⎝ …                …                …   k_N²/(2μ) + 2/π V(k_N,k_N)k_N²w_N ⎠ × ⎛ ψₙ(k₁) ⎞ = Eₙ ⎛ ψₙ(k₁) ⎞
                                   ⎜ ψₙ(k₂) ⎟           ⎜ ψₙ(k₂) ⎟
                                   ⎜  ⋮    ⎟           ⎜  ⋮    ⎟
                                   ⎝ ψₙ(k_N)⎠           ⎝ ψₙ(k_N)⎠ .  (26.10)
```

Equation 26.9 is the matrix representation of the Schrödinger equation (26.3). The wave function ψₙ(k) on the grid is the N × 1 vector

```
[ψₙ(kᵢ)] = ⎛ ψₙ(k₁) ⎞
           ⎜ ψₙ(k₂) ⎟
           ⎜  ⋮    ⎟
           ⎝ ψₙ(k_N)⎠ .  (26.11)
```

The astute reader may be questioning the possibility of solving N equations for (N + 1) unknowns, ψₙ(kᵢ), and Eₙ. Only sometimes, and only for certain values of Eₙ (eigenvalues), will the computer be able to find solutions. To see how this arises, we try to apply the matrix inversion technique (which we will use successfully for scattering in Section 26.3). We rewrite (26.9) as

```
[H − Eₙ I][ψₙ] = [0]  (26.12)
```

and multiply both sides by the inverse of [H − Eₙ I] to obtain the formal solution

```
[ψₙ] = [H − Eₙ I]⁻¹[0] .  (26.13)
```

This equation tells us that (1) if the inverse exists, then we have the trivial solution ψₙ ≡ 0, which is not revealing, and (2) for a nontrivial solution to exist, our assumption that the inverse exists must be incorrect. Yet we know from the theory of linear equations that the inverse fails to exist when the determinant vanishes:

```
det[H − Eₙ I] = 0  (bound-state condition) .  (26.14)
```

Equation 26.14 is the N + 1th equation needed to find unique solutions to the eigenvalue problem. Although, there is no guarantee that solutions of (26.14) can always be found, if they are found they are the desired eigenvalues of (26.9).