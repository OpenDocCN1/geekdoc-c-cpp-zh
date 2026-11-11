# 27.14 Software Interface to Material Models

For our applications of material modeling to rendering, we’ll restrict our discussion to a particular class of models: those composed of a finite part and an impulse part, which we’ll now characterize.

The “impulse” part of scattering describes phenomena like transmission through boundaries between media, and mirror reflection: Radiance arriving from one single direction generates radiance leaving in a single other direction (or, in the case of simultaneous transmission and reflection, two other directions). These are the phenomena for which the measurement of the BSDF is impossible, as we described in Section 26.10.2. “Impulsive” scattering from **ωᵢ** to **ωₒ** is described by a single factor by which incoming radiance is multiplied to produce outgoing radiance. We’ll assume that for a given direction **ωᵢ** toward a light source, there are finitely many (usually two!) directions **ωₒ** for which (**ωᵢ**, **ωₒ**) is an impulse-scattering pair. For each such pair, we’ll have a constant *m*, the **magnitude** of the impulse, which is the factor by which incoming radiance is multiplied to get outgoing radiance. Similarly, we’ll assume that if we know **ωₒ**, there are only finitely many directions **ωᵢ** such that (**ωᵢ**, **ωₒ**) is an impulse-scattering pair. To simplify things, for the remainder of this section we’ll say that there are exactly *two* impulse directions *ι₁* and *ι₂*, with magnitudes *m₁* and *m₂*.

When we want to ray-trace, it’s essential to recover these impulse directions and the associated material properties; we’ll need

```
`ImpulseArray getImpulsesIn(surface, ωₒ)`
```

where `surface` is a `SurfaceElement` data structure that stores the geometric normal at a point of some surface, the location of that point, the index of refraction of the material on the side pointed to by the normal and on the other side as well, and the shading normal (a vector used in shading computations, often interpolated from geometric normals at nearby points). The array of returned “impulses” contains a list of pairs (ωₒ, ωₒ, *m*) where all the ωₒ values equal the input argument, and *m* is the magnitude of the impulse. It’s also useful to have the dual form

```
`ImpulseArray getImpulsesOut(surface, ωᵢ)`
```

which returns an array of (ωᵢ, ωₒ) pairs, together with their impulse magnitudes.

In fancier versions of ray tracing that can handle area lights and glossy surfaces, it’s also important to be able to evaluate the finite part of the BSDF for any two inputs, that is, we need

```
`float getBSDFFinite(ωᵢ, ωₒ)`
```

It’s also useful to be able to “sample from the BSDF,” that is, to ask, given an output direction ωₒ, for an input direction ωᵢ where the probability density of selecting ωᵢ is proportional to *fₛ*(ωᵢ, ωₒ). For a Lambertian surface, such a procedure would return a direction ωᵢ in the upper hemisphere uniformly at random.

Sampling from the BSDF doesn’t make literal sense if the BSDF contains impulses, for in that case, certain BSDF values are infinite. Suppose, for instance, that we have a material and a direction-to-light ωᵢ in which 40% of the light is mirror-reflected in a direction ι₁, while 60% is Lambertian-scattered. In this case,