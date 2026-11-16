
![](img/e9afcec1487716b0ef80d7e7c09869c8_470_0.png)

### Figure 6.11 Phong reflection model

The **ambient component** is the overall illumination of the scene. Thus, it makes sense to directly tie the ambient component to the ambient light. Because ambient light applies evenly to the entire scene, the ambient component is independent of any other lights and the camera.

The **diffuse component** is the primary reflection of light off the surface. Any directional lights, point lights, or spotlights affecting the object affect the diffuse component. The diffuse component calculation uses both the normal of the surface and a vector from the surface to the light. The position of the camera does not affect the diffuse component.

The final component in the Phong model is the **specular component**. This approximates shiny reflections off a surface. An object with a high degree of specularity, such as a polished metal object, has stronger highlights than an object painted in matte black. As with the diffuse component, the specular component depends on both the light vector and the normal of the surface. However, specularity also depends on the position of the camera. This is because looking at a shiny object from different angles changes the perceived reflections.

Figure 6.12 shows the Phong reflection from a side view. Computing Phong reflection requires a series of calculations that include several variables:

- \(\hat{n}\)—Normalized surface normal
- \(\hat{l}\)—Normalized vector from the surface to the light
- \(\hat{v}\)—Normalized vector from the surface to the camera (eye) position
- \(\hat{r}\)—Normalized reflection of \(-\hat{l}\) about \(\hat{n}\)
- \(\alpha\)—Specular power (which determines the shininess of the object)

In addition, there are colors for the lights:

- \(k_a\)—Ambient color
- \(k_d\)—Diffuse color
- \(k_s\)—Specular color

![](img/e9afcec1487716b0ef80d7e7c09869c8_471_0.png)

### Figure 6.12 Diagram of Phong reflection calculations (vectors not to scale)

In the Phong reflection model, you calculate the light applied to a surface as follows:

```
Ambient = k_a
Diffuse = k_d(\hat{n} \cdot \hat{l})
Specular = k_s(\hat{r} \cdot \hat{v})^\alpha
Phong = Ambient + \sum_{\forall lights} \begin{cases} Specular + Diffuse & \text{if } \hat{n} \cdot \hat{l} > 0 \\ 0 & \text{otherwise} \end{cases}
```

```
Ambient = k_a
Diffuse = k_d(\hat{n} \cdot \hat{l})
Specular = k_s(\hat{r} \cdot \hat{v})^\alpha
Phong = Ambient
+ \sum_{\forall light} \begin{cases} Specular + Diffuse & \text{if } \hat{n} \cdot \hat{l} > 0 \\ 0 & \text{otherwise} \end{cases}
```

Note that the diffuse and specular component computes for all lights in the scene, but there's only one ambient component. The \(\hat{n} \cdot \hat{l}\) test ensures that the light affects only surfaces facing the light.

In any event, the Phong equation as described here yields a color for all lights in the scene. The final color of the surface is the light color multiplied by the color of the surface. Because both the light and surface color are RGB values, you use component-wise multiplication.

A more complex implementation separates the surface color into separate ambient, diffuse, and specular colors. In this implementation, the equations change to multiply each separate color by each component rather than only one multiplication at the end.

One remaining question is how frequently to compute the BRDF. There are three common options: once per surface (**flat shading**), once per vertex (**Gouraud shading**), or once per pixel (**Phong shading**). Although per-pixel lighting is more computationally expensive, modern graphics hardware can easily handle it. It's conceivable that some games might choose other types of shading for aesthetic reasons, but this chapter sticks to per-pixel lighting.

## Implementing Lighting

This section covers how to add ambient and directional lights to the game. Implementing this requires changes to both the vertex and fragment shaders. The `BasicMesh.vert/.frag` shaders are a starting point for the new `Phong.vert/.frag` shaders. (Remember that this shader code is in GLSL, not C++) You'll then change it so all meshes use this new Phong shader.

Because the lighting is per pixel, the Phong fragment shader needs several additional uniforms: a camera position, an ambient light color, and several variables for a directional light (see Listing 6.10).

### Listing 6.10 Phong.frag Lighting Uniforms

Click here to view code image

```
// Create a struct for directional light
struct DirectionalLight
{
    // Direction of light
    vec3 mDirection;
    // Diffuse color
    vec3 mDiffuseColor;
    // Specular color
    vec3 mSpecColor;
};

// Uniforms for lighting
// Camera position (in world space)
uniform vec3 uCameraPos;
// Ambient light level
uniform vec3 uAmbientLight;
// Specular power for this surface
uniform float uSpecPower;
// Directional Light (only one for now)
uniform DirectionalLight uDirLight;
```

Note the declaration of a `DirectionalLight` struct. GLSL supports struct declarations, much like those in C/C++. Next, you declare a corresponding `DirectionalLight` struct in the C++ code and add two member variables to `Renderer` for the ambient light and directional light.

Back in C++, the `glUniform3fv` and `glUniform1f` functions set 3D vector and float uniforms, respectively. You create two new functions in `Shader`, `SetVectorUniform` and `SetFloatUniform`, to call these functions. The implementation of both these functions is like that of the `SetMatrixUniform` function in Chapter 5.

A new function in `Renderer` called `SetLightUniforms` handles setting the new uniform values:

Click here to view code image

```
void Renderer::SetLightUniforms(Shader* shader)
{
    // Camera position is from inverted view
    Matrix4 invView = mView;
    invView.Invert();
    shader->SetVectorUniform("uCameraPos", invView.Get
// Ambient light
shader->SetVectorUniform("uAmbientLight", mAmbient
// Directional light
shader->SetVectorUniform("uDirLight.mDirection", m
shader->SetVectorUniform("uDirLight.mDiffuseColor"
mDirLight.mDiffuseColor);
shader->SetVectorUniform("uDirLight.mSpecColor", m
}
```

Note that this function uses dot notation to reference specific members of the uDirLight struct.

Extracting the camera position from the view matrix requires inverting the view matrix. After inverting the view matrix, the first three components of the fourth row (returned by the GetTranslation member function) correspond to the world space position of the camera.

Next, you update the gpmesh file format so that you can specify the specular power of a mesh's surface with the specularPower property. You then update the Mesh::Load code to read in this property, and set the uSpecPower uniform in MeshComponent::Draw right before drawing the mesh.

Back in GLSL, you must make some changes to the vertex shader in Phong.vert. Both the camera position and the directional light's direction are in world space. However, the gl_Position computed in the vertex shader is in clip space. Getting the correct vector from the surface to the camera requires a position in world space. Furthermore, the input vertex normals are in object space, but they also need to be in world space. This means the vertex shader must compute both the world space normal and the world space position and send these to the fragment shader via out variables:

```
// Normal (in world space)
out vec3 fragNormal;

// Position (in world space)
out vec3 fragWorldPos;
```

Similarly, you declare fragNormal and fragWorldPos as in variables in the fragment shader. Next, the main function of the vertex shader, in Listing 6.11, computes both fragNormal and fragWorldPos. The .xyz syntax, known as a swizzle, is a shorthand for extracting the x, y, and z components from a 4D vector and creating a new 3D vector with those values. This effectively converts between a vec4 and vec3.

The code also converts the normal into homogenous coordinates so that multiplication by the world transform matrix works. However, the w component
