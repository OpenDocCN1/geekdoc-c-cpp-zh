
Assuming that we use the method whereby a shadow texture has been attached to our custom framebuffer, OpenGL provides some relatively simple tools for determining whether each pixel is in shadow as we draw the objects. Here is a summary of the details handled in pass two:

- Build the "B" transform matrix for converting from light to texture space (actually, this is more appropriately done in init()).
- Enable the shadow texture for lookup.
- Enable color output.
- Enable the GLSL pass two rendering program, containing both vertex and fragment shaders.
- Build the MVP matrix for the object being drawn based on the camera position (as normal).
- Build the shadowMVP2 matrix (incorporating the B matrix, as described earlier)—the shaders will need it to look up pixel coordinates in the shadow texture.
- Send the matrix transforms to shader uniform variables.
- Enable buffers containing vertices, normal vectors, and texture coordinates (if used), as usual.
- Call glDrawArrays().

In addition to their rendering duties, the vertex and fragment shaders have additional tasks:

- The vertex shader converts vertex positions from camera space to light space and sends the resulting coordinates to the fragment shader in a vertex attribute so that they will be interpolated. This makes it possible to retrieve the correct values from the shadow texture.
- The fragment shader calls the textureProj() function, which returns a 0 or 1 indicating whether or not the pixel is in shadow (this mechanism is explained later). If it is in shadow, the shader outputs a darker pixel by not including its diffuse and specular contributions.

Shadow mapping is such a common task that GLSL provides a special type of sampler variable called a sampler2DShadow (as previously mentioned) that can be attached to a shadow texture in the C++/OpenGL application. The textureProj() function is used to look up values from a shadow texture, and it is similar to texture() that we saw previously in Chapter 5, except that it uses a vec3 to index the texture rather than the usual vec2. Since a pixel coordinate is a vec4, it is necessary to project that onto 2D texture space in order to look up the depth value in the shadow texture map. As we will see in the following, textureProj() does all of this for us.

The remainder of the vertex and fragment shader code implements Blinn-Phong shading. These shaders are shown in Figures 8.6 and 8.7, with the added code for shadow mapping highlighted.

Let’s examine more closely how we use OpenGL to perform the depth comparison between the pixel being rendered and the value in the shadow texture. We start in the vertex shader with vertex coordinates in model space, which we multiply by shadowMVP2 to produce shadow texture coordinates that correspond to vertex coordinates projected into light space, previously generated from the light’s point of view. The interpolated (3D) light space coordinates (x,y,z) are used in the fragment shader as follows.

```glsl
#version 430
layout (location=0) in vec3 vertPos;
layout (location=1) in vec3 vertNormal;

out vec3 varyingNormal, varyingLightDir, varyingVertPos, varyingHalfVec;
out vec4 shadow_coord;

struct PositionalLight { vec4 ambient, diffuse, specular; vec3 position; };
struct Material { vec4 ambient, diffuse, specular; float shininess; };
uniform vec4 globalAmbient;
uniform PositionalLight light;       // light's position is assumed to be in eye space
uniform Material material;
uniform mat4 mv_matrix;
uniform mat4 proj_matrix;
uniform mat4 norm_matrix;
uniform mat4 shadowMVP2;
layout (binding=0) uniform sampler2DShadow shTex;

void main(void)
{
    varyingVertPos = (mv_matrix * vec4(vertPos,1.0)).xyz;
    varyingLightDir = light.position - varyingVertPos;
    varyingNormal = (norm_matrix * vec4(vertNormal,1.0)).xyz;
    varyingHalfVec = (varyingLightDir + varyingVertPos).xyz;
    shadow_coord = shadowMVP2 * vec4(vertPos,1.0);
    gl_Position = proj_matrix * mv_matrix * vec4(vertPos,1.0);
}
```

**Figure 8.6**  
Shadow mapping pass 2 vertex shader.

```glsl
#version 430
in vec3 varyingNormal, varyingLightDir, varyingVertPos, varyingHalfVec;
in vec4 shadow_coord;
out vec4 fragColor;

// same structs and uniforms as in the vertex shader
. . .
void main(void)
{  vec3 L = normalize(varyingLightDir);
   vec3 N = normalize(varyingNormal);
   vec3 V = normalize(varyingVertPos);
   vec3 H = normalize(varyingHalfVec);

   float notInShadow = textureProj(shTex, shadow_coord);
   fragColor = globalAmbient * material.ambient + light.ambient * material.ambient;
   if(notInShadow == 1.0)
   {  fragColor += light.diffuse * material.diffuse * max(dot(L,N),0.0)
         + light.specular * material.specular
         * pow(max(dot(H,N),0.0),material.shininess*3.0);
   }
}
```

**Figure 8.7**  
Shadow mapping pass 2: fragment shader.

The z component represents the distance from the light to the pixel. The (x,y) components are used to retrieve the depth information stored in the (2D) shadow texture. This retrieved value (the distance to the object nearest the light) is compared with z. This comparison produces a “binary” result that tells us whether the pixel we are rendering is further from the light than the object nearest the light (i.e., whether the pixel is in shadow).

If in OpenGL we use glFramebufferTexture() as described earlier, and we enable *depth testing*, then using a sampler2DShadow and *textureProj()* as shown in the fragment shader (Figure 8.7) will do exactly what we need. That is, *textureProj()* will output either 0.0 or 1.0 depending on the depth comparison. Based on this value, we can then in the fragment shader omit the diffuse and specular contributions when the pixel is further from the light than the object nearest the light, effectively creating the shadow when appropriate. An overview is shown in Figure 8.8.

We are now ready to build our C++/OpenGL application to work with the previously described shaders.

![](img/1695de1bc7486362f86c143285f3fb40_219_0.png)

## 8.8 A SHADOW MAPPING EXAMPLE

Consider the scene in Figure 8.9 that includes a torus and a pyramid. A positional light has been placed on the left (note the specular highlights).

The pyramid *should* be casting a shadow on the torus.

![](img/1695de1bc7486362f86c143285f3fb40_219_1.png)

To clarify the development of the example, our first step will be to *render pass one to the screen* to make sure it is working properly. To do this, we will temporarily add a simple fragment shader (it will not be included in the final version) to pass one that just outputs a constant color (e.g., red); for example:

```glsl
#version 430
out vec4 fragColor;
void main(void)
{ fragColor = vec4(1.0, 0.0, 0.0, 0.0);
}
```

Let’s assume that the origin of the previous scene is situated at the center of the figure, in between the pyramid and the torus. In pass one we place the camera at the light’s position (at the left in Figure 8.10) and point it toward (0,0,0). If we then draw the objects in red, it produces the output shown at the right in Figure 8.10. Note the torus near the top—from this vantage point it is partially behind the pyramid.

![](img/1695de1bc7486362f86c143285f3fb40_220_0.png)

**Figure 8.10**  
Pass one: Scene (left) from light’s point of view (right).

The complete two-pass C++/OpenGL code with lighting and shadow mapping is shown in Program 8.1.

### Program 8.1 Shadow Mapping

```cpp
// Much is the same as we have seen before. New sections to support shadows are highlighted.
// The imports necessary for lighting, etc., would be included at the start, as are the same as before,
// and are not shown here.

// variable declarations for rendering programs, buffers, shader sources, etc., would go here.
...
ImportedModel pyramid("pyr.obj");            // define the pyramid
Torus myTorus(0.6f, 0.4f, 48);               // define the torus
int numPyramidVertices, numTorusVertices, numTorusIndices;

...
// locations of torus, pyramid, camera, and light
glm::vec3 torusLoc(1.6f, 0.0f, -0.3f);
glm::vec3 pyrLoc(-1.0f, 0.1f, 0.3f);
glm::vec3 cameraLoc(0.0f, 0.2f, 6.0f);
glm::vec3 lightLoc(-3.8f, 2.2f, 1.1f);

// properties of white light (global and positional) used in this scene
float globalAmbient[4] = { 0.7f, 0.7f, 0.7f, 1.0f };
float lightAmbient[4] = { 0.0f, 0.0f, 0.0f, 1.0f };
float lightDiffuse[4] = { 1.0f, 1.0f, 1.0f, 1.0f };
float lightSpecular[4] = { 1.0f, 1.0f, 1.0f, 1.0f };
```
