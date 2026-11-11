The condition that no more energy leave the surface than arrives there is called **energy conservation** (with the assumption that unscattered energy is “conserved” by appearing as heat). Not every scattering model is energy-conservative. Phong’s original model had no physical units attached, so it was impossible to tell whether it was conservative or not! In general, conservation can be expressed as a constraint on the integral of the BSDF; we’ll see this worked out in detail for Lambertian scattering.

The other commonly used constraint on scattering is **reciprocity**: If (ωᵢ, ωₒ) ↦ fᵣ(ωᵢ, ωₒ) is the BRDF for some material, then fᵣ(ωᵢ, ωₒ) = fᵣ(ωₒ, ωᵢ). Veach [Vea97] generalizes this to include transmission: For light arriving from direction ωᵢ in a medium of refractive index nᵢ, and scattering in direction ωₒ in a medium of index nₒ,

\[
\frac{f_s(\omega_i,\omega_o)}{n_o^2} = \frac{f_s(\omega_o,\omega_i)}{n_i^2}. \tag{27.1}
\]

Note that when this is applied to reflection, the two refractive indices are identical, and the equation simplifies to the usual symmetry law.

> It’s well known in graphics that the BRDF is symmetric, that is, fₛ(ωᵢ, ωₒ) = fₛ(ωₒ, ωᵢ), and this equality is usually attributed to Helmholtz. Veach describes a proof of symmetry, and explains why Helmholtz’s remarks, which involve mirror reflectors and lenses, are insufficient to imply reciprocity and why several other purported proofs have flaws in them. Despite this, the reciprocity property is still widely known as “Helmholtz reciprocity.”
> 
> Despite Veach’s proof of reciprocity, there are materials such as pearlescent paints for which reciprocity apparently does not hold [CPMV⁺09]. Such materials do not contradict the proof, which assumes that the materials involved in the scattering are homogeneous.
> 
> So is the BRDF symmetric or not? For a very wide range of measured materials, the answer appears to be “yes, for almost all practical purposes.” Snyder [SWL98] explains this in some detail.

# 27.4  Kinds of Scattering

Looking at the differences among solid materials, one of the first things that attracts our attention is the range of shininess, from the matte appearance of chalk to the very shiny appearance of a polished metal surface. Another is that some surfaces are transparent while others are reflective. As we already saw in Chapter 26, these differences are in part due to fundamental physical processes and structures: Conductive materials, with lots of free electrons, tend to be reflective; those whose electron orbital energy levels lack “gaps” corresponding to the energies of quanta of visible light tend to be transparent, etc. But at a higher level, it’s useful to have a language for describing kinds of scattering: reflective, transmissive, mirror, impulse, glossy, diffuse, Lambertian, retroreflective, refractive. To give these meaning, we’ll consider a flat surface (see Figure 27.1) with outward normal vector **n** (i.e., **n** points from the material toward empty space) and the hemispheres S²₊(**n**) and S²₋(**n**), where S²₊(**n**) is the set of all unit vectors **ω** with **ω** · **n** ≥ 0, and S²₋(**n**) is the set of all those for which the dot product is non-positive. Since we’ll mostly be considering a single surface with a fixed normal

![](bbox=[0.787, 0.673, 0.936, 0.818])

*Figure 27.1: We’ll consider a surface (shown shaded) with normal vector **n**; S²₊ consists of all vectors pointing away from the surface, while S²₋ consists of vectors pointing into the surface. Light arrives from a source that’s in either direction ωᵢ ∈ S²₊, and scatters in directions ωₒ, which may be in either S²₋ or S²₊.*