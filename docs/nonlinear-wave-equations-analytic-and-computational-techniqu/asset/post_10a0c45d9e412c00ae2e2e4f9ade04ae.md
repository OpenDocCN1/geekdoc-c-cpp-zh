
be identically zero due to the smoothness of A₀, and for simplicity we shall largely ignore the role of the norming constants in our exposition here. As noted above, Klaus & Shaw [18] have shown that the eigenvalues (for bell-shaped potential A₀ in (2.1)) are purely imaginary. The evolution in time of the scattering data in the spectral domain is governed by the other half of the Lax pair, a linear problem, and is simple and explicit. Finally, the solution at times t > 0 is recovered by an inverse scattering map; that is, the solution u(x,t;ε) is recovered from the time-evolved scattering data (eigenvalues, norming constants, reflection). A complete and detailed description of this methodology for (1.1) can be found, for example, in the monographs [1,13].

### 2.2. WKB analysis

In the case of a Klaus–Shaw potential, as in (2.1), one may obtain further, formal information about the precise location of the eigenvalues by performing a WKB analysis. We only summarize the results here; details may be found in the article of Ercolani et al. [12]. We begin with the density function

(2.2) ρ⁰(η) := η/π ∫_{x₋(η)}^{x₊(η)} dx / √(A₀(x)² + η²) = 1/(π η) d/dη ∫_{x₋(η)}^{x₊(η)} √(A₀(x)² + η²) dx ,

defined for η ∈ (0,iA) where x±(η) are the two real turning points guaranteed to exist by our assumption that A₀ is bell-shaped and A := max_{x∈ℝ} A₀(x); see Figure 1. From ρ⁰ we obtain the function

![](img/c92a9d81ba7f671c83a4c600d27389fb_107_0.png)

Figure 1. The turning points x±(η).

(2.3) θ⁰(λ) := -π ∫_{λ}^{iA} ρ⁰(η) dη .

This function measures the number of WKB eigenvalues in the segment (λ,iA) ⊂ iℝ. We then define for N = 1,2,3,…

ε_N := -1/N ∫₀^{iA} ρ⁰(η) dη = 1/(π N) ∫_{-∞}^{∞} A₀(x) dx .

Finally, the WKB eigenvalues λ_{N,k}^{wkb} are defined (there are N of them for ε_N) by the formula

(2.4)  -∫_{λ_{N,k}^{wkb}}^{iA} ρ^0(η) dη = ε_N (k + 1/2) = θ^0(λ_{N,k}^{wkb})/π ,  k = 0, …, N - 1.

Evidently, we may rewrite the left-hand side as -∫_{λ_{N,k}^{wkb}}^{iA} ρ^0(η) dη = 2/π ∫_0^{x_+(λ_{N,k}^{wkb})} √{A_0(x)^2 + (λ_{N,k}^{wkb})^2} dx .

Therefore, writing λ_{N,k}^{wkb} = i τ_{N,k}^{wkb} for τ_{N,k}^{wkb} ∈ (0, A) ⊂ ℝ, the eigenvalue locations (important components of the scattering data for A_0) are approximately given by solutions to the equations

(2.5) ∫_0^{x_+(i τ_{N,k}^{wkb})} √{A_0(x)^2 - (τ_{N,k}^{wkb})^2} dx = π ε_N /2 (k + 1/2) , k = 0,1,2,…, N - 1.

## 3. Semiclassical soliton ensembles

### 3.1. Origins

We are now in a position to describe precisely the origin of the SSE. As noted above, the WKB method applied to (2.1) suggests that the reflection coefficient is negligible and the purely imaginary eigenvalues are given by a quantization condition of Bohr–Sommerfeld type (2.5). Remarkably, this information is completely parallel to the information used by Lax & Levermore [19] in their analysis of the zero-dispersion limit of the Korteweg–de Vries (KdV) equation. Lax & Levermore neglected reflection and adopted the WKB eigenvalues¹ in place of the true eigenvalues. That is, they approximated the initial data by a family of reflectionless potentials which, in the limit, approach the true initial data. Since exact information about the true scattering data (eigenvalues of (2.1) and the reflection coefficient) is not known, the temptation to adopt Lax & Levermore’s strategy is overwhelming, and we use the (formal) WKB scattering data in its place. This process, neglecting reflection and using the WKB eigenvalues, amounts to replacing the true initial data A_0 with some other initial condition, denoted by A_0^{(ε)}, which depends on the small parameter ε and for which the WKB data is the true data. Thus, this process introduces perturbations to the initial data, and we write

(3.1) A_0^{(ε)}(x) = A_0(x) + q^{(ε)}(x),

so that q^{(ε)} is the induced perturbation; see Figure 4 (b) for an example of such a perturbed initial condition. Because reflection is neglected, each solution of (1.1) with initial data A_0^{(ε)} is an N-soliton with N ∼ ε^{-1}. The collection of all these exact N-soliton solutions of (1.1) (with N → ∞ and ε ↓ 0) is the semiclassical soliton ensemble associated with the bell-shaped data A_0.

It is important to note, however, that in the case of the KdV equation, the Whitham equation is hyperbolic and is therefore locally well posed. Lax & Levermore appealed to this local well-posedness to absorb the asymptotically vanishing family of perturbations induced by their reflectionless approximation. As described above, we are unable to appeal to the well-posedness of the Whitham system in the

¹ In their case, these eigenvalues are associated with the WKB analysis of the spectral problem for the stationary Schrödinger operator associated with the solution of KdV by IST not with (2.1).

Finally, once the solution of RHP 4 is found, one recovers an $N$-soliton solution via the formula

$$u(x,t)=2i\lim_{\lambda\to\infty}\lambda m_{12}(\lambda;x,t),$$

where $m_{12}$ is the $(1,2)$ entry of $\mathbf{m}$.

#### 3.2.2. Steepest Descent

We condense the asymptotic analysis to its most abbreviated form². Roughly, after a change of coordinates, the meromorphic RHP can be exchanged for a sectionally holomorphic RHP. This allows the study of the $N\to\infty$ (equivalently, $\epsilon\downarrow0$) problem using the “$g$-function mechanism” [10], a modification of the steepest descent method [9]. This method of asymptotic analysis hinges on being able to find an appropriate complex phase, or “$g$-function”, which allows the RHP to go over to a tractable form in the limit. In the present setting, such a $g$ selects certain contours in the complex plane on which the RHP should be posed; the contours consist of bands which are fixed and gaps which may lie anywhere a certain inequality is satisfied. If $g$ and the appropriate contours (bands & gaps) can be found, the solution of the RHP (for small $\epsilon$) can be approximately built from Riemann theta functions of the hyperelliptic surface with branch points at the band end points. (Note: In [16,22] $g$ and the band/gap contours are found by an ansatz about the number of bands and numerical calculation. In contrast to direct simulation of (1.1) for small $\epsilon$, these calculations are extremely well conditioned; “bad” behavior has been factored out.) The upshot is that the semiclassical asymptotics for focusing NLS are described by modulated multiphase waves written in terms of theta functions, where the number of phases is related to the genus $G$ of the surface. The nonlinear caustics (phase transitions) correspond to a change in the genus of the surface. An essential feature of the analysis, one that bears on the problems below, is that this global parametrix for the RHP (uniformly close to the true solution on all of $\mathbb{C}$) is built by matching an “inner” part (near branch points) to an “outer” part (elsewhere).

The above description outlines the strategy employed by Kamvissis et al. [16]. This was the first analytic breakthrough in the analysis of the semiclassical NLS equation, and variations on this basic scheme have been used in much of the subsequent work on this problem; see, e.g., [2,22,31–33].

### 3.3. Nonlinear Caustics

As described in the previous subsection, nonlinear caustics are curves in space-time which separate qualitatively different modulated oscillations due to differences in the number of phases. The sharpening boundaries are clearly visible in well-resolved simulations of the initial-value problem; see Figure 2. Certainly, any reasonable theory of the semiclassical limit for (1.1) should be able to predict the number and location of such important features of the dynamics. However, much remains to be done before these phenomena are completely understood (but see the interesting recent work of Bertola & Tovbis [3,4]).

Applying the methodology of Kamvissis et al. [16] described above, the search for caustics thus amounts to a search, as parameters $x$ and $t$ vary, for topological changes in the region of the complex plane where a certain inequality must be satisfied in order for a gap contour to be located there. Using these ideas, Kamvissis et al. showed that a $G=0$ ansatz correctly describes the semiclassical behavior for $t\neq0$ and for $t$ sufficiently small (but independent of $\epsilon$). They also showed that the
