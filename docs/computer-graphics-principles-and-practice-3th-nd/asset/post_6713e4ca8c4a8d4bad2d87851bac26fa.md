
```xml
<GeometryModel3D
    Geometry="{StaticResource RSRCDesertFloor}"
    Material="{StaticResource RSRCTextureSand}"/>
```

![](img/f464cd0043eb5336aa0543fe20a0561b_182_0.png)

The result is shown in Figure 6.32, from a point of view high above the pyramid. The result is *not acceptable*; there is some subtle variation in the color of the desert floor, but the color patches are huge (in comparison with the pyramid).

The problem is that our tiny 64 × 64-pixel sand decal (which was designed to represent about one square inch of a sandy floor) has been stretched to cover the entire desert floor. The result looks nothing like sand even though our decal provides fairly good realism when viewed unscaled.

Our failure to simulate desert sand here is a case of a reasonable texture image being applied to the model incorrectly. Implementing texturing in WPF requires choosing between two mapping strategies: tiling and stretching.

### 6.4.1 Texturing via Tiling

If the texture is being used to simulate a *material* with a consistent look and no obvious points of discontinuity (e.g., sand, asphalt, brick), the texture image is replicated as needed to cover the target surface. In this case, the texture is typically a small sample image (either synthetic or photographic) of the material, which has been designed especially to ensure that adjacent tiles fit together seamlessly. As an example, consider the texture image of Figure 6.33 showing six rows of red brick.

![](img/f464cd0043eb5336aa0543fe20a0561b_182_1.png)

Applying it to each face of a rectangular prism without tiling produces a decent image (Figure 6.34) but the number of rows is insufficient for representing a tall brick fortress. Tiling allows the number of apparent brick rows to be multiplied, producing an image (Figure 6.35) that is more indicative of a tall fortress.

![](img/f464cd0043eb5336aa0543fe20a0561b_182_2.png)

![](img/f464cd0043eb5336aa0543fe20a0561b_182_3.png)

Consult the texture-mapping module of the lab for details on how to enable and configure tile-based texturing in WPF.

### 6.4.2 Texturing via Stretching

If texture is being used as a substitute for a highly complex model (e.g., a city as seen from above, or a cloudy sky), the texture image is often quite large (to provide sufficiently high resolution) and may be either photographic or original artwork (e.g., if being used to represent a landscape in a fantasy world). Most importantly, this kind of texture image is a “scene” that would look unnatural if tiled. The correct application of this kind of texture image is to set the mesh’s texture coordinates in such a way as to stretch the texture image to cover the mesh.

For example, in our desert scene, the background sky (as seen often in Figures 6.5 through 6.17) is modeled as a cylinder whose interior surface is stretch-textured with the actual sky photograph shown in Figure 6.36.

![](img/f464cd0043eb5336aa0543fe20a0561b_182_4.png)

Consult the texture-mapping module of the lab for details on how to enable and configure stretch-based texturing in WPF. More information, including algorithms for computing texture coordinates for curved surfaces and a discussion of common texture-mapping problems, is presented in Section 9.5 and in Chapter 20.

## 6.5 The WPF Reflectance Model

In Section 6.2.2, we presented Lambert’s simple cosine rule for calculating reflected light from a diffuse surface. That simple equation is just one part of the complete WPF reflectance model, which is based on a classic approximation strategy that provides results of acceptable quality, without complex physics-based calculations, on a wide variety of commodity graphics hardware.

### 6.5.1 Color Specification

The word “color” is used to describe multiple things: the spectral distribution of wavelengths in light, the amount of light of various wavelengths that a surface will reflect, and the perceptual sensation we experience on seeing an object. Representing color precisely is a serious matter to which Chapter 28 is dedicated. Indeed, specifying color via RGB triples—the common approach in graphics APIs and drawing/painting applications—may well be the grossest of all the approximations made in computer graphics practice!

When describing a scene, we specify the colors of the light sources and of the objects themselves. In WPF, specifying the former is straightforward (see Section 6.2.2), but describing the latter is far more complex, requiring the separation of the material into three distinct components. Section 6.5.3 is dedicated to describing this specification technique and the effects it can achieve.

### 6.5.2 Light Geometry

The two WPF lighting types we have used thus far (ambient and directional) are useful approximations but decidedly unrealistic: They are not considered to be emanating from a specific point in the scene, and their brightness is uniform throughout the entire scene.

A geometric light source adds realism in that it is located in the scene and is attenuated—that is, the amount of energy reaching a particular surface point P is dependent on the distance from P to the light source. WPF offers two geometric light source types.

- **A point light** emanates energy equally in all directions, simulating a naked bulb suspended from a ceiling without any shade or baffles. Specification parameters include its position and the attenuation type/rate (constant, linear, or quadratic, as described in Section 14.11.9). The lab software for this chapter allows experimentation with this type of light source.
- **A spotlight** is similar, but it simulates a theatre spotlight in that it spreads light uniformly but restricts it to a cone-shaped volume.

Geometric lights are useful but should still be considered only approximations, since real physical light sources (described in Section 14.11.6) have volume and surface area, and thus do not emit light from a single point.

### 6.5.3 Reflectance

In our modeling of desert scenes throughout this chapter, we have applied material to our meshes by specifying either a solid color or a texture image. However, there is more to a material than its color. If you’ve shopped for interior-wall paint, you know that you must also choose the finish (flat, eggshell, satin, semigloss), which describes how the painted surface will reflect light.

The physics of how light is reflected from a surface is extremely complex, so for decades, the fixed-function pipeline has relied on a classic approximation strategy called the **Phong reflection (lighting) model** that yields an effective simulation of reflection at very little computational cost.³ In the Phong model, a material is described by configuring three distinct components of reflection: ambient (a small constant amount of light, providing a gross level of inter-reflection), diffuse (representing viewer-independent light reflected equally in all directions), and specular⁴ (providing glossy highlights on shiny surfaces when the viewpoint is close to the reflection ray). The values calculated for the three components—Figure 6.37, (a) through (c)—are summed to produce the final appearance, shown in part (d) of that figure.

![](img/f464cd0043eb5336aa0543fe20a0561b_184_0.png)

*Figure 6.37: Renderings of a teapot, showing the contribution of each of the three components generated by the Phong lighting equation: (a) ambient, (b) diffuse, (c) specular, and (d) result generated by summing the contributions.*

The independent nature of the diffuse and specular components allows us to generate the appropriate appearance of materials having multiple layers with distinct reflectance characteristics. Consider a polished red apple: On top of its diffuse red layer lies a colorless wax coating that provides glossy highlights based on the color of the light source (not of the apple). This same pattern of reflection is also very common in plastics, although it is not generated by a multilayer reflectance, but by the nature of the plastic material itself. Our blue plastic teapot (in Figure 6.37) shows this: Its glossy highlights have the colorless hue of the incoming white light, while the diffuse reflections have the blue hue of the plastic. In Section 6.5.3.3 we’ll provide more detail on how to produce this effect. Of course, this is not a complete summary; summing noninteracting layers is inadequate for complex materials such as human skin; Section 14.4 presents an introduction to richer, more accurate material models, and Chapter 27 gives full details.

In this section, we describe the lighting equation for WPF’s reflectance model, which is heavily based on, but not completely identical to, the Phong model. Let’s first examine the equation’s inputs that are specified as properties of the material resources (e.g., in WPF elements such as `DiffuseMaterial` and others enumerated in this chapter’s online materials):

| Symbol | Description | Format |
|---|---|---|
| $C_d$ | Innate color of “diffuse layer” | $(C_{d,R}, C_{d,G}, C_{d,B})$ |
| $C_s$ | Innate color of “specular layer” | $(C_{s,R}, C_{s,G}, C_{s,B})$ |
| $k_a$ | Efficiency of diffuse layer at reflecting ambient light | $(k_{a,R}, k_{a,G}, k_{a,B})$ |
| $k_d$ | Efficiency of diffuse layer at reflecting directional/geometric light | $(k_{d,R}, k_{d,G}, k_{d,B})$ |
| $k_s$ | Efficiency of specular layer at reflecting directional/geometric light | $(k_{s,R}, k_{s,G}, k_{s,B})$ |

³ This non-physics-based reflectance model was invented early in the history of raster graphics and rendering research in the 1970s initially by University of Utah Ph.D. student Bui Tuong Phong and then slightly modified by Blinn, and has been remarkably long-lived, especially in real-time graphics.

⁴ For this chapter only, we are following the convention that “specular” refers to *somewhat concentrated reflections rather than to a perfect mirror reflection*. Elsewhere specular means “mirrorlike,” while sort-of-specular reflection is called “glossy.” The use of “specular” for glossy follows both Phong’s original paper and the WPF convention, but conflicts with its ordinary meaning of “having the properties of a mirror.”
