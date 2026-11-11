Most of this is a straightforward simulation of the process of light bouncing around in a scene. If, for a moment, we ignore wavelength dependence, then the absorption step can be explained, just as we saw in path tracing, as follows: When a photon hits a surface that scatters 30% of the arriving light, we could produce a scattered photon with its power multiplied by a factor of 0.3, or we could produce a scattered photon will full power, but only 30% of the time, an approach called **Russian roulette**. Over the long term, as many photons arrive at this point and get scattered, the total outgoing power is the same, but there’s an important difference between the two strategies: In the second, at least for a scene that is not dependent on wavelength, the power of a photon never changes. This means that all samples stored in the photon map have the same power. This makes the radiance-estimation step work better in general, although the statistical reasons for that are beyond the scope of this book. The code, in saying “reflect a full-strength photon with a probability determined by the scattering probability,” is applying Russian roulette.

Because the scattering is wavelength-dependent, the final update to Φᵢ(λ) scales the power in each band in proportion to that band’s scattering probability. Notice that if the surface is white (i.e., reflectance is the same across all bands), then Φ(λ) is unchanged. By contrast, if we’re using RGB and the surface is pure red, then the average scattering probability is 1/3; the red component of the photon power is multiplied by 1/⅓ = 3, while the green and blue components are set to zero.

**Inline Exercise 31.12:** What happens to the power of a photon if the surface is a uniform 30% gray, so it reflects 30% of the light at each wavelength?

The actual implementation of light emission and of scattering (particularly for reflectance models that have a diffuse, a glossy, and a specular part, for instance) requires some care; we discuss these in Chapter 32.

The second part of photon mapping is radiance estimation at points visible from the eye, determined, for instance, by tracing rays from the eye E into the scene. Before performing any radiance estimation, however, we balance the k-d tree. Then for each visible point P, with normal n, we let ωₒ = S(E − P), and compute the radiance.

+   1. Set L = 0 W/m²sr. L represents the radiance scattered toward the eye.
+   2. Find the K photons nearest to P in the photon map, by searching for a radius r within which there are K photons.
+   3. For each photon ph = (Q, ωᵢ, Φᵢ), update L using

L ← L + fₛ(P, ωᵢ, ωₒ) Φᵢ κ(Q − P),  (31.100)

where κ(Q − P) = 1/(πr²) is called the **estimator kernel**. This assignment is wavelength-dependent (i.e., if we use three different wavelength bands, Equation 31.100 represents three assignments, one for each of R, G, and B).

It’s easy to see that this computation is an approximation of the integral ∫ fₛ(P, ωᵢ, ωₒ) · n dωᵢ over the positive hemisphere at P: The arriving radiance at nearby points is used as a proxy for the arriving radiance at P in the integral. Of course, light arriving at some point Q that’s near P from direction ωᵢ may have originated at a fairly nearby light source. If so, then the arriving direction at Q will be different from that at P (see Figure 31.28).