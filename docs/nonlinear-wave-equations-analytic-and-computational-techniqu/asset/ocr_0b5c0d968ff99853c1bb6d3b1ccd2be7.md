and h is the both the grid spacing and the perturbation parameter. Then, because

```
(1.4) $$h^{(\frac{1}{N})}=h^{(\frac{h}{L})}\to 1,\quad\text{as}\quad h\to 0,$$
```

the bound provided by the standard Nekhoroshev theorem becomes ineffective in the continuum (PDE) limit. Notwithstanding this complication, there has been some progress in the development of Nekhoroshev-like theorems for infinite-dimensional systems (e.g., [6, 7, 14, 33]. Hence, it would be reasonable to hypothesize Nekhoroshev-like bounds on the orbits of discretizations of KdV.

The supposition that recurrence in the ZK lattice (1.3) is a manifestation of the solitons and/or integrability of KdV leads one naturally to hypothesize that stronger and more-persistent recurrences than described in [36] will occur:

+   H1 as the lattice spacing h approaches zero (with Nh = L fixed), and the lattice converges to KdV;
+   H2 with a higher-accuracy discretization of KdV, such as a spectral or pseudo-spectral discretization;
+   H3 with a discretization that is itself integrable as a system of ODEs.

In this article, we present evidence obtained by numerical simulation that the above hypotheses are false. Consequently, we infer that the underlying structure which leads to recurrence in the lattice is not a result of either the (approximate) existence of solitons nor of integrability more generally.

The original expectation of FPU (that they would observe the equipartition of energy among the modes in nonlinear lattices) is, in some sense, diametrically opposite from the results of their simulations (repeated recurrence of a single-mode state). However, while recurrence precludes equipartition, the absence of recurrence is, by itself, insufficient to imply equipartition. Instead, a system can evolve to a state in which energy is shared unequally between the modes (or a subset of the modes), but there is no recurrence of the single-mode state. Therefore, the question of the mechanism of recurrence is distinct from, though likely related to, the question of equipartition in KdV and FPU lattices.

Following the original work of Zabusky and Kruskal [36], we consider simulations of the ZK lattice (1.3) with the single-mode initial condition (1.2) restricted to an evenly spaced lattice,

```
(1.5) $$u_n(0)=\sin\pi h n,\quad n=0,\dots,N-1,$$
```

where Nh = L = 2. Moreover, following the original simulations, we take δ = .022 in (1.3). In an examination of 1, Section 2 describes the results of simulations of ZK (1.3) with 70 ≤ N ≤ 300. To examine Hypothesis 1 we consider the spectral discretization of (1.1), as described in Section 3. To shed light on the role of integrability in the recurrence (1), we construct a semi-discretization (i.e., a spatial discretization) of KdV which is integrable as a lattice/ODE system (indeed, a family of integrable systems that converges to KdV as the grid-spacing parameter h → 0) in Section 4. For all three spatial discretizations, the time evolution was computed with the variable-step-size "ode5r" routine in the "odepkg" [35] extension of Octave [12]. The ode5r routine of odepkg uses the radau5.f Fortran code [19] to compute the time evolution.