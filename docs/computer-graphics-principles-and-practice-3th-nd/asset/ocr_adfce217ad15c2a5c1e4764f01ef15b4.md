![](bbox=[0.157, 0.107, 0.581, 0.293])

*Figure 27.15: A single vase, illuminated by two lights, made of 12 different materials whose reflectance properties were determined with the Cook-Torrance model. (Courtesy of Robert Cook, ©1981 ACM, Inc. Reprinted by permission.)*

surface roughness means that even when we are looking near a silhouette, some parts of the surface are facing back toward us, and thus reflect more light than might be expected (see Figure 27.16). In particular, they apply essentially the Torrance-Sparrow-Cook idea of microfacet, but in a situation where they assume that each microfacet acts like a Lambertian reflector rather than a mirror.

![](bbox=[0.707, 0.257, 0.931, 0.371])

*Figure 27.16: (Top) Near the edge of a smooth diffuse surface, very little light would be scattered back toward the viewer because the off-normal incidence of the light makes the irradiance small. (Bottom) If a small piece of surface near the silhouette is oriented more perpendicular to the incident light direction, this surface piece will scatter much more light in all directions, including the direction back toward the viewer.*

Furthermore, they consider not only single-bounce interactions of illumination with microfacets, but multiple inter-reflections, observing that for a quite rough surface, illuminated at a nearly grazing angle and viewed from the opposite side from the illumination, each lighted facet is invisible to the viewer, but the facets that are not directly lit may nonetheless be visible. If you look east toward a mountain range at dawn, you cannot see the sunlight on the east sides of each mountain, but the west side of some mountains will be illuminated by light reflected from the east side of more westerly mountains (see Figure 27.17).

The expression for the radiance (assuming a Gaussian distribution of facet slopes) from a facet is a rather messy integral. Oren and Nayar evaluated this integral for many different directions of arriving light, viewer direction, and Gaussian shape parameters, and developed a much simplified form that's suitable for more rapid computation of approximately correct values. The result is given in terms of θ_i, the angle between ω_i and n, θ_o, the angle between ω_o and n, and φ, the difference in azimuth between the incoming and outgoing light. If light arrives from the west and leaves to the east, then φ = 0; if it leaves to the northeast, then φ = 45°; if it leaves to the southeast, then φ = −45°, etc. The model has two parameters: the slope-distribution constant σ, where the probability of a facet at angle θ is proportional to exp(−θ²/(2σ²)), and the albedo, ρ, of the surface (which may be a function of wavelength).

The full-generality result is seldom used; instead, the simplified version, which accounts for only single scattering, is

L_r(θ_i, θ_o, φ; σ) = (ρ/π) E_0 cos(θ_i)(A + B max(0, cos(φ)) sin α tan β), where (27.40)

![](bbox=[0.707, 0.617, 0.935, 0.786])

*Figure 27.17: The west sides of mountains illuminated by the rising sun will be in shadow, but may be lit by light reflected from the east sides.*