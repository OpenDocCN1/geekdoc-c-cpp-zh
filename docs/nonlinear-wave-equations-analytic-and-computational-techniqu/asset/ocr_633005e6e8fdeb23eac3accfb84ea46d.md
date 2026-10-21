[I₂ denotes the 2 × 2 identity matrix], and by using (2.12) we get

(2.16) \[\tilde{\Psi}(x,k)=\tilde{\Phi}(x,k)=\begin{cases}e^{xA_{+}(k)},&\text{for }x>0,\\e^{xA_{-}(k)},&\text{for }x<0.\end{cases}\]

From (2.16) and taking into account (2.15) and (2.10), we arrive at

\[S(k)=\begin{pmatrix}a(k)&\bar b(k)\\b(k)&\bar a(k)\end{pmatrix}=W_{+}^{-1}(k)W_{-}(k)=\frac{\lambda+k}{2\lambda}\begin{pmatrix}1-\frac{q_{+}q_{-}^{*}}{(\lambda+k)^{2}}&i\frac{(q_{+}-q_{-})}{\lambda+k}\\i\frac{(q_{-}^{*}-q_{+}^{*})}{\lambda+k}&1-\frac{q_{-}q_{+}^{*}}{(\lambda+k)^{2}}\end{pmatrix}.\]

Putting λ = iℓ with ℓ ∈ (0, q₀), from the preceding equation we obtain:

\[a(k)=\frac{(k+i\ell)^{2}-q_{0}^{2}e^{i(\theta_{+}-\theta_{-})}}{2i\ell(k+i\ell)}=\frac{k^{2}-\ell^{2}-q_{0}^{2}\cos(\theta_{+}-\theta_{-})+i\left(2k\ell-q_{0}^{2}\sin(\theta_{+}-\theta_{-})\right)}{2i\ell(k+i\ell)}.\]

As a result a(k)=0 if and only if

(2.17) \[\cos(\theta_{+}-\theta_{-})=\frac{k^{2}-\ell^{2}}{q_{0}^{2}},\qquad \sin(\theta_{+}-\theta_{-})=\frac{2k\ell}{q_{0}^{2}}.\]

Equation (2.17) has a unique solution k₀ ∈ (−q₀, q₀), unless q₊ = q₋. This eigenvalue k₀ = 0 iff θ₊ − θ₋ is an odd multiple of π.

From now on, we denote with k₀ the unique discrete eigenvalue of the free Hamiltonian operator associated to the scattering problem (1.3) and computed in the example above.

# 3. Resolvent of the free Hamiltonian

In this section we calculate the resolvent (k − H_f)⁻¹ of the free Hamiltonian H_f. The result obtained will be used in the next section to determine the location of the discrete eigenvalues.

Let us compute the resolvent (k − H_f)⁻¹ of the free Hamiltonian for k ∉ σ(H_f) = Σ ∪ {k₀} if q₊ ≠ q₋ [or k ∉ σ(H_f) = Σ if q₊ = q₋]. Letting F(x) be a column vector function in L²(ℝ)² = L²(ℝ) ⊕ L²(ℝ), we seek the unique vector function Ψ(k, x) in L²(ℝ)² such that H_f Ψ = k Ψ − F. Writing Ψ(x, k) = W(x, k) ψ(x, k), where W(x, k) = W₊(k)θ(x) + W₋(k)θ(−x), we get for 0 ≠ x ∈ ℝ

(3.1) \[\psi'(x,k)=-i\lambda\sigma_{3}\psi(x,k)+iW^{-1}(x,k)\sigma_{3}F(x),\]

where we have used that A(x,k)W(x,k) = −iλW(x,k)σ₃.

THEOREM 3.1. Let q₊ ≠ q₋ and k ∈ ℂ⁺. Then for F ∈ L²(ℝ)² and k ∉ Σ ∪ {k₀} we have

(3.2) \[[(k-H_f)^{-1}F](x)=\int_{-\infty}^{\infty}dy\,[K_f(x,y;k)+K_{f1}(x;k)K_{f2}(y;k)]F(y),\]