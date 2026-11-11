Actually *using* the Schlick approximation requires that you know \(R_F(0)\). But the original Fresnel equations (for dielectrics) give you this value:

\(R_F(0)=\left(\frac{n-1}{n+1}\right)^2\), where \(n=\frac{n_2}{n_1}\). (27.32) (27.33)

**Inline Exercise 27.5:** Verify this formula.

In graphics, most objects sit in air, so \(n_1=1\), and the formula is slightly simpler: You just replace \(n\) with \(n_2\).

**Inline Exercise 27.6:** Show that in the case of conductors, the correct form is \(R_F(0)=\frac{\kappa^2+(n-1)^2}{\kappa^2+(n+1)^2}\), (27.34) using the approximation of the Fresnel reflectance for conductors.

We sometimes want to render things like an underwater view of the surface of a swimming pool. In this case, the light rays are traveling in a medium of large refractive index, and the “other” side is air, which has lower refractive index. Of course, Fresnel’s equations still hold, as does the Schlick approximation, but to make it work you must use \(\theta_t\), the angle of the transmitted ray (the one in the air, not the water) as the argument. The result is that the Fresnel reflectance approaches 1.0 as \(\theta_i\) approaches the critical angle, which is generally much less than 90°. (For angles greater than the critical angle, \(R_F\) remains at 1.0.)

**Inline Exercise 27.7:** If you have looked up at the pool’s surface while swimming, explain the appearance of the surface from below, and the difference in its appearance from above, by considering the Fresnel reflectance and the critical angle for total internal reflection.

# 27.8.2 The Torrance-Sparrow Model

The Phong model predicts that a surface illuminated in direction \(\omega_i\) will reflect light in all directions, with a peak in the mirror-reflection direction \(\omega_r\). In actual observations of nonmirror materials, that’s not the peak direction. Torrance and Sparrow provided a model to explain this off-mirror peak: They imagined that the surface was made up of *microfacets*, each of which was a tiny mirror reflector, but with random orientations. The microfacets were assumed to pair up to form “V” shapes, with identical slopes of each side of the “V” so that an edge-on slice of the material appeared as a collection of grooves of varying depth, all with their tops at the same height, as in Figure 27.13.

Note that we are implicitly assuming that the BRDF we’re estimating is for a measurement area that’s substantially larger than the size of a single microfacet, or the analysis, which is based on average microfacets, is no longer reasonable.

![](bbox=[0.699, 0.689, 0.934, 0.792])

*Figure 27.13:* The symmetric grooves all have their tops at the same height. Light arriving at an angle (downward-pointing black arrows) can be reflected in the mirror direction (the dashed green arrow), or reflect back toward the source or in other directions (red).