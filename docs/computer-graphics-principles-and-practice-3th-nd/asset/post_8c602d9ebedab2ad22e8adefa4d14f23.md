
- Arguments that are constant over all triangles are passed as global (“uniform”) variables.
- Points, vectors, and colors are all stored in `vec3` type.
- `const` has different semantics (compile-time constant).
- `in`, `out`, and `inout` are used in place of C++ reference syntax.
- `length`, `dot`, etc. are functions instead of methods on vector classes.

### Listing 15.32: Vertex shader for projecting vertices.

*The output is in homogeneous space before the division operation. This corresponds to the `perspectiveProject` function from Listing 15.24.*

```glsl
#version 130

// Triangle vertices
in vec3 vertex;
in vec3 normal;

// Camera and screen parameters
uniform float fieldOfViewX;
uniform float zNear;
uniform float zFar;
uniform float width;
uniform float height;

// Position to be interpolated
out vec3 Pinterp;

// Normal to be interpolated
out vec3 ninterp;

vec4 perspectiveProject(in vec3 P) {
    // Compute the side of a square at z = -1 based on our
    // horizontal left-edge-to-right-edge field of view.
    float s = -2.0 * tan(fieldOfViewX * 0.5f);
    float aspect = height / width;

    // Project onto z = -1
    vec4 Q;
    Q.x = 2.0 * -P.x / s;
    Q.y = 2.0 * -P.y / (s * aspect);
    Q.z = 1.0;
    Q.w = -P.z;

    return Q;
}

void main() {
    Pinterp = vertex;
    ninterp = normal;

    gl_Position = perspectiveProject(Pinterp);
}
```

None of these affect the expressiveness or performance of the basic language. The specifics of shading-language syntax change frequently as new versions are released, so don’t focus too much on the details. The point of this example is how the overall form of our original program is preserved but adjusted to the conventions of the hardware API.

Under the OpenGL API, the outputs of a vertex shader are a set of attributes and a vertex of the form $(x, y, a, -z)$. That is, a homogeneous point for which the perspective division has not yet been performed. The value $a/-z$ will be used for the depth test. We choose $a = 1$ so that the depth test is performed on $-1/z$, which is a positive value for the negative $z$ locations that will be visible to the camera. We previously saw that any function that provides a consistent depth ordering can be used for the depth test. We mentioned that distance along the eye ray, $-z$, and $-1/z$ are common choices. Typically one scales the $a$ value such that $-a/z$ is in the range $[0, 1]$ or $[-1, 1]$, but for simplicity we’ll omit that here. See Chapter 13 for the derivation of that transformation.

Note that we did not scale the output vertex to the dimensions of the image, negate the $y$-axis, or translate the origin to the upper left in screen space, as we did for the software renderer. That is because by convention, OpenGL considers the upper-left corner of the screen to be at $(-1, 1)$ and the lower-right corner at $(1, -1)$.

We choose the 3D position of the vertex and its normal as our attributes. The hardware rasterizer will automatically interpolate these across the surface of the triangle in a perspective-correct manner. We need to treat the vertex as an attribute because OpenGL does not expose the 3D coordinates of the point being shaded.

Listings 15.33 and 15.34 give the pixel shader code for the shade routine, which corresponds to the shade function from Listing 15.17, and helper functions that correspond to the `visible` and `BSDF::evaluateFiniteScatteringDensity` routines from the ray tracer and software rasterizer. The output of the shader is in homogeneous space before the division operation. This corresponds to the `perspectiveProject` function from Listing 15.24. The interpolated attributes enter the shader as global variables `Pinterp` and `ninterp`. We then perform shading in exactly the same manner as for the software renderers.

### Listing 15.33: Pixel shader for computing the radiance scattered toward the camera from one triangle illuminated by one light.

```glsl
#version 130
// BSDF
uniform vec3    lambertian;
uniform vec3    glossy;
uniform float   glossySharpness;

// Light
uniform vec3    lightPosition;
uniform vec3    lightPower;

// Pre-rendered depth map from the light’s position
uniform sampler2DShadow shadowMap;

// Point being shaded. OpenGL has automatically performed
// homogeneous division and perspective-correct interpolation for us.
in vec3         Pinterp;
in vec3         ninterp;

// Value we are computing
out vec3        radiance;

// Normalize the interpolated normal; OpenGL does not automatically
// renormalize for us.
vec3 n = normalize(ninterp);

vec3 shade(const in vec3 P, const in vec3 n) {
    vec3 radiance             = vec3(0.0);

    // Assume only one light
    vec3 offset               = lightPosition - P;
    float distanceToLight     = length(offset);
    vec3 w_i                  = offset / distanceToLight;
    vec3 w_o                  = -normalize(P);

    if (visible(P, w_i, distanceToLight, shadowMap)) {
        vec3 L_i = lightPower / (4 * PI * distanceToLight * distanceToLight);

        // Scatter the light.
        radiance +=
            L_i *
            evaluateFiniteScatteringDensity(w_i, w_o) *
            max(0.0, dot(w_i, n));
    }

    return radiance;
}

void main() {
    vec3 P = Pinterp;

    radiance = shade(P, n);
}
```

### Listing 15.34: Helper functions for the pixel shader.

```glsl
#define PI 3.1415927

bool visible(const in vec3 P, const in vec3 w_i, const in float distanceToLight,
            sampler2DShadow shadowMap) {
    return true;
}

/* Returns f(wi, wo). Same as BSDF::evaluateFiniteScatteringDensity
   from the ray tracer. */
vec3 evaluateFiniteScatteringDensity(const in vec3 w_i, const in vec3 w_o) {
    vec3 w_h = normalize(w_i + w_o);

    return (k_L +
            k_G * ((s + 8.0) * pow(max(0.0, dot(w_h, n)), s) / 8.0)) / PI;
}
```

However, there is one exception. The software renderers iterated over all the lights in the scene for each point to be shaded. The pixel shader is hardcoded to accept a single light source. That is because processing a variable number of arguments is challenging at the hardware level. For performance, the inputs to shaders are typically passed through registers, not heap memory. Register allocation is generally a major factor in optimization. Therefore, most shading compilers require the number of registers consumed to be known at compile time, which precludes passing variable length arrays. Programmers have developed three **forward-rendering** design patterns for working within this limitation. These use a single framebuffer and thus limit the total space required by the algorithm. A fourth and currently popular **deferred-rendering** method requires additional space.

- 1. **Multipass Rendering:** Make one **pass** per light over all geometry, summing the individual results. This works because light combines by superposition. However, one has to be careful to resolve visibility correctly on the first pass and then never alter the depth buffer. This is the simplest and most elegant solution. It is also the slowest because the overhead of launching a pixel shader may be significant, so launching it multiple times to shade the same point is inefficient.
- 2. **Ubershader:** Bound the total number of lights, write a shader for that maximum number, and set the unused lights to have zero power. This is one of the most common solutions. If the overhead of launching the pixel shader is high and there is significant work involved in reading the BSDF parameters, the added cost of including a few unused lights may be low. This is a fairly straightforward modification to the base shader and is a good compromise between performance and code clarity.
- 3. **Code Generation:** Generate a set of shading programs, one for each number of lights. These are typically produced by writing another program that automatically generates the shader code. Load *all* of these shaders at runtime and bind whichever one matches the number of lights affecting a particular object. This achieves high performance if the shader only needs to be swapped a few times per frame, and is potentially the fastest method. However, it requires significant infrastructure for managing both the source code and the compiled versions of all the shaders, and may actually be slower than the conservative solution if changing shaders is an expensive operation.

If there are different BSDF terms for different surfaces, then we have to deal with all the permutations of the number of lights and the BSDF variations. We again choose between the above three options. This combinatorial explosion is one of the primary drawbacks of current shading languages, and it arises directly from the requirement that the shading compiler produce efficient code. It is not hard to design more flexible languages and to write compilers for them. But our motivation for moving to a hardware API was largely to achieve increased performance, so we are unlikely to accept a more general shading language if it significantly degrades performance.

- 4. **Deferred Lighting:** A deferred approach that addresses these problems but requires more memory is to separate the computation of **which** point will color each pixel from illumination computation. An initial rendering pass renders many parallel buffers that encode the shading coefficients, surface normal, and location of each point (often, assuming an ubershader). Subsequent passes then iterate over the screen-space area conservatively affected by each light, computing and summing illumination. Two common structures for those lighting passes are multiple lights applied to large screen-space tiles and ellipsoids for individual lights that cover the volume within which their contribution is non-negligible.

For the single-light case, moving from our own software rasterizer to a hardware API did not change our **perspectiveProject** and **shade** functions substantially.

However, our shade function was not particularly powerful. Although we did not choose to do so, in our software rasterizer, we could have executed arbitrary code inside the shade function. For example, we could have written to locations other than the current pixel in the frame buffer, or cast rays for shadows or reflections. Such operations are typically disallowed in a hardware API. That is because they interfere with the implementation's ability to efficiently schedule parallel instances of the shading programs in the absence of explicit (inefficient) memory locks.
