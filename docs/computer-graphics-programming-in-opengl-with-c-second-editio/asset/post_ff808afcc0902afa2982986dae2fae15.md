
```cpp
void main(void)
{
    // note that it is no longer necessary to compute R in the fragment shader
    vec3 L = normalize(varyingLightDir);
    vec3 N = normalize(varyingNormal);
    vec3 V = normalize(-varyingVertPos);
    vec3 H = normalize(varyingHalfVector);

    ...
    // get angle between the normal and the halfway vector
    float cosPhi = dot(H,N);

    // halfway vector H was computed in the vertex shader, and then interpolated by the rasterizer
    vec3 ambient = ((globalAmbient * material.ambient) + (light.ambient * material.ambient)).xyz;
    vec3 diffuse = light.diffuse.xyz * material.diffuse.xyz * max(cosTheta,0.0);
    vec3 specular =
        light.specular.xyz * material.specular.xyz * pow(max(cosPhi,0.0), material.shininess*3.0);
        // the multiplication by 3.0 at the end is a “tweak” to improve the specular highlight.
    fragColor = vec4((ambient + diffuse + specular), 1.0);
}
```

![](img/1695de1bc7486362f86c143285f3fb40_202_0.png)

Figure 7.16 shows two examples of the effect of Phong shading on more complex externally generated models. The top image shows a rendering of an OBJ model of a dolphin created by Jay Turberville at Studio 522 Productions [TU16]. The bottom image is a rendering of the well-known “Stanford Dragon,” the result of a 3D scan of an actual figurine, done in 1996 [ST96]. Both models were rendered using the “gold” material we placed in our “Utils.cpp” file. The Stanford dragon is widely used for testing graphics algorithms and hardware because of its size—it contains over 800,000 triangles.

**Figure 7.16**  
External models with Phong shading.

### 7.6 COMBINING LIGHTING AND TEXTURES

So far, our lighting model has assumed that we are using lights with specified ADS values to illuminate objects made of material that has also been defined with ADS values. However, as we saw in Chapter 5, some objects may instead have surfaces defined by texture images. Therefore, we need a way of combining colors retrieved by sampling a texture and colors produced from a lighting model.

The manner in which we combine lighting and textures depends on the nature of the object and the purpose of its texture. There are several scenarios, a few of which include:

- The texture image very closely reflects the actual appearance of the object's surface.
- The object has both a material and a texture.
- The texture contains shadow or reflection information (covered in Chapters 8 and 9).
- There are multiple lights and/or multiple textures involved.

Let's consider the first case, where we have a simple textured object and we wish to add lighting to it. One simple way of accomplishing this in the fragment shader is to remove the material specification entirely, and to use the texel color returned from the texture sampler in place of the material ADS values. The following is one such strategy (expressed in pseudocode):

```
fragColor = textureColor * ( ambientLight + diffuseLight ) + specularLight
```

Here the texture color contributes to the ambient and diffuse computation, while the specular color is defined entirely by the light. It is common to set the specular contribution solely based on the light color, especially for metallic or “shiny” surfaces. However, some less shiny surfaces, such as cloth or unvarnished wood (and even a few metals, such as gold) have specular highlights that include the color of the object surface. In those cases, a suitable slightly modified strategy would be:

```
fragColor = textureColor * ( ambientLight + diffuseLight + specularLight )
```

There are also cases in which an object has an ADS material that is supplemented by a texture image, such as an object made of silver that has a texture that adds some tarnish to the surface. In those situations, the standard ADS model with both light and material, as described in previous sections, can be combined with the texture color using a weighted sum. For example:

```
textureColor = texture(sampler, texCoord)
lightColor = (ambLight * ambMaterial) + (diffLight * diffMaterial) + specLight
fragColor = 0.5 * textureColor + 0.5 * lightColor
```

This strategy for combining lighting, materials, and textures can be extended to scenes involving multiple lights and/or multiple textures. For example:

```
texture1Color = texture(sampler1, texCoord)
texture2Color = texture(sampler2, texCoord)

light1Color = (ambLight1 * ambMaterial) + (diffLight1 * diffMaterial) + specLight1
light2Color = (ambLight2 * ambMaterial) + (diffLight2 * diffMaterial) + specLight2

fragColor = 0.25 * texture1Color
          + 0.25 * texture2Color
          + 0.25 * light1Color
          + 0.25 * light2Color
```

Figure 7.17 shows the Studio 522 Dolphin with a UV-mapped texture image (produced by Jay Turberville [TU16]), and the NASA shuttle model we saw earlier in Chapter 6. Both textured models are enhanced with Blinn-Phong lighting, without the inclusion of materials, and with specular highlights that utilize light only. In both cases, the relevant output color computation in the fragment shader is:

```
vec4 texColor = texture(sampler, texCoord);
fragColor = texColor * (globalAmbient + lightAmb + lightDiff * max(dot(L,N),0.0))
          + lightSpec * pow(max(dot(H,N),0.0), matShininess*3.0);
```

Note that it is possible for the computation that determines fragColor to produce values greater than 1.0. When that happens, OpenGL clamps the computed value to 1.0.

### SUPPLEMENTAL NOTES

![](img/1695de1bc7486362f86c143285f3fb40_205_0.png)

![](img/1695de1bc7486362f86c143285f3fb40_205_1.png)

**Figure 7.17**  
Combining lighting and textures.

The faceted-shaded torus shown in Figure 7.7 was created by adding the “flat” interpolation qualifier to the corresponding normal vector vertex attribute declarations in the vertex and fragment shaders. This instructs the rasterizer to not perform interpolation on the specified variable and instead assign the same value for each fragment (by default it chooses the value associated with the first vertex in the triangle). In the Phong shading example, this could be done as follows:

```
flat out vec3 varyingNormal;    in the vertex shader, and
flat in vec3 varyingNormal;     in the fragment shader.
```

An important kind of light source that we haven’t discussed is a *distributed light* or *area light*, which is a light that is characterized by having a source that

## Chapter 8: Shadows

- 8.1 The Importance of Shadows ........................................ 189
- 8.2 Projective Shadows ................................................ 190
- 8.3 Shadow Volumes ................................................... 191
- 8.4 Shadow Mapping ................................................... 192
- 8.5 A Shadow Mapping Example ......................................... 199
- 8.6 Shadow Mapping Artifacts ......................................... 205
- 8.7 Soft Shadows ..................................................... 208
- Supplemental Notes ................................................... 216

### 8.1 THE IMPORTANCE OF SHADOWS

In Chapter 7, we learned how to add lighting to our 3D scenes. However, we didn’t actually add light; instead, we simulated the effects of light on objects—using the ADS model—and modified how we drew those objects accordingly.

The limitations of this approach become apparent when we use it to light more than one object in the same scene. Consider the scene in Figure 8.1, which includes both our brick-textured torus and a ground plane (the ground plane is the top of a giant cube with a grass texture from [LU16]).

![](img/1695de1bc7486362f86c143285f3fb40_209_0.png)

At first glance our scene may appear reasonable. However, closer examination reveals that there is something very important missing. In particular, it is impossible to discern the distance between the torus and the large textured cube below it. Is the torus floating above the cube, or is it resting on top of the cube?
