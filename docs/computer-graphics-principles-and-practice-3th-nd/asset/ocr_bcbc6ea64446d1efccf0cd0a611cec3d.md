![](bbox=[0.078, 0.107, 0.663, 0.535])

*Figure 27.9: BSDF (black outer curves) and probability density plots (blue inner curves) for several classes of reflections; for impulse scattering, like mirror reflection, we’ve indicated the impulse direction with a green arrow as in the two right-pointing arrows in (c). For the others, the peaks in probability density and BSDF are offset from one another because of the cosine weighting. (a) A generic reflective material. (b) A purely transmissive material, which is physically unrealistic. (c) A material with mirror and refractive impulses; this is the kind of scattering we expect at an air-to-water interface. (d) Glossy scattering. (e) Lambertian scattering. (f) Retroreflective scattering.*

spectral distribution as the incoming light, while for conductors, certain frequencies of light are preferentially reflected. This is why a polished piece of plastic has white highlights, while a polished piece of gold has gold-colored highlights. We’ll return to this in Section 27.8.3.

The simplest summary representation of the spectral dependence of the reflected light is to just give RGB values, representing the overall reflectance of the material in response to long-, middle-, and short-wave incoming radiation. Thus, the summary computational model becomes

$$L(P,\omega_o,\lambda)=\begin{cases}\rho(\lambda)L(P,-\omega_i,\lambda) & \text{if }\omega_o=\omega_i-2(\omega_i\cdot\mathbf n)\mathbf n\text{ and }\omega_i\cdot\mathbf n>0,\\0 & \text{otherwise,}\end{cases}\tag{27.3}$$

where λ represents the wavelength of the light as usual.

![](bbox=[0.706, 0.562, 0.934, 0.732])

*Figure 27.10: A mirrored plane, reflecting a light source above the plane (black solid line), produces the same outgoing radiance field (pink) as a “virtual” source below the plane placed at the proper location behind the mirror would produce (dashed green) in the absence of the mirror.*