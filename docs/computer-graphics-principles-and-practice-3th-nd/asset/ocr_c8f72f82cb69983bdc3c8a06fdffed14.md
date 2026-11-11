where $k_d$ and $k_s$ are the diffuse and specular reflection coefficients, $I_a$ is the ambient light color, $I_d$ is the diffuse light color (i.e., the color of our directional light), $O_d$ is the diffuse color of the object, $\ell$ is a unit vector in the direction from the surface point toward the light source, $\mathbf{r}$ is the (unit) reflection of the eye vector (the vector from the surface to the eye) through the surface normal, and $n_s$ is the specular exponent, or shininess: A small value gives a spread-out highlight; a large value like $n_s = 500$ gives a very concentrated highlight. The formula is only valid if $\mathbf{r} \cdot \mathbf{n} > 0$; if it’s negative, the last term gets eliminated.

In the vertex shader (see Listing 33.5), we compute the normal vector at each vertex, and the ray from the surface point to the eye (at each vertex). We don’t normalize either one yet.

# Listing 33.5: The vertex shader for the Phong shading program.

```
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
```

In the pixel shader, we take the interpolated values of the normal and eye-ray vectors and use them to evaluate the Phong lighting equation. Even if the normal vector at each vertex is a unit vector, the result of interpolating these will generally not be a unit vector. That’s why we didn’t bother normalizing them in the vertex shader: We’ll need to do a normalization at each pixel anyhow. After normalizing these, we compute the reflected eye vector $\mathbf{r}$, and use it in the Phong equation to evaluate the pixel color. Note the use of max (line 32) to eliminate the case where the reflected eye vector is not in the same half-space as the ray to the light source. (See Listing 33.6.)

# Listing 33.6: The fragment shader for the Phong shading program.

```
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
```