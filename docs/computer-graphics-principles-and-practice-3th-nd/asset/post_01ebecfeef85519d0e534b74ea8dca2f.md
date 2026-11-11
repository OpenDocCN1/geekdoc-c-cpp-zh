
up a value at location \((u, v)\) in an image whose domain is parameterized by \(0 \leq u, v \leq 1\)." but there are many other possibilities.

Much of this chapter elaborates on this idea, discussing the parameters that can be varied, the codomains for texture coordinates (i.e., the meaning of the values that they take on), and mechanisms for defining mappings from a mesh to the space of coordinates.

You’ll notice that this entire notion of “texture mapping” is really just a name for *indirection* as applied in a specific context: We use an index (the texture coordinates) to determine a value. This determination may be performed by a table lookup (as in the case of the soft-drink can above, where the texture image serves as the “table”) or by a more complex computation, in which case it’s often called **procedural texturing**.

An example of the power of various mapping operations is given by this book’s cover image, in which almost every object you see has had multiple maps applied to it—color, texture, displacement, etc.—resulting in a visual richness that would be almost impossible to achieve otherwise.

## 20.2 Variations of Texturing

We’ll illustrate several variations on the idea of texture mapping, working with the Phong reflection model as an exemplar. The ideas we present are largely independent of the reflection model, and they apply more generally. Because the unit square \(0 \leq u, v \leq 1\) occurs so often in this chapter, we’ll give it a name, \(U\), which we’ll use in this chapter only.

Recall that in the Phong model of Chapter 6, the light scattered from a surface is defined by various constants (the diffuse reflection coefficient \(k_d\), the specular reflection coefficient \(k_s\), the diffuse and specular colors \(C_d\) and \(C_s\), and the specular exponent \(n\)), dot products of various unit vectors, including the direction vector to the light source, the direction vector from the surface to the eye, the surface normal vector, and finally, the arriving light. There is also, in some versions of the model, an ambient term, modeled by \(k_a\) and \(C_a\), indicating an amount of light emitted by the surface independent of the arriving light. Each of these things—the constants, the vectors, and even the way you compute the dot product—is a candidate for mapping.

### 20.2.1 Environment Mapping

If our surface is mirrorlike (i.e., \(k_d = k_a = 0\), and \(n\) is very large, or even infinite), then the light scattered toward the eye, as determined by the Phong model, is computed by reflecting the eye ray through the surface normal to get a ray that may point toward a light source (in which case light is scattered) or not. If all sources are point sources, this tends to result in no rendered reflection at all, since the probability of a ray hitting any particular source is zero. If the sources are area sources, we see them reflected in our object.

We can replace our model of light arriving at the surface point \(P\) from one based on a few point or area sources to one based on a texture lookup: We can treat the reflected eye vector as a point of the unit sphere, and use it to index into a texture-mapped sphere to look up the arriving light. In practical terms, if we write this eye vector in polar (world) coordinates, \((\theta, \phi)\), for instance, we can use \(u = \frac{\phi}{2\pi}\), \(v = \frac{\theta}{\pi} + \frac{1}{2}\) to index into an **environment map** that contains, at location \((u, v)\), the light arriving from the corresponding direction.

Notice that as the point *P* moves, the light arriving at the point *P* from direction **v** doesn’t change. Thus, this **environment map** is useful for modeling the specular reflection of an object’s surroundings, but it is not good for modeling reflections of nearby objects, where the direction from *P* to some object will change substantially as we vary *P*.

Where do we get an environment map in the first place? A fisheye-lens photograph taken from the center of a scene can provide the necessary input, although the mapping from pixels in the photograph to pixels in the environment map requires careful resampling. In practice, it’s common to use multiple ordinary photographs, and a rather different mapping strategy from the one we’ve suggested here, but the key idea—doing a lighting “lookup” rather than iterating over a small list of point or area lights—remains the same.

Debevec has written an interesting first-person history of reflection mapping in general [Deb06], tracing its first use in graphics to a paper by Blinn and Newell in 1976 [BN76], which is long before digital photographs were available! The “environment map” in this case was a scene created in a drawing program.

**Inline Exercise 20.1:** We’ve carefully suggested using environment mapping in a ray tracer for describing the lighting of a mirrorlike surface. What would be entailed in using environment mapping on a glossy surface? A diffuse one? Would it substantially increase the computation time over that of a simpler model in which the light was specified by a few point and area lights?

### 20.2.2 Bump Mapping

In **bump mapping**, we fiddle with another of the ingredients in the Phong model: the surface normal, **n**. A typical version of this uses texture coordinates on a model to look up a value in a bump map image and uses the resultant values to alter the normal vector a little.

The exact meaning assigned to the RGB values from this image depends on the implementation, but a simple version uses just *R* and *G* to “tilt” the normal vector as follows. We’ll assume that at each surface point *P* we have a pair of unit vectors **t₁** and **t₂** that are tangent to the surface, are mutually perpendicular, and vary continuously across the surface. In theory, it may be impossible to find such a pair of vector fields (see Chapter 25), and in Section 20.3 we’ll discuss this further, but in practice usually only the continuity assumption is violated, and only at a few isolated points. For example, on the unit sphere, tangents to the lines of constant latitude and constant longitude can play the role of **t₁** and **t₂**, failing the continuity requirement only at the north and south poles. If we arrange to not perturb the normal vector at either pole, then the lack of continuity of **t₁** and **t₂** has no effect.

With **t₁** and **t₂** in hand, we’ll show how to adjust the normal vector. The *R* and *G* values from the bump map, typically bytes representing values −128, . . . , 127, or unsigned bytes representing 0 to 255, are adjusted to range from −1 to 1 by writing (in the first case)

$$r = \max\left(\frac{R}{127}, -1.0\right) \tag{20.2}$$

and a corresponding expression for *g*. (The loss of −128 as a distinct value is deliberate. If we’d divided by 128, we could not represent +1.0.)

> **Inline Exercise 20.2:** Write a formula to convert values from 0 to 255 into values from -1 to 1.

We can now adjust the normal vector **n**, as shown in Figure 20.4, by computing

$$n' = \mathcal{S}(n + r t_1 + g t_2). \tag{20.3}$$

At the extreme (when *r* = *g* = 1) this tilts the normal vector by about 54°. If a larger amount of tilt is needed, one can redefine *r* and *g* to range from −2 to 2, or even more.

One advantage to this scheme, originally proposed by Blinn [BN76], is that **n** + *r***t₁** + *g***t₂** can never be zero, because its dot product with **n** is one. This means that it can always be normalized.

By the way, the particular form we've described for converting image-pixel values into values between −1.0 and 1.0 is part of the OpenGL standard and is called the **signed normalized fixed-point 8-bit representation** (see Chapter 14). There are other standard representations as well, using more bits per pixel, unsigned rather than signed values, etc. There's nothing sacred about any of these. They've proven to be convenient over the years, so they become standardized.

A more direct approach is to store in the texture image three floating-point numbers (i.e., we treat the bits in the red channel as a float, and do the same for green and blue), and use this triple of numbers as the coordinates of the (unnormalized) normal vector, from which we can compute **n**; this is one of the most common approaches today.

- It's possible to specify a set of normal vectors that are not actually consistent with each other, that is, they do not form the normal vector field for any surface (see Exercise 20.2). When rendered, these can look peculiar. So a third approach to bump mapping is to have the texture contain a *height* for each texture coordinate (*u*, *v*), indicating that we are to imagine that the surface is displaced from its current position by that amount along the original normal vector. The resultant surface (which is never actually created!) has tangent vectors in the *u*- and *v*-directions (i.e., the direction of greatest increase of *u*, and correspondingly of *v*), whose cross product we compute and use as the "normal" vector during shading computations. This clearly requires substantially more computation, but far less bandwidth, since we need only one value per location rather than two or three.

### 20.2.3 Contour Drawing

This example differs from the previous ones, because each surface point will have only *one* texture coordinate. A point *P* of a smooth surface is on a **contour** if the ray from *P* to the eye *E*, *r* = *E* − *P*, is perpendicular to the surface normal **n**. Thus, to render a surface by drawing its contours, all we must do is compute this dot product, and when it's near zero, make a black mark on the image, or leave the image white otherwise. To do so we make a one-dimensional texture map like the one shown in Figure 20.5. And as a texture coordinate, we compute

$$d = \mathbf{r} \cdot \mathbf{n} \tag{20.4}$$

$$u = \frac{d + 1}{2}. \tag{20.5}$$

![](img/f464cd0043eb5336aa0543fe20a0561b_601_0.png)

*Figure 20.4:* The vector **n** will be normalized to produce the new normal **n**'; the values *r* and *g* (for "red" and "green") vary across the surface, and are looked up in a texture map.

![](img/f464cd0043eb5336aa0543fe20a0561b_601_1.png)

*Figure 20.5:* A contour-drawing 1D texture.
