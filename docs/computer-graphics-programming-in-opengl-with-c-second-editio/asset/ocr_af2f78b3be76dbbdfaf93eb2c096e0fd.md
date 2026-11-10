The vertex shader contains our first example of using the struct notation. A GLSL “struct” is like a datatype; it has a name and a set of fields. When a variable is declared using the name of a struct, it then contains those fields, which are accessed using the “.” notation. For example, variable “light” is declared of type “PositionalLight”, so we can thereafter refer to its fields light.ambient, light.diffuse, and so forth.

![](bbox=[0.543, 0.11, 0.857, 0.278])

**Figure 7.9**  
Torus with Gouraud shading.

Also note the field selector notation “.xyz”, used in several places in the vertex shader. This is a shortcut for converting a vec4 to an equivalent vec3 containing only its first three elements.

The vertex shader is where most of the lighting computations are performed. For each vertex, the appropriate matrix transforms are applied to the vertex position and associated normal vector, and vectors for light direction (L⃗) and reflection (R⃗) are computed. The ADS computations described in Section 7.4 are then performed, resulting in a color for each vertex (called varyingColor in the code). The colors are interpolated as part of the normal rasterization process. The fragment shader is then a simple pass-through. The lengthy list of uniform variable declarations is also present in the fragment shader (for reasons described earlier in Chapter 4), but none of them are actually used there.

Note the use of the GLSL functions normalize(), which converts a vector to unit length and is necessary for proper application of the dot product, and reflect(), which computes the reflection of one vector about another.

Artifacts are evident in the output torus shown in Figure 7.9. Specular highlights have a blocky, faceted appearance. This artifact is more pronounced if the object is in motion (we can’t illustrate that here).

Gouraud shading is susceptible to other artifacts. If the specular highlight is entirely contained within one of the model’s triangles—that is, if it doesn’t contain at least one of the model vertices—then it may disappear entirely. The specular component is calculated per-vertex, so if a model vertex with a specular contribution does not exist, none of the rasterized pixels will include specular light either.