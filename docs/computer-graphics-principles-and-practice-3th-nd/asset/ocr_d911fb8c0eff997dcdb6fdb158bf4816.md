n = [0 1 0]^T, we’ll simply write S₂⁺ or S₂⁻. Indeed, our diagrams will always show a flat surface facing up, and we’ll sometimes refer to the “upper” and “lower” hemispheres. We’ll consider light arriving from some direction ωᵢ ∈ S₂⁺ (i.e., traveling in direction −ωᵢ), and consider the scattered light from the surface, using ωₒ to denote a generic direction of scattered light. We’ll use fₛ(ωᵢ, ωₒ) to denote the BSDF for light arriving in direction ωᵢ and leaving in direction ωₒ. (In the case of transmission, we’ll denote the transmitted light direction ωₜ.)

> While the formulation given here—an object that lies in the y ≤ 0 half-space, scattering light upward—is nice and simple, it’s an approximation of a larger truth, which we’ll return to in Section 29.4, namely, that we have a surface that’s a boundary between two materials. For a glass marble, there’s an outward-pointing normal vector that points into the surrounding air, but for the mass of surrounding air, the outward normal points into the glass! We tend to think of air as “nothing” in graphics, but in a situation like a glass filled with wine, the boundary between the glass and the wine serves to delimit both the glass and the wine. Surface scattering is really a property of a pair of media rather than a single medium.

![](bbox=[0.706, 0.297, 0.935, 0.477])

Before we describe the kinds of scattering, we caution that some terms are used very informally. For example, “diffuse” can be used to mean “anything except mirror reflection” or “very similar to Lambertian.”

Here is a collection of terms used for scattering, with figures showing some of them.

+   - **Reflective (Figure 27.2):** The scattered light is all in the upper hemisphere, that is, ωₒ · n ≥ 0. More precisely, fₛ(ωᵢ, ωₒ) = 0 for ωₒ ∉ S₂⁺.
+   - **Transmissive (Figure 27.3):** The scattered light is all in the lower hemisphere, that is, ωₒ · n ≤ 0. More precisely, fₛ(ωᵢ, ωₒ) = 0 for ωₒ ∉ S₂⁻.
+   - **Mirror (Figure 27.4; “specular” is a synonym):** The scattered light is all in a single direction, the mirror-reflection direction ωᵣ = 2(ωᵢ · n)n − ωᵢ. The “function” fₛ has an infinity: fₛ(ωᵢ, ωₒ) = ∞. More precisely, trying to measure the reflectance in the usual way fails, because the outgoing radiance is independent of the solid angle subtended by the light source; this means that our usual BSDF approach is inappropriate for handling mirror-reflected light. Practically speaking, this means that in the programs you write, you need to handle mirrors as a special case.
+   - **Impulse:** The scattered light is all in a single direction, but this direction is not necessarily the direction of mirror reflection. For example, we may want to model a camera lens as purely transmissive, with all

![](bbox=[0.706, 0.529, 0.935, 0.697])

![](bbox=[0.706, 0.757, 0.935, 0.923])

¹ In truth, this is a case where the notion of “distribution” applies: What we tend to write as integrals involving the BSDF typically have the form ∫ fₛ Lᵢ dωᵢ, where L is some representation of radiance and g represents other terms like change of variables Jacobians, etc.; such integrals transform the radiance field L into either a number or another function, and they do so linearly. Thus, “integrating against the BSDF” is just a way to write a linear function from one function space to another. A few such linear maps cannot be written this way, just like the “delta functions” of Chapter 18, but in the quest for consistent notation, researchers in graphics pretend that they can and claim the BSDF “is infinite” at certain points of its domain.