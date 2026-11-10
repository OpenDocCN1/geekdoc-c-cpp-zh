
![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_207_0.png)

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_207_1.png)

**Figure 7.17** Combining lighting and textures.

for each fragment (by default it chooses the value associated with the first vertex in the triangle). In the Phong shading example, this could be done as follows:

```
flat out vec3 varyingNormal;        in the vertex shader, and
flat in vec3 varyingNormal;         in the fragment shader.
```

An important kind of light source that we haven’t discussed is a *distributed light* or *area light*, which is a light that is characterized by having a source that occupies an area rather than being a single point location. A real-world example would be a fluorescent tube-style light commonly found in an office or classroom. Interested readers can learn about such lighting details in [MH18].

## HISTORICAL NOTE

We took the liberty of oversimplifying some of the terminology in this chapter, with respect to the contributions of Gouraud and Phong. Gouraud is credited with *Gouraud shading*—the notion of generating a smoothly curved surface appearance by computing light intensities at vertices and allowing the rasterizer to interpolate these values (sometimes called “smooth shading”). Phong is credited with *Phong shading*, another form of smooth shading that instead interpolates normals and computes lighting per-pixel. Phong is also credited with pioneering the successful incorporation of specular highlights into smooth shading. For this reason, the ADS lighting model, when applied to computer graphics, is often referred to as the *Phong Reflection Model*. So our example of Gouraud shading is, more accurately, Gouraud shading with a Phong reflection model. Since Phong’s reflection model has become so ubiquitous in 3D graphics programming, it is common to demonstrate Gouraud shading in the presence of Phong reflection, although it is a bit misleading because Gouraud’s original 1971 work did not, for example, include any specular component.

## Exercises

- 7.1 (*PROJECT*) Modify Program 7.1 so that the light can be positioned by moving the mouse. After doing this, move the mouse around and note the movement of the specular highlight and the appearance of the Gouraud shading artifacts. You may find it convenient to render a point (or small object) at the location of the light source.

- 7.2 Repeat Exercise 7.1, but applied to Program 7.2. This should only require substituting the shaders for Phong shading into your solution to Exercise 7.1. The improvement from Gouraud to Phong shading should be even more apparent here, when the light is being moved around.

- 7.3 (*PROJECT*) Modify Program 7.2 so that it incorporates TWO positional lights, placed in different locations. The fragment shader will need to blend the diffuse and specular contributions of each of the lights. Try using a weighted sum, similar to the one shown in Section 7.6. You can also try simply adding them and clamping the result so it doesn't exceed the maximum light value.

- *7.4 (RESEARCH AND PROJECT)* Replace the positional light in Program 7.2 with a "spot" light, as described in Section 7.2. Experiment with the settings for *cutoff angle* and *falloff exponent*, and observe the effects.

## References

- [BA20] N. Barradeau, accessed March 2021, http://www.barradeau.com/nicoptere/dump/materials.html
- [BL77] J. Blinn, "Models of Light Reflection for Computer Synthesized Pictures," *Proceedings of the 4th Annual Conference on Computer Graphics and Interactive Techniques*, 1977.
- [DI21] *Luxo Jr.* (Pixar, © Disney), accessed March 2021, https://www.pixar.com/luxo-jr
- [GO71] H. Gouraud, "Continuous Shading of Curved Surfaces," *IEEE Transactions on Computers* C-20, no. 6 (June 1971).
- [MH18] T. Akenine-Möller, E. Haines, N. Hoffman, A. Pesce, M. Iwanicki, and S. Hillaire, *Real-Time Rendering*, 4th ed. (A. K. Peters / CRC Press 2018).
- [PH73] B. Phong, "Illumination of Computer-Generated Images" (PhD thesis, University of Utah, 1973).
- [PH75] B. Phong, "Illumination for Computer Generated Pictures," *Communications of the ACM* 18, no. 6 (June 1975): 311–317.
- [ST14] The Stanford 3D Scanning Repository, accessed March 2021, http://graphics.stanford.edu/data/3Dscanrep/
- [TU18] J. Turberville, Studio 522 Productions, Scottsdale, AZ, www.studio522.com (dolphin model developed March 2021).

## Chapter 8

## Shadows

- 8.1 The Importance of Shadows ····································· 191
- 8.2 Projective Shadows ··········································· 192
- 8.3 Shadow Volumes ·············································· 193
- 8.4 Shadow Maps ················································· 194
- 8.5 A Shadow Mapping Example ····································· 201
- 8.6 Shadow Mapping Artifacts ····································· 208
- 8.7 Soft Shadows ················································· 210
- Supplemental Notes ··············································· 218

### 8.1 THE IMPORTANCE OF SHADOWS

In Chapter 7, we learned how to add lighting to our 3D scenes. However, we didn’t actually add light—instead, we simulated the effects of light on objects—using the ADS model—and modified how we drew those objects accordingly.

The limitations of this approach become apparent when we use it to light more than one object in the same scene. Consider the scene in Figure 8.1, which includes both our brick-textured torus and a ground plane (the ground plane is the top of a giant cube with a grass texture from [LU16]).

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_211_0.png)

At first glance our scene may appear reasonable. However, closer examination reveals that there is something very important missing. In particular, it is impossible to discern the distance between the torus and the large textured cube below it. Is the torus floating above the cube, or is it resting on top of the cube?

**Figure 8.1** Scene without shadows.

The reason we cannot answer this question is due to the lack of *shadows* in the scene. We expect to see shadows, and our brain uses shadows to help build a more complete mental model of the objects we see and where they are located.

Consider the same scene, shown in Figure 8.2, with shadows incorporated. It is now obvious that the torus is resting on the ground plane in the left example and floating above it in the right example.

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_212_0.png)

### 8.2 PROJECTIVE SHADOWS

A variety of interesting methods have been devised for adding shadows to 3D scenes. One method that is well suited to drawing shadows on a ground plane (such as our image in Figure 8.1) and relatively computationally inexpensive is called *projective shadows*. Given a point light source position (X_L, Y_L, Z_L), an object to render, and a plane on which the object's shadow is to be cast, it is possible to derive a transformation matrix that will convert points (X_W, Y_W, Z_W) on the object to corresponding shadow points (X_S, 0, Z_S) on the plane. The resulting "shadow polygon" is then drawn, typically as a dark object blended with the texture on the ground plane, as illustrated in Figure 8.3.

The advantages of projective shadow casting are its efficiency and simplicity of implementation. However, it only works on a flat plane—the method can't be used to cast shadows on a curved surface or on other objects. It is still useful for performance-intensive applications involving outdoor scenes, such as in many video games.

Development of projective shadow transformation matrices is discussed in [AS14], [BL88], and [KS16].

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_213_0.png)

### 8.3 SHADOW VOLUMES

Another important method, proposed by Crow in 1977, is to identify the spatial volume shadowed by an object, and reduce the color intensity of polygons inside the intersection of the shadow volume with the view volume [CR77]. Figure 8.4 shows a cube in a shadow volume, so the cube would be drawn darker.

Shadow volumes have the advantage of being highly accurate, with fewer artifacts than other methods. However, finding the shadow volume, and then computing whether each polygon is inside of it, is computationally expensive even on modern GPU hardware. Geometry shaders can be used to generate shadow volumes, and the *stencil buffer*<sup>1</sup> can be used to determine whether a pixel is within the volume. Some graphics cards include hardware support for optimizing certain shadow volume operations.

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_213_1.png)

<sup>1</sup> The *stencil buffer* is a third buffer—along with the color buffer and the z-buffer—accessible through OpenGL. The stencil buffer is not described in this textbook.
