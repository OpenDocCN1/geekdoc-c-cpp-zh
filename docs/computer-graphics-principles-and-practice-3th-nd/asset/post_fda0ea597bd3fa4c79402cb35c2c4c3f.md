

$\{\omega_k : k = 1, \ldots, n\},$

$f_s(\mathbf{P}, \omega_i, \omega_o) = \frac{\rho_d}{\pi} + \sum_{k=1}^{n}(\omega_o \cdot \omega_k)^{e_k},$  (27.23)

where $\rho_d$ is the diffuse reflectivity. For this to be reciprocal requires that the vectors $\omega_k$ be expressed as term-by-term multiples of $\omega_i$ so that $\omega_1$, for instance, is

$\omega_1 = (\omega_{i,x}a_{1,x}, \omega_{i,y}a_{1,y}, \omega_{i,z}a_{1,z}).$  (27.24)

Alternatively, one can express this by building a diagonal matrix $\mathbf{A}_1$, and then saying that $\omega_1 = \mathbf{A}_1(\omega_i)$. Then the Lafortune model ends up being

$f_s(\mathbf{P}, \omega_i, \omega_o) = \frac{\rho_d}{\pi} + \sum_{k=1}^{n}(\omega_o^T\mathbf{A}_k\omega_i)^{e_k},$  (27.25)

where the fact that the matrices $\mathbf{A}_k$ are all diagonal guarantees that the BRDF is reciprocal.

> **Inline Exercise 27.3:** Quickly verify the preceding claim. Now suppose that $\mathbf{A}_1$, instead of being diagonal, represents rotation through $90^\circ$ about the $z$-axis. Show that the resultant BRDF is *not* reciprocal. Conclude that the Lafortune BRDF is reciprocal if and only if all the matrices $\mathbf{A}_k$ are symmetric.

In practice, since the Lafortune model only uses diagonal matrices, it makes much more sense to just store the three diagonal entries than the whole matrix, and to treat the matrix-vector multiplication as a term-by-term multiplication.

The Lafortune model is very general. In fact, it’s possible to approximate almost any conservative, reciprocal function on $S^2 \times S^2$ by using a large enough value of $n$. But to get a good fit may require a very large $n$ indeed.

To add spectral dependence to the BRDF representation, we need to let the diagonal matrices $\mathbf{A}_k$ (or their three diagonal entries) be functions of wavelength; this is typically done with RGB values.

The Lafortune model is a hybrid. It’s based on a phenomenological model (Phong), but it is motivated by a rather different kind of phenomenon: the appearance of measured BRDFs! In some sense, the Lafortune model can be seen not as a model of light scattering, but as a model of a class of functions, with the property that observed BRDFs tend to be representable with relatively few coefficients, and hence be amenable to rapid evaluation.

### 27.5.5  Sampling

We’ve described the BRDF for the mirror and Lambertian and Blinn-Phong models in a form where, given $\omega_i$ and $\omega_o$, you could easily compute $f_s(\omega_i, \omega_o)$. But in ray tracing/path tracing and photon mapping, which we’ll describe in more detail in Chapters 31 and 32, there are two other computations we need to perform.

For photon mapping, we’re given $\omega_i$ and we need to randomly select a vector $\omega_o$ with probability density proportional to $f_s(\omega_i, \omega_o)(\omega_o \cdot \mathbf{n})$. (Probability densities are described in detail in Chapter 30; for now it’s sufficient to think, “We want to pick a vector $\omega_o$ more often if $f_s(\omega_i, \omega_o)(\omega_o \cdot \mathbf{n})$ is large, and less often if it’s small.”)

For mirror reflection, this is easy: We always return ωᵣ, the mirror-reflected version of ωᵢ. For Lambertian scattering, we need to pick a direction on the hemisphere, favoring the North Pole, and fading off in probability as we approach the equator. Fortunately, using the Average Height principle, it’s not too difficult to do this. Section 30.3.8 gives the details.

For Blinn-Phong scattering, things are not so simple. Although it’s possible to sample directly from the BRDF by doing some careful computations, that’s only because of the nice power-of-a-cosine form; by the time other factors, like the Fresnel term, get included such direction sampling is no longer possible. Far better is to use an approach like that of Lawrence [Law04], which approximates the BRDF with terms that are amenable to efficient sampling.

For ray tracing/path tracing, we have a similar problem, except that we’re given ωₒ and want to select ωᵢ with density proportional to fₛ(ωᵢ, ωₒ). And for direct computation of the reflectance integral, we may want to sample in proportion to fₛ(ωᵢ, ωₒ)(ωᵢ · n).

The same arguments apply in these cases, except that in the Lambertian case for the ray tracing/path tracing computation, instead of using the cosine-weighted BRDF, we just need to sample in proportion to the BRDF, which is constant. In other words, we just need to pick points uniformly on the hemisphere, which is easy with the cylinder-sphere projection theorem.

## 27.6  Measured Models

Phenomenological models tend to approximate well those things that we, as humans, recognize as “phenomena.” But it’s possible that other aspects of scattering, when combined with light transport, produce other “phenomena” as well, and if we suppress those aspects, these secondary phenomena will never be simulated. The only way to know is to have a ground-truth representation of the scattering, and compare results of simulations that use this ground truth to those that use either phenomenological or physically based approximations to it, and see whether the results differ significantly.

One such ground-truth representation is provided by the full BRDF measurements made by Matusik et al. [MPBM03] of about one hundred isotropic materials. For an isotropic material, the BRDF, represented in polar coordinates, depends only on the difference between the longitude coordinates of ωᵢ and ωₒ, so the data can be tabulated in a three-index table (two latitudes, one longitude difference). Tabulated at approximately one sample per degree, these tables have many entries (90 × 90 × 180), each of which is an RGB triple. (The sampling near glossy highlights is deliberately somewhat denser so that very shiny materials can be accurately represented.)

Others have measured various anisotropic materials [War92], texture characteristics of surfaces [DvGNK99], and more complex data like subsurface scattering distribution [JMLH01], and have developed image-based approaches to measuring BRDFs without the high cost of a gonioreflectometer [MLW+99].

One value of these measurements is that they can be used to compare the expressive power of various BRDF models: if optimally adjusting all the parameters of the Blinn-Phong model, for instance, only allowed you to get within 5% of the measured values, and that only for, say, 90% of all possible (ωᵢ, ωₒ) pairs, you might conclude that the Blinn-Phong model was not sufficiently rich to represent real materials decently. Matusik in fact took this approach in comparing two BRDF models, the first due to Ward [War92] and the second to Lafortune [LFTG97]; he found that the Lafortune model was better able to fit the data in many cases, but even so, there were cases for which the average error was as large as 20%, where the difference was measured as a difference of logarithms, to discount somewhat the overwhelming effect of glossy peaks in the BRDF.

One drawback to using measured BRDFs in rendering is the cost of performing effective sampling. While Matusik describes techniques for this, they require a large amount of extra precomputed data and are still slow compared to those few models for which explicit sampling techniques are known.

There are some limits to using measured BRDFs. We can only render images of scenes for which we know the BRDFs of all materials, and measuring the BRDF of a material is nontrivial; gathering observations at grazing angles is particularly challenging. And we can only gather the BRDF of a material that already exists. We can’t create new BRDFs by adjusting parameters, as we can do with the various physically based models described below. Finally, there’s the problem that the gathered data may well contain errors, errors that can make the observed BRDF turn out to be physically unrealistic. Matusik handles this in part by projecting every measured BRDF onto the reciprocal-BRDF subspace, by replacing $f_s(\omega_i,\omega_o)$ with the average of $f_s(\omega_i,\omega_o)$ and $f_s(\omega_o,\omega_i)$, thus ensuring reciprocity, and by discarding certain outlying measurements.

## 27.7  Physical Models for Specular and Diffuse Reflection

We now turn to physically based models of reflective scattering. There is a choice to be made in attempting to explain scattering phenomena: Should we use **physical optics**, based on the wave theory of light, in conjunction with a geometric model, to determine the scattering, or **geometric optics**, in which the reflection of light by surfaces is determined entirely by a billiard-ball-bounce model, in which the arriving light reflects from the surface in the mirror direction? At first glance, the geometric optics approach seems destined for failure; after all, not every surface is mirrorlike. This can, however, be addressed by examining the interaction of light with a *rough* surface, in which the reflection is mirrorlike, but the geometry is extremely complex, consisting of many tiny reflecting facets oriented in many possible directions. Since the roughness can be described probabilistically, this approach is actually feasible. In contrast, the physical optics approach presents enormous computational challenges, in the sense that to apply it, we must apply Maxwell’s equations to relatively complex situations, where any hope of an easily expressed formula is lost; our best hope is for rapid numerical solutions of the equations. We’ll return to this after examining the geometric optics approaches.

Geometric optics is really only appropriate when the small reflecting parts of the surface are large compared to the wavelength of the incident light. Since the incident light that interests us is in the visible range, we can say that the wavelength is about 0.5 to 1.0 microns; this means that the microfacets must be at the very least 1 micron in size. When you recall that a human hair is on the order of 15 microns in diameter, and that it’s easy to feel a single hair on a flat surface, you realize that the geometric optics assumption for ordinary materials is just barely reasonable: 15 micron sandpaper feels about like newsprint; 2 micron sandpaper

