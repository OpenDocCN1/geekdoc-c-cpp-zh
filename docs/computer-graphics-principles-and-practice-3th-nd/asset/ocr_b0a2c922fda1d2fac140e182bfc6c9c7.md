Blinn’s actual model was derived from physical considerations motivated by the microfacet models we’ll discuss shortly, and also included a factor for the Fresnel equations, but we’ll omit those details for now.

# 27.5.3.1 Historical Notes

The original Phong model described the reflected light in terms of “intensity,” which was not carefully defined, and included a third term, for reflection of “ambient light,” that is, all the light in the scene that underwent multiple reflections until it was widely diffused. Thus, you’ll sometimes encounter reflection models that use an ambient, a diffuse, and a specular reflection constant, as you saw in Chapter 6.

Phong’s original model also had just one constant for the specular term (which we call the glossy term); this meant that reflectance was independent of wavelength, and a white directional light tended to produce a white highlight, no matter what the material. This wavelength independence is characteristic of many insulators, but does not hold for conductors in general (e.g., look at the reflection of a white light in a gold ring). The specular reflectance was therefore given a wavelength dependence (typically by specifying red, green, and blue reflectance values). The diffuse reflectance was similarly extended to include RGB variation (e.g., a red shirt reflects lots of red light, and little blue or green light). And finally, the intensity of light was known to fall off quadratically as a function of distance from the light source (although this notion was problematic for “directional light sources” that were assumed to be “at infinity”). Thus, for many years the “standard” lighting model looked like

$$I = k_a I_a + f(d)I\left[k_d(-\boldsymbol{\omega}_i \cdot \mathbf{n}) + k_s(\mathbf{n} \cdot \mathbf{h})^{n_s}\right], \qquad (27.20)$$

where the terms labeled $I$ are all “intensities,” the $k$ factors are the constants associated with ambient, diffuse, and specular reflection (we’ve folded the ambient, diffuse, and specular “color” into these for simplicity), $h$ is the average of the vector to the light and the vector to the eye, $n_s$ is the specular exponent, $d$ is the distance from the light to the point $P$, and

$$f(d) = \min\left(1,\frac{1}{a+bd+cd^2}\right) \qquad (27.21)$$

was a “quadratic falloff” term, although in practice $c$ was often set to zero, and there’s no reasonable explanation for the “min” in the expression except that “things got dark too fast otherwise.” When there were multiple light sources, the bracketed term in Equation 27.20 was repeated once per source.

From a modern viewpoint, this entire model, especially the “ambient term,” was a terrible thing: Instead of solving the underlying problem (light transport), you apply a “hack” in a completely different area (scattering at a point). But from the point of view of the engineering of the day, it was a reasonable choice: Doing accurate light-transport computations was clearly beyond the capacity of the computers of the day, while evaluating the more straightforward solution provided by Phong’s model was relatively simple and drastically improved the empirical results. But you should not be fooled into thinking that the model has any physical basis.

There’s also a terminology challenge: The computation of the amount of light reflected from a surface was sometimes called “lighting” or “illumination,”