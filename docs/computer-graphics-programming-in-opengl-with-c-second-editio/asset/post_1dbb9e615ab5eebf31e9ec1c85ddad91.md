
Now use the integer reference (textureID) in the same manner as was described throughout the chapter.

## SUPPLEMENTAL NOTES

Researchers have developed a number of uses for texture units beyond just texturing models in a scene. In later chapters, we will see how texture units can be used for altering the way light reflects off an object, making it appear bumpy. We can also use a texture unit to store “height maps” for generating terrain, and for storing “shadow maps” to efficiently add shadows to our scenes. These uses will be described in subsequent chapters.

Shaders can also *write to textures*, allowing shaders to modify texture images, or even copy part of one texture into some portion of another texture.

Mipmaps and anisotropic filtering are not the only tools for reducing aliasing artifacts in textures. *Full-scene anti-aliasing* (FSAA) and other supersampling methods, for example, can also improve the appearance of textures in a 3D scene. Although not part of the OpenGL core, they are supported on many graphics cards through OpenGL’s extension mechanism [OE20].

There is an alternative mechanism for configuring and managing textures and samplers. Version 3.3 of OpenGL introduced *sampler objects* (sometimes called “*sampler states*”—not to be confused with sampler variables) that can be used to hold a set of texture settings independent of the actual texture object. Sampler objects are attached to texture units and allow for conveniently and efficiently changing texture settings. The examples shown in this textbook are sufficiently simple that we decided to omit coverage of sampler objects. For interested readers, usage of sampler objects is easy to learn, and there are many excellent online tutorials (such as [GE11]).

## Exercises

- 5.1 Modify Program 5.1 by adding the “noperspective” declaration to the texture coordinate vertex attributes, as described in Section 5.11. Then rerun the program and compare the output with the original. Is any perspective distortion evident?
- 5.2 Using a simple “paint” program (such as Windows “Paint” or GIMP [GI16]), draw a freehand picture of your own design. Then use your image to texture the pyramid in Program 5.1.
- 5.3 (PROJECT) Modify Program 4.4 so that the “sun,” “planet,” and “moon” are textured. You may continue to use the shapes already present, and you may use any texture you like. This will require you to build texture coordinates for the cube.

## References

- **[BL20]** Blender, The Blender Foundation, accessed July 2020, https://www.blender.org/
- **[GE11]** Geeks3D, “OpenGL Sampler Objects: Control Your Texture Units,” September 8, 2011, accessed July 2020, http://www.geeks3d.com/20110908/
- **[GI16]** GNU Image Manipulation Program, accessed October 2018, http://www.gimp.org
- **[HT12]** J. Hastings-Trew, JHT’s Planetary Pixel Emporium, accessed July 2020, http://planetpixelemporium.com/
- **[LU16]** F. Luna, Introduction to 3D Game Programming with DirectX 12, 2nd ed. (Mercury Learning, 2016) [accompanying disk].
- **[MA20]** Maya, AutoDesk, Inc., accessed July 2020, http://www.autodesk.com/products/maya/overview
- **[OE20]** OpenGL Registry, The Khronos Group, accessed July 2020, https://www.khronos.org/registry/OpenGL/index_gl.php
- **[OP14]** OpenGL Graphics System: A Specification (version 4.4), M. Segal and K. Akeley, March 19, 2014, accessed July 2020, https://www.khronos.org/registry/OpenGL/specs/gl/glspec44.core.pdf
- **[OP16]** OpenGL 4.5 Reference Pages, accessed July 2016, https://www.khronos.org/registry/OpenGL-Refpages/gl4/
- **[OT18]** OpenGL Tutorial, “Loading BMP Images Yourself,” opengl-tutorial.org, accessed July 2020, http://www.opengl-tutorial.org/beginners-tutorials/tutorial-5-a-textured-cube/#loading-bmp-images-yourself
- **[SO20]** Simple OpenGL Image Library 2 (SOIL2), *SpartanJ*, accessed July 2020, https://bitbucket.org/SpartanJ/soil2
- **[SP16]** Perspective Correct Interpolation and Vertex Attributes. Scratchapixel, c.2016, Accessed July 2020. https://www.scratchapixel.com/lessons/3d-basic-rendering/rasterization-practical-implementation
- **[TU16]** J. Turberville, Studio 522 Productions, Scottsdale, AZ, www.studio522.com (dolphin model developed 2016).
- **[WI83]** L. Williams, “Pyramidal Parametrics,” *Computer Graphics* 17, no. 3 (July 1983).

## Chapter 6

## 3D Models

- 6.1 Procedural Models – Building a Sphere ··· 129
- 6.2 OpenGL Indexing – Building a Torus ··· 138
- 6.3 Loading Externally Produced Models ··· 145
- Supplemental Notes ··· 155

So far we have dealt only with very simple 3D objects, such as cubes and pyramids. These objects are so simple that we have been able to explicitly list all of the vertex information in our source code and place it directly into buffers.

However, most interesting 3D scenes include objects that are too complex to continue building them as we have, by hand. In this chapter, we will explore more complex object models, how to build them, and how to load them into our scenes.

3D modeling is itself an extensive field, and our coverage here will necessarily be very limited. We will focus on the following two topics:

- *building models procedurally*
- *loading models produced externally*

While this only scratches the surface of the rich field of 3D modeling, it will give us the capability to include a wide variety of complex and realistically detailed objects in our scenes.

### 6.1 Procedural Models – Building a Sphere

Some types of objects, such as spheres, cones, and so forth, have mathematical definitions that lend themselves to algorithmic generation. Consider for example a circle of radius R—coordinates of points around its perimeter are well defined (Figure 6.1).

![](img/1695de1bc7486362f86c143285f3fb40_150_0.png)

We can systematically use our knowledge of the geometry of a circle to algorithmically build a sphere model. Our strategy is as follows:

1. Select a *precision* representing a number of circular regions the sphere is divided into. In the left side Figure 6.2, the sphere is sliced into four regions.
2. Subdivide the circumference of each circular slice into some number of points. See the right side of Figure 6.2. More points and horizontal slices produces a more accurate and smoother model of the sphere. In our model, *each slice will have the same number of points, including at the very top and bottom (where those points are coincident).*

   ![](img/1695de1bc7486362f86c143285f3fb40_150_1.png)
3. Group the vertices into triangles. One approach is to step through the vertices, building two triangles at each step. For example, as we move along the row of the five colored vertices on the sphere in Figure 6.3, for each of those five vertices we build the two triangles shown in the corresponding color (the steps are described in greater detail below).

![](img/1695de1bc7486362f86c143285f3fb40_153_0.png)

**Figure 6.7**  
Vertex array and corresponding index array.

two triangles forming a square region above and to its right, as shown earlier in Figure 6.3. The processing is thus organized into nested loops, as follows:

```
for each horizontal slice i in the sphere (i ranges from 0 through all the slices in the sphere)
{
    for each vertex j in slice i (j ranges from 0 through all the vertices in the slice)
    {
        calculate indices for two triangles which point to neighboring vertices to the right,
        above, and to the above-right of vertex j
    }
}
```

For example, consider the “red” vertex from Figure 6.3 (repeated in Figure 6.8). The vertex in question is at the lower left of the yellow triangles shown in Figure 6.8, and given the loops just described, would be indexed by i*n+j, where i is the slice currently being processed (the outer loop), j is the vertex currently being processed within that slice (the inner loop), and n is the number of vertices per slice. Figure 6.8 shows this vertex (in red) along with its three relevant neighboring vertices, each with formulas showing how they would be indexed.

These four vertices are then used to build the two triangles (shown in yellow) generated for this (red) vertex. The six entries in the index table for these two triangles are indicated in the figure in the order shown by the numbers 1 through 6. Note that entries 3 and 6 both refer to the same vertex, which is also the case for entries 2

![](img/1695de1bc7486362f86c143285f3fb40_153_1.png)

**Figure 6.8**  
Indices generated for the jth vertex in the ith slice (n = number of vertices per slice).
