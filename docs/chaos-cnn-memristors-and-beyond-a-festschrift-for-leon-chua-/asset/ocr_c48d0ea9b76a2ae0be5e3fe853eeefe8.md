approximate quantitative agreement with the corresponding regions of the Rössler system. Thus, the characteristic parameters of anticipating synchronization can be simply estimated from the linear Eqs. (19) that model the local dynamics of the chaotic system close to the fixed point.

# 3.3. Extended phase-lag compensating coupling

To further improve the PLCC algorithm, we employ an idea from the DFC theory. In the original DFC algorithm (cf. [32]), the coupling law is analogous to that of the anticipating synchronization. To improve the DFC, [12] proposed an extended version of the original DFC, which incorporates in the feedback loop an information from many previous states of the system. This modification, known as an extended DFC (EDFC), makes possible the stabilization of high-periodic orbits with large positive Lyapunov exponents (cf. [33]). We use the idea of the EDFC to improve the performance of the PLCC algorithm [42]. We refer to this modification as an extended PLCC (EPLCC). The PLCC uses the single difference between the current state of the master system and the time-delayed state of the response system, whereas the EPLCC extends this perturbation to an infinite series of corresponding differences that are time-delayed by integer multiplies of the delay τ. Again, we demonstrate the idea for two coupled unstable spirals

Ż₁ = (γ + iω)Z₁, (21a)
Ż₂ = (γ + iω)Z₂ + kS(t). (21b)
Now the EPLCC perturbation S(t) is governed by
S(t) = e^{iα}[Z₁(t) - Z₂(t - τ)] + Σ_{n=1}^{∞} Rⁿ e^{i(n+1)α}[Z₁(t - nτ) - Z₂(t - (n + 1)τ)], (22)
where R is a memory parameter that regulates the weight of the time-delayed information. We require -1 < R < 1 to guarantee the convergence of the infinite sum. The case of R = 0 corresponds to the PLCC considered in the previous section (cf. Eq. (19b)). Note that S(t) vanishes for any value of R when the system moves along the synchronization manifold, since the equality Z₁(t - nτ) = Z₂(t - (n + 1)τ) holds on the manifold for all n.

The phase lag of each term in the sum is compensated by the multiplier e^{i(n+1)α}, and the amplitude is weighted by the multiplier Rⁿ, such that the contribution of terms exponentially decreases with the increase of time delay. At the first look, Eq. (22) seems to be very complex. Fortunately, the infinite sum can be rewritten in an equivalent, recursive form
S(t) = e^{iα}[Z₁(t) - Z₂(t - τ) + RS(t - τ)] (23)
and implemented experimentally with the single delay line (cf. [12]). Now, the stability of the synchronized state is defined by variational equations
Δ̇(t) = (γ + iω)Δ(t) - kS(t - τ), (24a)
S(t) = e^{iα}[Δ(t) + RS(t - τ)], (24b)
where Δ(t) = Z₁(t) - Z₂(t - τ) describes the deviation from the synchronization manifold. This leads to the characteristic equation
(λ - γ)(e^{-i(α - ωτ)+λτ} - R) + k = 0. (25)
For R = 0, it coincides with Eq. (20) analyzed in the previous section. Here, as well as in the previous section, we set α = ωτ and analyze the simplified version of Eq. (25)
(λ - γ)(e^{λτ} - R) + k = 0. (26)
Unfortunately, the solution of Eq. (26) for R ≠ 0 cannot be expressed through the Lambert function. Although the analytical solution of this equation is not available, the boundaries of stability can be obtained analytically. The lower bound of stability k₁ = γ(1 - R) is deduced from Eq. (26) by substituting λ = 0. The upper bound of stability k₂ is defined by a Hopf bifurcation. Substituting λ = iΩ in Eq. (26) and denoting Ωτ = β, we obtain the dependence k₂ on τ in a parametric form
τ(β) = β(cos β - R) / (γ sin β),
k₂(β) = γ(cos β - R) + (β sin β)/τ(β). (27)
These boundaries are depicted in Fig. 8 for R = -0.3. We see that the EPLCC extends the stability region of the synchronization manifold in the (τ,k)-plane. The maximum prediction time can be obtained from Eqs. (27) in the limit β → 0. The necessary condition for stability of the synchronized state is
τ < τ_H = (1 - R)/γ. (28)