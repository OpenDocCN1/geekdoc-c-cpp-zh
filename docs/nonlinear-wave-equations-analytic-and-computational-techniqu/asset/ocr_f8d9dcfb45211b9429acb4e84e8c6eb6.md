solves the NV equation with initial data q0. The inverse scattering method may be visualized by the following commutative diagram:

![](bbox=[0.23, 0.22, 0.7, 0.36])

where T and Q stand for the direct and inverse nonlinear Fourier transform, respectively, and the function tτ : C → C is called the scattering transform. In the case E = 0, the inverse scattering method was studied by Boiti et. al. [9], Tsai [89], Nachman [58], Lassas-Mueller-Siltanen [44], Lassas-Mueller-Siltanen-Stahel [45,46], Music [54], Music-Perry [55], and Perry [68]. Recently, Angelopoulos [1] proved that the Novikov-Veselov equation at E = 0 is locally well-posed in the Sobolev spaces H^s(R²) for s > 1/2, placing the local existence theory for this equation on a sound footing. The potential utility of the inverse scattering method is to elucidate global behavior of the solutions.

The case E = 0 is somewhat special and is intimately connected with the following trichotomy of behaviors for the two-dimensional Schrödinger operator L at zero energy.

# DEFINITION 1.1. The operator L = −Δ + q is said to be:

+   (i) subcritical if the operator L has a positive Green's function and the equation Lψ = 0 has a strictly positive distributional solution,
+   (ii) critical if Lψ = 0 has a bounded strictly positive solution but no positive Green's function, and
+   (iii) supercritical otherwise.

This distinction first arose in the study of Schrödinger semigroups, i.e., the operators e^{−tL} where L = −Δ + q. Simon [79,80] (see also [81]) studied L^p-mapping properties of e^{−tL} and asymptotics of ‖e^{−tL}‖_{p,p'}, where ‖·‖_{p,p} denotes the operator norm as maps from L^p to itself. Simon shows that α_p(q) = lim_{t→∞} t^{−1} ln ‖e^{−tL}‖_{p,p} is independent of p ∈ [1,∞]. In the language of Schrödinger semigroups, a potential q is:

+   (i) subcritical if α_∞((1+ε)q) = 0 for some ε > 0,
+   (ii) critical if α_∞(q) = 0 but α_∞((1+ε)q) > 0 for all ε > 0, and
+   (iii) supercritical if α_∞(q) > 0.

Clearly, a sufficient condition for q to be supercritical is that L have a negative eigenvalue.

In [52], Murata showed that, for two-dimensional Schrödinger operators with potentials q with q(x) uniformly Hölder continuous and q(x) = O(|x|^{−4−ε}) for some ε > 0, the trichotomy of behaviors for Schrödinger semigroups is equivalent to Definition 1.1. Murata further studied the existence and properties of positive solutions of the Schrödinger equation in [52], and showed that for his class of potentials, the trichotomy could be characterized as follows: a potential is