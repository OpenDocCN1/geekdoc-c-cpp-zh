origin is an equilibrium point with a pair of complex conjugate eigenvalues σ ± jω, (σ < 0, ω ≠ 0) and a real eigenvalue γ > 0 satisfying |σ| < γ. If in addition, ξ has a homoclinic orbit through the origin, then ξ can be infinitesimally perturbed into a nearby vector field ξ* with a countable set of horseshoes.

The difficult part of Shilnikov’s theorem is rigorously confirming the existence of a homoclinic orbit at the origin. Such an orbit is double-asymptotic at the origin, that is, x_h(t) → 0 as t → ±∞. However, because of the piecewise-linear nature of the nonlinearity, we analyze the system in each linear region and then carefully “stitch” the trajectories at the boundaries. Since closed form solutions of trajectories and eigenspaces can be found for linear systems, we can plot the geometrical structure and typical trajectories of the piecewise-linear system. Fig. 10 shows a typical plot of eigenspaces for Chua’s circuit.

![](bbox=[0.095, 0.52, 0.46, 0.77])

Fig. 10. Eigenspaces for the Chua system. The nonlinearity separates phase space into three distinct regions. E^s(0) is the stable complex eigenspace associated with the origin. E^u(P+) is the unstable complex eigenspace associated with P+. For clarity, only the complex eigenspaces are shown. A trajectory x_h(t) initially starts along the unstable real eigenspace associated with the origin. Once the trajectory passes into D1, it is shown here to spiral tangentially to E^u(P+) before going through C1. If there exists a C1 such that it also lies on the line of intersection between E^s(0) and U1, we have found a homoclinic orbit x_h(t). We have exaggerated the homoclinic orbit by hand for clarity.

The detailed analysis is very involved and the reader is encouraged to go through the double scroll family paper [4] to understand the complete picture (such as rigorous analysis of bifurcation phenomenon). But there are three essential steps and we have included relevant equation, page numbers from the double scroll family paper [4] for correlating the “cookbook” approach in this chapter with Chua’s original work.

+   (1) Determine the eigenvalues for each of the linear regions in Chua’s system (Eqs. (16) through (19)). The transition matrix for region D0 is
+   M0 = ( -αm0  α  0 ; 1  -1  1 ; 0  -β  0 )  (22)
+   The transition matrix for region D1 is
+   M1 = ( -αm1  α  0 ; 1  -1  1 ; 0  -β  0 )  (23)
+   The eigenvalues for Eqs. (22) are defined as γ̃0, σ̃0 ± ω̃0 and for (23) are defined as γ̃1, σ̃1 ± ω̃1.

+   (2) Define necessary normalized eigenvalues (Eqs. (2.9) and (2.12), p. 1076 [4]) and strategic points (Eqs. (2.20) through (2.33), pp. 1077–1078 [4]).
+   σ0,1 = σ̃0,1 / ω̃0,1    γ0,1 = γ̃0,1 / ω̃0,1   (24)
+   k0 = -γ̃0 / γ̃1    k1 = -γ̃1 / γ̃0
+   p0 = σ0 + k0/γ0 (σ0² + 1)    p1 = σ1 + k1/γ1 (σ1² + 1)   (25)
+   Q0 = (σ0 - γ0)² + 1    Q1 = (σ1 - γ1)² + 1   (26)

+   (3) Compute the following quantities and check if the given conditions are satisfied.
+   a1 = -σ1γ1(p1² + 1) / Q1 > 0   (27)
+   a2 = Q0² + γ0²(1 + p0²(2 + (γ0 - σ0)²)) + 2(γ0 - σ0)² + 2p0(σ0 - γ0)) + Q0γ0(-3γ0 + 3σ0 + p0(2 + p0(σ0 - γ0))) > 0   (28)