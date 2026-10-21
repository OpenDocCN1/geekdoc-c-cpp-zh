models EM waves in a manner related to those derived for the dNV equation, and whether either NV or dNV serves as a physical model for any kind of hydrodynamic phenomenon.

# 6.2. Exceptional Sets and Large-Time Behavior for the NV Equation.

Recall that the exceptional set of a potential q0 is the set of all those k ∈ ℂ for which there is not a unique NCGO solution μ(z,k). Here we discuss the relationship between: (1) the “size” of the exceptional set,” (2) whether the potential q0 is subcritical, critical, or supercritical (recall this trichotomy, Definition 1.1 from the introduction) and (3) whether the NV equation with initial data q0 has a global solution. In these remarks, we will usually restriction attention to real-valued potentials q0 belonging to the space Lpρ(ℝ²) for ρ > 1 and p ∈ (1,2) (see the remarks preceding Definition 1.3); one may think of potentials of order O(|z|⁻²⁻ᵉ) as |z| → ∞. Recall that, in the inverse scattering literature, critical potentials are usually referred to as “potentials of conductivity type.”

To date, the only rigorous results on the size of exceptional sets for the zero-energy NV equation are due to Nachman [58] and Music [54]. As explained above, Nachman showed that a potential is of conductivity type (or, equivalently, a critical potential as defined in the introduction, Definition 1.1) if and only if the exceptional set is empty and the scattering transform t(k) is O(|k|ᵉ) as |k| → 0 for some ε > 0. Music, extending Nachman’s ideas and techniques, showed that a subcritical potential with sufficient decay at infinity has an empty exceptional set and characterized the singularity of the potential as |k| → 0. Perry [67] showed that, if q0 is a sufficiently smooth critical potential, the NV equation with initial data q0 has a solution global in time. There is strong evidence to suggest that a similar result can be proved for the NV equation with subcritical initial data, based on the work of Music [54].

Thus, it remains to understand the singularities of the scattering transform for supercritical potentials. Examples due to Grinevich and Novikov [30] and Music, Perry and Siltanen [56] show that supercritical potentials may have circles of exceptional points. It is not known whether supercritical potentials must or may have exceptional points, nor is it known how to extend the inverse scattering formalism to potentials with nonempty exceptional sets. The following result due to Brown, Music, and Perry [10] gives an initial constraint on the size of exceptional sets for particularly nice potentials.

THEOREM 6.1. [10] Suppose that q is a real-valued measurable valued function with the property that |q(z)| ≤ C1 exp(−C2|z|) for some constants C1 and C2. Then the exceptional set of q consists at most of isolated points together with at most finitely many smooth curves with at most finitely many intersections.

To analyze the exceptional set, the authors define a renormalized determinant whose zero set is exactly the exceptional set. To describe it, let Tk is the integral operator

```
Tkψ = 1/4 gk * (qψ).
```

The differential equation for μ(z,k), the NCGO solution, may be rewritten μ = 1 + Tkμ. Hence, uniqueness of solutions is equivalent to invertibility of (I − Tk), and the exceptional set is exactly the set of points k for which (I − Tk) fails to be invertible. It can be shown that Tk is a compact linear operator from Lp to itself