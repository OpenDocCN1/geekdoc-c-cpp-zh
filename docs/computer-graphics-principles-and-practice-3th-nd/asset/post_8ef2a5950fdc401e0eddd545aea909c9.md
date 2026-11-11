
is used to smooth out automotive finishes and to polish sharp knives. Thus, materials whose roughness is between that of a highly polished metal and a piece of newsprint are likely to contain scratches that are on the scale of a few wavelengths of light. Despite this, the geometric optics approach seems to make good predictions in practice at this scale. We’ll describe the main ideas of the geometric optics approach in the next several sections.

We do so with a caution, however: Given the scale disagreements (facets must be large compared to the wavelength of light, but in practice are quite close to it), these models are at best weak approximations of the underlying phenomena. Recent careful measurement work has shown the weakness of the approximations [Lei10].

## 27.8 Physically Based Scattering Models

The underlying physics of reflection from a flat surface depend on the electrical properties of the atomic structure of the material, some of which we described in Chapter 26. In particular, metals, which tend to make the best mirror reflectors, have many free electrons that float about the surface, creating an almost perfectly planar sheet of constant electrical potential with which the electromagnetic light-wave interacts. The Fresnel equations determine the degree of reflection for light of varying polarizations; in graphics, we typically assume unpolarized light, and thus average the perpendicular and parallel terms of the Fresnel equations. We’ll review these equations, and describe how they’re applied in practice, since they are part of all the physically based scattering models.

As we said, the assumption, in the physical computations that support these reflectance models, is that the reflecting surface is large compared to the wavelength of the arriving light, or else diffraction will start to dominate. The mirror-plane model can also be used to compute the reflection from a mirror surface that’s nonplanar, provided that its curvature is not too great; to compute the reflection at a point Q, we use the normal vector n(Q) to compute the mirror direction just as before. If the curvature is too large (i.e., if the normal vector changes too fast), then again the “sheet of constant potential” model fails, and diffraction starts to dominate. A radius of curvature (in any surface direction) that’s near or lower than the wavelength indicates a place where the mirror model is no longer appropriate. It’s worth noting that in polygonal models, the curvature at every point of every edge is infinite. This is typically ignored in ray tracers, where a ray hits either one facet or the other, and proximity of the ray to an edge is ignored. If the ray actually hits an edge precisely, it may be ignored or treated as lying on one of the two adjacent surfaces. The results look correct enough that they have not generally been a point of concern.

### 27.8.1 The Fresnel Equations, Revisited

In Chapter 26, we saw that at a surface between dielectric materials such as water and air, or glass and air, the amount of light reflected and transmitted depended strongly on the angle of the arriving light. Under the assumption that the arriving light was unpolarized, the fraction of light energy reflected is a function of the refractive indices of the two materials and the incident angle θᵢ = cos⁻¹(ωᵢ · n), and the angle of the transmitted ray is θₜ. The Fresnel reflectance R_F is the average of the parallel- and perpendicular-polarized terms, $R_s$ and $R_p$, which are given by

$$r_p = \frac{n_2\cos\theta_i - n_1\cos\theta_t}{n_2\cos\theta_i + n_1\cos\theta_t} \tag{27.26}$$
$$R_p = r_p^2 \tag{27.27}$$
$$r_s = \frac{n_1\cos\theta_i - n_2\cos\theta_t}{n_1\cos\theta_i + n_2\cos\theta_t} \tag{27.28}$$
$$R_s = r_s^2 \tag{27.29}$$

Recall that $\theta_i$ and $\theta_t$ are related by Snell's law:

$$\sin(\theta_i) = \frac{n_1}{n_2}\sin(\theta_t). \tag{27.30}$$

For an air-water interface, we have $n_1$, the refractive index of air, is approximately 1.0, while that of water is approximately 1.33. The plot of $R_F$ as a function of $\theta_i$ is shown in Figure 27.12.

![](img/f464cd0043eb5336aa0543fe20a0561b_778_0.png)

*Figure 27.12: The Fresnel reflectance $R_F$ as a function of $\theta_i$, for an air-to-water interface*

As you'll observe, the function is nearly constant until we approach grazing, at which point it rises rapidly. If you plot $R_F$ for some other ratios of refractive indices (see Exercise 27.5), you'll see that this characterization is quite general: nearly constant for small angles, a sudden rise near grazing angles.

For metallic surfaces, the formula for $R_F$ is somewhat more complex, but it exhibits the same general characteristics.

Schlick [SCH94] observed that for metallic surfaces $R_F$ could be well approximated by a simple expression, and others have observed that the approximation works reasonably well even for nonmetallic materials. The approximation is

$$R_F(\theta_i) = R_F(0) + (1 - R_F(0))(1 - \cos\theta_i)^5, \tag{27.31}$$

where $R_F(0)$ is the reflection at normal incidence ($\theta_i = 0$) and $\theta_i = \cos^{-1}(\omega_i \cdot \mathbf{n})$ is the angle of incidence. When the cosine is 1, we get $R_F(0)$; when the cosine is 0, we get 1.0.

> **Inline Exercise 27.4:** There's usually no reason to compute $\theta$ explicitly, since many formulas involve the cosine or sine of $\theta$ rather than $\theta$ itself. Rewrite Schlick's approximation in terms of $\omega_i$ and $\mathbf{n}$ rather than $\theta$.

For insulators, $R_F(0)$ tends to be small, so there's large variation in $R_F$ with angle $\theta_i$, leading to a pronounced Fresnel effect. For conductors, $R_F(0)$ tends to be large (typically greater than 0.5), so the Fresnel effect is less pronounced.

Note that the index of refraction and the coefficient of extinction depend on wavelength (although they have not been tabulated for many materials, which is a problem); this means that the Fresnel reflectance is also a function of wavelength. For many metals, this dependence is considerable. For gold, for instance, the extinction coefficient drops substantially above about 500 nm, while the index of refraction rises steadily above about 500 nm, which together give gold its characteristic yellow appearance. For insulators, the refractive index is nearly constant with respect to frequency, causing highlights on insulators to be the color of the incoming light.

Actually *using* the Schlick approximation requires that you know \(R_F(0)\). But the original Fresnel equations (for dielectrics) give you this value:

\(R_F(0)=\left(\frac{n-1}{n+1}\right)^2\), where \(n=\frac{n_2}{n_1}\). (27.32) (27.33)

**Inline Exercise 27.5:** Verify this formula.

In graphics, most objects sit in air, so \(n_1=1\), and the formula is slightly simpler: You just replace \(n\) with \(n_2\).

**Inline Exercise 27.6:** Show that in the case of conductors, the correct form is \(R_F(0)=\frac{\kappa^2+(n-1)^2}{\kappa^2+(n+1)^2}\), (27.34) using the approximation of the Fresnel reflectance for conductors.

We sometimes want to render things like an underwater view of the surface of a swimming pool. In this case, the light rays are traveling in a medium of large refractive index, and the “other” side is air, which has lower refractive index. Of course, Fresnel’s equations still hold, as does the Schlick approximation, but to make it work you must use \(\theta_t\), the angle of the transmitted ray (the one in the air, not the water) as the argument. The result is that the Fresnel reflectance approaches 1.0 as \(\theta_i\) approaches the critical angle, which is generally much less than 90°. (For angles greater than the critical angle, \(R_F\) remains at 1.0.)

**Inline Exercise 27.7:** If you have looked up at the pool’s surface while swimming, explain the appearance of the surface from below, and the difference in its appearance from above, by considering the Fresnel reflectance and the critical angle for total internal reflection.

### 27.8.2 The Torrance-Sparrow Model

The Phong model predicts that a surface illuminated in direction \(\omega_i\) will reflect light in all directions, with a peak in the mirror-reflection direction \(\omega_r\). In actual observations of nonmirror materials, that’s not the peak direction. Torrance and Sparrow provided a model to explain this off-mirror peak: They imagined that the surface was made up of *microfacets*, each of which was a tiny mirror reflector, but with random orientations. The microfacets were assumed to pair up to form “V” shapes, with identical slopes of each side of the “V” so that an edge-on slice of the material appeared as a collection of grooves of varying depth, all with their tops at the same height, as in Figure 27.13.

Note that we are implicitly assuming that the BRDF we’re estimating is for a measurement area that’s substantially larger than the size of a single microfacet, or the analysis, which is based on average microfacets, is no longer reasonable.

![](img/f464cd0043eb5336aa0543fe20a0561b_779_0.png)

*Figure 27.13: The symmetric grooves all have their tops at the same height. Light arriving at an angle (downward-pointing black arrows) can be reflected in the mirror direction (the dashed green arrow), or reflect back toward the source or in other directions (red).*
