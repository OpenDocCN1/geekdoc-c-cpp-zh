
We will discuss more about the nonlinearity and ill-posedness of inverse problems while discussing DOT below.

### 5.2.2.2 Connection to DOT

EIT is a close cousin of DOT because the forward problem for both is elliptic with DOT being worse in the sense that DOT requires estimating two functions mainly q = (D, μ_a) rather than one parameter for EIT. However DOT is an important modality in practice because DOT can be used as an alternative to X-ray in detecting cancer in the breast and the brain.

## 5.3 Diffuse Optical Tomography

In optical imaging, low-energy visible light is used to illuminate biological tissue. The illumination of the tissue is modelled as a photon transport phenomenon. The process is described by the most widely applied equation in optical imaging, the radiative transfer, or transport equation (RTE) [11, 12]. RTE is an integro-differential equation for photon density and has spatially dependent diffusion and absorption parameters as coefficients. These coefficients are a priori unknown for a particular tissue sample of an individual who is being examined for cancer. Therefore, the problem is to infer from the measurements of the photon density on the boundary the coefficients of absorption and diffusion in the tissue. This estimate helps determine the location and size of the abnormality in the tissue.

### 5.3.1 Radiative Transport Equation

Let Ω ⊂ R^n, with n = 2, 3 and with boundary ∂Ω, let ν(x) denote the outward unit normal to ∂Ω at the point x ∈ ∂Ω, and Γ± is defined as,

Γ± := { (x,s,t) ∈ ∂Ω × S^{n-1} × [0,T], ±ν(x)·s > 0 }.

For example, one may assume a geometry as shown in Figure 5.1.

![](img/81c56bc4b2fca1951aff5e0ab85b66be_105_0.png)

**FIGURE 5.1** Tomographic imaging.

Then the RTE is given by,

$$1/c ∂u/∂t (x,s,t) + s·∇u(x,s,t) + a(x)u(x,s,t) - b(x) ∫_{S^{n-1}} Θ(s·s') u(x,s',t) ds' = f(x,s,t) (5.20)$$

together with the initial and boundary conditions,

$$u(x,s,0) = 0 \quad \text{in } Ω × S^{n-1} (5.21)$$

$$u(x,s,t) = 0 \quad \text{on } Γ_- (5.22)$$

where u(x,s,t) describes the density function of particles (photons) which travel in Ω at time t through the point x in the direction s ∈ S^{n-1}, the unit sphere in R^n. The parameter a is the total cross section or attenuation, and b is the scattering cross section. The difference μ := a − b has the physical meaning of an absorption cross section. The parameters a, b and μ are assumed to be real, nonnegative, and bounded functions of the position. The parameters a and b are the sought-for tissue parameters and c is the velocity of light. The function Θ is the scattering phase function characterizing the intensity of a wave incident in direction s′ scattered in the direction s. It is assumed to be a real, nonnegative function and is normalized to one. The inverse problem is to recover a and b from measurements of some given functionals of the outgoing density u_j|_{Γ₊} at the boundary ∂Ω for m_s different source distributions f_j, j = 1, …, m_s.

### 5.3.2 DOT Model

Simpler deterministic models can be derived from RTE by expanding the density u and source f in spherical harmonics and retaining a limited number of terms [13, 14, 15, 16]. Due to the prevalence of scattering, the flux is essentially isotropic a small distance away from the sources; i.e. it depends only linearly on s. Thus we may describe the process adequately by the first two moments of u. We get the diffusion approximation P₀. The frequency-domain diffusion approximation can easily be obtained by Fourier transforming the time-domain equation. Furthermore, the diffusion approximation to the radiative transfer model can be written in the time independent (dc) case as in [16],

$$-∇·(D∇u) + μ_a u = 0. (5.23)$$

The associated boundary condition is

$$u + 2D ∂u/∂ν = f, x ∈ ∂Ω. (5.24)$$

If we let Ω be the domain under consideration with surface ∂Ω, the weak forward problem corresponding to Equation (5.23) is to find u ∈ H¹(Ω) such that for all v ∈ H¹(Ω), the following variational equation is satisfied,

$$∫_Ω D∇v·∇u dx + ∫_Ω μ_a v u dx + ∫_{∂Ω} 1/2 v u ds = ∫_{∂Ω} v f ds. (5.25)$$

![](img/81c56bc4b2fca1951aff5e0ab85b66be_106_0.png)

**FIGURE 5.2** Nonlinear mapping.

Now, we can define the forward problem as: given sources f_j in ∂Ω and q in Q, a vector of model parameters, for example the coefficient of diffusion D and the coefficient of absorption μ_a (i.e. q = (D, μ_a)^T) that belongs to a parameter set Q, find the data u on ∂Ω and the inverse problem as: given data z on ∂Ω find q. We can recast the forward problem in an abstract setting with u in an appropriate abstract space H, and f represents a source or a forcing distribution. In general, measurement of u may not be possible; only some observable part z = 𝒞 u(q) of the actual state u(q) may be measured. In this abstract setting, the objective of the inverse or parameter estimation problem is to choose a parameter q^* in Q, that minimizes an error criterion or cost functional J(u(q), 𝒞 u(q), q) over all possible q in Q subject to u(q) satisfying the diffusion approximation. A typical observation operator is,

$$𝒞^f u(q) = \{ -D ∂u/∂ν (x_i ; q, f) \}_{i=1}^m  (5.26)$$

where x_i is in ∂Ω, m is the number of measurements, and the second equality comes from the boundary condition (5.24). A typical Tikhonov cost functional J_λ is given as,

$$J_λ(q) = 1/2 Σ_{j=1}^{m_s} Σ_{i=1}^{m} w_{ij} | 𝒞_i^{f_j} u(q) - z_i^{f_j} |^2 + λ || q - q_0 ||^2  (5.27)$$

where z_i^{f_j} is the measured data at the boundary for a given source f_j, w_{ij} is the weight for ij-th data, and λ is the Tikhonov regularization parameter. As shown in Figure 5.2, composing u(q) and 𝒞 u(q) we obtain the parameter-to-output mapping:

$$T : Q → Z$$

such that T q = 𝒞 u(q), where Z is the space of measurements. This is the nonlinear mapping of DOT in abstract setting. The map from Q to Z is nonlinear because the solution of a partial differential equation is a nonlinear function of its coefficients q = (D, μ_a).

## 5.4 Computational Aspect and the Regularization of the Ill-Posed Problem

There are various approaches for solving this nonlinear ill-posed problem; we outline a few approaches in this section. In general for complex geometries, the analytic solution is intractable. Therefore, one requires numerical solutions. The finite element method (FEM) is somewhat more versatile because of its ease in complex geometries and modelling boundary effects. The FEM is a variational method used to approximate the solution by a family of finite dimensional basis functions. Then the forward problem is reduced to one of linear algebra and one computes the approximate solution using FEM codes. The FEM is derived by projecting the weak form of Equation (5.25) onto a finite dimensional function space. For example, the finite dimensional function space could be the set of continuous and twice differentiable, piecewise cubic polynomials.

More precisely, for example in EIT, we can project the infinite dimensional solution space X into a finite dimensional subspace X_K ⊂ X which means to restrict u and v above to lie in X_K rather than X. Let us assume that there exists a family of basis functions φ_m(x) for m = 1,⋯,K for X_K. Then let u_K = Σ_{m=1}^K c_m φ_m(x) to be the approximation to u and we want the weak formulation to be satisfied for the K test functions φ_k = v for k = 1,⋯,K. Now plugging this into the weak formulation we obtain the system of equations for c_m:

$$\sum_{m=1}^K (∫_Ω q ∇φ_m · ∇φ_k dx) c_m = ∫_{∂Ω} f Γ_D φ_k ds (5.28)$$

for k = 1,⋯,K. If we denote

$$A_{mk} = ∫_Ω q ∇φ_m · ∇φ_k dx$$

$$F_k = ∫_{∂Ω} f Γ_D φ_k ds$$

then we can solve for the solution c = (c_m)_{m=1}^K, which depends nonlinearly on q using the linear system Ac = F where A is a K × K matrix and F is a vector of length K. We can also approximate the infinite dimensional parameter space Q by a finite dimensional subspace Q_M ⊂ Q. The solution to the finite dimensional problem is the solution q_M in Q_M that is closest to the infinite dimensional optimization problem, for example J_α(q). Therefore we assume that there exists a family of basis functions ψ_k(x) for k = 1,⋯,M for Q_M. Then set q_M = Σ_{k=1}^M q_k ψ_k(x) to be the approximation to q and we arrive at the finite dimensional nonlinear optimization problem for q_M = (q_k)_{k=1}^M:

$$\Ĵ_{α1,α2}(q_M) = Σ_{k=1}^{K̂} |ĝ_k(f) - ĝ_k^δ|^2 + α1 Σ_{i=1}^M δ_i |q_i - q_i^*|^p + α2 Σ_{j=1}^Z d_j |Δ_j q_M|. (5.29)$$

where 1 ≤ p ≤ 2 and δ_i's are weights, ĝ_k(f) = Γ_D u_K^{q_M}(f)[x̂_k] is the trace of the solution evaluated at K̂ boundary points x̂_k, ĝ_k^δ is the noisy voltage data collected at the boundary point x̂_k, the second term is the approximation to the TV term using a nearest neighbor approximation where Z is the number of nearest neighbors, and d_j is the distance between two neighbors [18, 17, 19].

EIT is well known to suffer from a high-degree of nonlinearity and severe ill-posedness [20, 21]. Therefore, regularization is required to produce reasonable electrical impedance images. Most reconstruction methods are deterministic, such as the factorization method
