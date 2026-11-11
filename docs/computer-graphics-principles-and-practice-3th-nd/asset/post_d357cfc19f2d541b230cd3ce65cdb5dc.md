
Even with this idealization, however, the pixel value that we’re hoping to compute is an integral over the pixel area and the set of directions through the lens. Even if we assume a lens so tiny that the latter integral can be accurately estimated by a single ray (the pinhole approximation), there’s still an area integral to estimate.

One very bad way to estimate this integral is with a single sample, taken at the center of the pixel region (i.e., the simplest ray-tracing model, where we shoot a ray through the pixel center). What makes this approach particularly bad are aliasing artifacts: if we’re making a picture of a picket fence, and the spacing of the pickets is slightly different from the spacing of the pixels, the result will be large blocks of constant color, which the eye detects as bad approximations of what should be in each pixel (see Figure 31.9).

If we instead take a random point in each pixel, then this aliasing is substantially reduced (see Figure 31.10). Instead, we see salt-and-pepper noise in the image.

Because our visual system does not tend to see “edges” in such noise, but is very likely to see incorrect edges in the aliased image, the tradeoff of aliases for noise is a definite improvement (see Figure 31.11).

This notion of taking many (randomized) samples over some domain of integration and averaging them applies in far more generality. We can integrate over wavelength bands (rather than doing the simpler RGB computations that are so common, which amount to a fixed-sample strategy). We can integrate over the lens area to get depth-of-field effects and chromatic aberration. For a scene that’s moving, we can simulate the effect of a shutter that’s open for some period of time by integrating over a fixed “time window.” All of these ideas were described in a classic paper by Cook et al. [CPC84], which called the process distributed ray tracing. Because of possible confusion with notions of distributed processing, we prefer the term **distribution ray tracing** which Cook now uses to describe the algorithm [Coo10]. We’ll discuss the particular sampling strategies used in distribution ray tracing in Chapter 32.

In short: To render a realistic image in the general case, we need to average, in some way, many values, each of which is $L(P, \omega)$ for some point $P$ of the image plane and some direction $\omega \in S^2$.

![](img/f464cd0043eb5336aa0543fe20a0561b_887_0.png)

*Figure 31.9: Pixel-center samples of a picket-fence scene lead to large blocks of black-and-white pixels.*

![](img/f464cd0043eb5336aa0543fe20a0561b_887_1.png)

*Figure 31.10: Random ray selection within each pixel reduces aliasing artifacts, but replaces them with noise.*

![](img/f464cd0043eb5336aa0543fe20a0561b_887_2.png)

*Figure 31.11: (a) A close-up view of a portion of a sawtooth-shaped geometry (note that each sawtooth occupies a little more than one unit on the x-axis) and the locations of pixel samples (small circles). (b) The resultant image. Even though there are 1024 rays in this 104-pixel-wide image, aliasing causes us to see just two. (c) When we take “jittered samples” (each sample is moved up to a half pixel both vertically and horizontally), the resultant image is noisy, but exhibits no aliasing.*

## 31.10 The Discretization Approach: Radiosity

We’ll now briefly discuss radiosity—an approach that produces renderings for certain scenes very effectively—and then return to the more general scenes that require sampling methods and discuss how to effectively estimate the value $L(P, \omega)$ in the algorithms that work on those scenes.

The radiosity method for rendering differs from the methods we’ve seen in Chapter 15; in those methods, we started with the imaging rectangle and said, “We need to compute the light that arrives here, so let’s cast rays into the scene and see where they hit, and compute the light arriving at the hit point by various methods.” Whether we did this one pixel at a time or one light at a time or one polygon at a time was a matter of implementation efficiency. The key thing is that we said, “Start from the imaging rectangle, and use that to determine which parts of the light transport to compute.” A radically different approach is to simulate the physics directly: Start with light emitted from light sources, see where it ends up, and for the part that ends up falling on the imaging rectangle, record it. This approach was taken by Appel [App68], who cast light rays into the scene and then, at the image plane location of the intersection point (if it was visible), drew a small mark (a “+” sign). In areas of high illumination there were many marks; in areas of low illumination, almost none. By taking a black-and-white photograph of the result (which was drawn with a pen on plotter paper) and then examining the negative of the photograph, he produced a rendering of the incident light.

Radiosity takes a similar approach, concentrating first on the light in the scene, and only later on the image produced. Because the surfaces in the scene are assumed Lambertian, the transformation from a representation of the surface radiance at all points of the scene to a final rendering is relatively easy.

The radiosity approach has two important characteristics.

- It’s a solution to a *subproblem*, in the sense that it only applies to Lambertian reflectors, and is generally applied to scenes with only Lambertian emitters.
- It’s a “discretization” approach: The problem of computing $L(P, \omega_o)$ for every $P \in \mathcal{M}$ and $\omega_o \in S_+^2(P)$ is reduced to computing a finite set of values. The scene is partitioned into small patches, and we compute a radiosity value for each of these finitely many patches.

The division into patches means that radiosity is a **finite element** method, in which a function is represented as a sum of finitely many simpler functions, each typically nonzero on just a small region. (The word “finite” here is in contrast to “infinitesimal”: Rather than finding radiance at every single point of the surface, each point being “infinitesimal,” we compute a related value on “finite” patches.)

Radiosity was the first method to produce images exhibiting color bleeding (in which a red wall meeting a white ceiling could cause the ceiling to be pink near the edge where they meet), and not requiring an “ambient term” in its description of reflection—a term included in scattering models (see Chapter 27) to account for all the light in a scene that wasn’t “direct illumination,” which had presented problems for years previously. Figure 31.12 shows an example.

![](img/f464cd0043eb5336aa0543fe20a0561b_889_0.png)

*Figure 31.12: A radiosity rendering of a simple scene. Note the color-bleeding effects. (Courtesy of Greg Coombe, “Radiosity on graphics hardware” by Coombe, Harris and Lastra, Proceedings of Graphics Interface 2004.)*

The first step in radiosity is to partition all surfaces in the scene into small (typically rectangular) patches. The patches should be small enough that the illumination arriving at a patch is roughly constant over the patch so that the light leaving the patch will be too, and hence can be represented by a single value. This “meshing” step has a large impact on the final results, which we’ll discuss presently. For now, let’s just assume the scene surfaces are partitioned into many small patches. We’ll use the letters j and k to index the patches, and use $A_j$ to indicate the area of patch j, $B_j$ to denote a value proportional to the radiance leaving any point of patch j, in any outgoing direction² $\omega_o$, and $n_j$ to indicate the normal vector at any point of patch j.

Each patch j is assumed to be a Lambertian reflector, so its BRDF is a constant function,

$$f_r(P, \omega_o, \omega_i) = \rho_j/\pi \tag{31.32}$$

where $\rho_j$ is the reflectivity and $P$ is any point of the patch. Furthermore, each luminaire is assumed to be a “Lambertian” emitter of constant radiance, that is, $L^e(P, \omega_o)$ is a constant for $P$ in patch j and $\omega_o$ an outgoing vector at $P$.

This simple form for scattering and the assumption about constant emission together mean that the rendering equation can be substantially simplified.

For the moment, let’s make four more assumptions. The first is that the scene is made up of closed 2-manifolds, and no 2-manifold meets the interior of any other (e.g., two cubes may meet along an edge or face, but they may not interpenetrate). This also means that we don’t allow two-sided surfaces (i.e., a single polygon that reflects from both sides)—these must be modeled as thin, solid panels instead.

For the other three, we let $P$ and $P'$ be points of patch j and $Q$ and $Q'$ be points of patch k, and $n_j$ and $n_k$ be the patch normal vectors. Then we assume the following.

- The distance between $P$ and $Q$ is well approximated by the distance from the center $C_j$ of patch j to the center $C_k$ of patch k.
- $n_j \cdot (P-Q) \approx n_j \cdot (P'-Q')$, that is, any two lines between the patches are almost parallel.
- If $n_j \cdot n_k < 0$, then every point of patch j is visible from patch k, and vice versa. So, if two patches face each other, then they are completely mutually visible.

2. By “outgoing direction,” we mean that $\omega_o \cdot n_j > 0$; the radiance is independent of direction because the surfaces are assumed Lambertian.
