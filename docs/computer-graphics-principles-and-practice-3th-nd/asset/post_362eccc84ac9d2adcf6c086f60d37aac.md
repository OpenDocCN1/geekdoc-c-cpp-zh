
### Table 33.1: Predefined items in GLSL.

| Name | Type | Meaning |
|---|---|---|
| `gl_Vertex` | `vec4` | The homogeneous position of the current vertex |
| `gl_Normal` | `vec4` | The normal at the current vertex |
| `gl_FragColor` | `vec4` | The RGBA color of the current fragment |
| `gl_ModelViewProjectionMatrix` | `mat4` | The transformation from modeling coordinates to normalized device coordinates |
| `gl_Position` | `vec4` | The homogeneous normalized device coordinates of the current vertex, before perspective divide, i.e., `gl_Position.w` may not be `1.0`.² |
| `pow(x, y)` |  | Raises x to the y power; if x is a vector, do so termwise |
| `max(x, y)` |  | Returns the larger of x and y |
| `dot(x, y)` |  | Dot product of vectors; x and y must be of the same size (i.e., `vec2` or `vec3` or `vec4`) |

A vertex shader may also get *other* input data, in one of two forms. First, there may be other per-vertex information, like the normal vector, or texture coordinates. Second, there may be information that’s specified *per object*. In our case, the diffuse reflectivity is one such item (we don’t use it in the vertex shader), and the world-space position of the light is another. That world-space light position is declared `uniform vec3 wsLight`; the keyword `uniform` tells GL that the value is set once per object. The declaration of the variable before `main` indicates that it needs to be linked to the rest of the program. In this case, it’s linked to the host program by a call in `ConfigureShaderArgs`.

Finally, a vertex shader may *set* values to be used by other shaders. These values are computed once per vertex; during the rasterization and clipping phase, they’re interpolated to get values at each fragment. The default is perspective interpolation (i.e., barycentric interpolation in camera coordinates), but image-space barycentric interpolation is also an option. The resultant values vary from point to point on the triangle, and so they are declared `varying`.

Our shader computes one of these, `gouraudFactor` (line 2), which is the dot product of the unit surface normal and the incoming light direction to the world-space light source.

Having computed this dot product (line 10) and the location of each vertex, we move on to the fragment shader (see Listing 33.4).

² In OpenGL these are called “Clip coordinates,” while normalized device coordinates are those after the perspective divide.

### Listing 33.4: The fragment shader for the Gouraud shading program.

```glsl
    /* Diffuse/ambient surface color */
    uniform vec3 diffuseColor;

    /* Intensity of the diffuse term. */
    uniform float diffuse;

    /* Color of the light source */
    uniform vec3 lightColor;

    /* dot product of surf normal with light */
    varying float gouraudFactor;

    void main() {
        gl_FragColor.rgb = diffuse * diffuseColor *
            (max(gouraudFactor, 0.0) * lightColor);
    }
```

Once again, three uniform variables, whose values were established in the host program, get used in the fragment shader: the diffuse reflectivity, the color of the surface, and the color of the light.

We also, in the fragment shader, have access to the gouraudFactor that was computed in the vertex shader. At any fragment, the value for this variable is the result of interpolating the values at the three vertices of the triangle. In the shader, we do a very simple operation: We multiply the diffuse reflectivity by the diffuse color to get a vec3, and multiply the gouraudFactor (if it's positive) by the light color, giving another vec3. We then take the term-by-term product of these two (using the * operator) and assign it to the gl_FragColor.rgb. If the light is pure red and the surface is pure blue, then the product will be all zeroes. But in general, we are taking the product of the amount of red light and how well the surface reflects red light (and how well it reflects in this direction at all), and similarly for green and blue, to get a color for the fragment.

Every fragment shader is responsible for setting the value of gl_FragColor, which is used by the remainder of the graphics pipeline.

That's it! This simple host program and two simple shaders implement Gouraud shading. The results are shown in Figure 33.3. In the version of the program available on the book's website, we've added one GUI that allows you to pick a diffuse color and set the reflectivity interactively, and another that allows you to rotate the icosahedron to any position you like, but the essential ideas are unchanged.

![](img/f464cd0043eb5336aa0543fe20a0561b_987_0.png)

*Figure 33.3: An icosahedron rendered by our first shader.*

## 33.5 A Phong Shader

In generalizing this to implement the Phong model, there are no real surprises. We have to declare a few more variables in the host program, such as the specular exponent shininess, the specular reflection coefficient specular, and the specular color specularColor, and we also include ambient light as ambientLightColor, but we're confident that you can do this without seeing the code.

Recall that the basic Phong model of Chapter 6 tells us to compute the pixel color using

color = k_a O_a I_a + k_d O_d I_d (n · l) + k_s O_s (r · n)^{n_s} I_d, (33.2)

where $k_d$ and $k_s$ are the diffuse and specular reflection coefficients, $I_a$ is the ambient light color, $I_d$ is the diffuse light color (i.e., the color of our directional light), $O_d$ is the diffuse color of the object, $\ell$ is a unit vector in the direction from the surface point toward the light source, $\mathbf{r}$ is the (unit) reflection of the eye vector (the vector from the surface to the eye) through the surface normal, and $n_s$ is the specular exponent, or shininess: A small value gives a spread-out highlight; a large value like $n_s = 500$ gives a very concentrated highlight. The formula is only valid if $\mathbf{r} \cdot \mathbf{n} > 0$; if it’s negative, the last term gets eliminated.

In the vertex shader (see Listing 33.5), we compute the normal vector at each vertex, and the ray from the surface point to the eye (at each vertex). We don’t normalize either one yet.

### Listing 33.5: The vertex shader for the Phong shading program.

```glsl
/** Camera origin in world space */
uniform vec3 wsEyePosition;

/** Non-unit vector to the eye from the vertex */
varying vec3 wsInterpolatedEye;

/** Surface normal in world space */
varying vec3 wsInterpolatedNormal;

void main(void) {
    wsInterpolatedNormal = g3d_ObjectToWorldNormalMatrix *
                          gl_Normal;
    wsInterpolatedEye = wsEyePosition -
                        g3d_ObjectToWorldMatrix * gl_Vertex.xyz;

    gl_Position = gl_ModelViewProjectionMatrix * gl_Vertex;
}
```

In the pixel shader, we take the interpolated values of the normal and eye-ray vectors and use them to evaluate the Phong lighting equation. Even if the normal vector at each vertex is a unit vector, the result of interpolating these will generally not be a unit vector. That’s why we didn’t bother normalizing them in the vertex shader: We’ll need to do a normalization at each pixel anyhow. After normalizing these, we compute the reflected eye vector $\mathbf{r}$, and use it in the Phong equation to evaluate the pixel color. Note the use of max (line 32) to eliminate the case where the reflected eye vector is not in the same half-space as the ray to the light source. (See Listing 33.6.)

### Listing 33.6: The fragment shader for the Phong shading program.

```glsl
/** Diffuse/ambient surface color */
uniform vec3 diffuseColor;
/** Specular surface color, for glossy and mirror refl’n. */
uniform vec3 specularColor;
/** Intensity of the diffuse term. */
uniform float diffuse;
/** Intensity of the specular term. */
uniform float specular;
/** Phong exponent; 100 = sharp highlight, 1 = broad highlight */
uniform float shine;
/** Unit world space dir’n to (infinite, directional) light */
uniform vec3 wsLight;
```
