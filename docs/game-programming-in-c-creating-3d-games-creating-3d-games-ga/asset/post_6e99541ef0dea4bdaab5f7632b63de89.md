
translation is just based on the position of the light,
which comes from the owning actor.

Furthermore, you need to set the different uniforms for
this specific point light, which isn’t different from how
you’ve set the uniforms before. Finally, the
`glDrawElements` call draws the light geometry for the
point light, which is your sphere mesh. You don’t need to
set the vertex array as active because the `Renderer` does
this before calling `Draw`.

Once you draw all the point light meshes, for every
fragment you calculate the contribution of the point light
to the color of the fragment. You then add this additional
light color to the already existing color from the global
lighting pass.

### Listing 13.15 PointLightComponent::Draw Implementation

Click here to view code image

```
void PointLightComponent::Draw(Shader* shader, Mesh* mesh)
{
// Scale world transform to the outer radius (divide
// the mesh radius) and positioned to the world position
Matrix4 scale = Matrix4::CreateScale(mOwner->GetScale() * mOuterRadius / mesh->GetRadius());
Matrix4 trans = Matrix4::CreateTranslation(mOwner->GetPosition());

Matrix4 worldTransform = scale * trans;

shader->SetMatrixUniform("uWorldTransform", worldTransform);

// Set point light shader constants

shader->SetVectorUniform("uPointLight.mWorldPos", mOwner->GetPosition());
shader->SetVectorUniform("uPointLight.mDiffuseColor", mDiffuseColor);
shader->SetFloatUniform("uPointLight.mInnerRadius", mInnerRadius);
shader->SetFloatUniform("uPointLight.mOuterRadius", mOuterRadius);

// Draw the sphere

glDrawElements(GL_TRIANGLES, mesh->GetVertexArray(), GL_UNSIGNED_INT, nullptr);
}
```

To demonstrate the point light rendering, this chapter's game project creates several point lights with different colors along the floor. Figure 13.10 illustrates these point lights, powered by deferred shading.

![](img/e9afcec1487716b0ef80d7e7c09869c8_900_0.png)

Figure 13.10 Numerous point lights in the game project

## Improvements and Issues

Although deferred shading is a very powerful rendering technique used by many modern games, it isn’t perfect. One problem is that it can’t handle partially transparent objects such as windows. Because the G-buffer can only store a single surface’s properties, drawing such an object into the G-buffer would overwrite the objects behind it. The solution for this case is to draw transparent objects in a separate pass after drawing the rest of the scene.

Also, for some types of games, the overhead of setting up the G-buffer and rendering to multiple targets is not worth it. If a game takes place largely during the day or has a very small number of lights, the cost of the deferred shading setup every frame might be higher than the cost of a forward-rendering approach. Many virtual-reality games, which need a very high frame rate, use forward rendering for this reason.

Another issue is that the light geometry has many edge cases to consider and fix. For example, if the point light sphere partially intersects with a wall, the point light will affect both sides of the wall in the current approach. Also, if you create a very big point light but place the camera inside the light, you don't see the effect of that light. To fix these light geometry issues, you need to use a stencil buffer, which is a different type of output buffer.

## GAME PROJECT

This chapter's game project provides the full implementation of deferred shading. In addition, it uses both mipmapping and anisotropic aliasing to improve texture quality. The project includes the mirror texture that's forward rendered. The code is available in the book's GitHub repository, in the Chapter13 directory. Open Chapter13-windows.sln in Windows and Chapter13-mac.xcodeproj on Mac.

There are no changes to the controls or character from the previous chapter. The player still uses the WASD keys to move the character around. To demonstrate the point lights, several point lights are provided in Game::LoadData.

## SUMMARY

This chapter covers a handful of intermediate graphics techniques. First, it looks at how texture filtering works—both nearest-neighbor filtering and bilinear filtering. Mipmapping can reduce sampling artifacts when reducing the size of textures because it generates several lower-resolution textures. However, for oblique surfaces, mipmapping may appear blurry. In this case, anisotropic filtering improves the quality of the textures.

Another powerful technique is rendering the scene to textures. OpenGL allows creation of arbitrary framebuffer objects associated with textures. Then, you can choose to draw the 3D scene to this texture. One use of this technique is to draw a high-quality reflection, such as for a mirror.

Finally, this chapter explores deferred shading, which is a two-pass approach to lighting. In the first pass, you write the object's surface properties, such as diffuse color, normals, and world position, into a G-buffer. In the second pass, you read from the G-buffer to calculate lighting equations. For lights with limited ranges, such as point lights, you render lighting geometry to ensure that the light affects only the fragments in range. Deferred shading is an excellent approach when there are many lights in the scene, though there are some issues, such as the inability to handle partially transparent objects.

## ADDITIONAL READING

As mentioned in Chapter 6, Real-Time Rendering by Thomas Akenine-Moller et al. is the go-to book when it comes to rendering techniques and games. Jason Zink et al. give a good overview of many techniques, including deferred shading, even though the book focuses on Direct3D 11 instead of OpenGL. Matt Pharr et al. cover physically based rendering, which is a newer technique games use to achieve more realistic lighting. Wolfgang Engel's books are always on the cutting edge of what graphics programmers in the video game industry are using. Phil Djonov discusses how to eliminate the need for the world position in the G-buffer. Finally, sometimes to understand how various OpenGL extensions work, you need to read the official registry.

- Akenine-Moller, Thomas, Eric Haines, and Naty Hoffman. Real-Time Rendering, 3rd edition. Natick: A K Peters, 2008.
- Djonov, Phil. “Deferred Shading Tricks.” Shiny Pixels. Accessed November 26, 2017. http://vec3.ca/code/graphics/deferred-shading-tricks/.
- Engel, Wolfgang, ed. GPU Zen: Advanced Rendering Techniques. Encinitas: Black Cat Publishing, 2017.
- Khronos Group. OpenGL Extensions Registry. Accessed October 16, 2017. https://github.com/KhronosGroup/OpenGL-Registry.

Pharr, Matt, Wenzel Jakob, and Greg Humphreys. Physically Based Rendering: From Theory to Implementation, 3rd edition. Cambridge: Elsevier, 2017.

Zink, Jason, Matt Pettineo, and Jack Hoxley. Practical Rendering and Computation with Direct3D 11. Boca Raton: CRC Press, 2012.

## EXERCISES

In this chapter's exercises, you explore improving the deferred shading techniques covered in the latter half of the chapter.

### Exercise 13.1

Add support for the specular component to both the global G-buffer lighting (the directional light) and the point lights. To do this, first you need a new texture in the G-buffer that stores the specular power of the surface. Add this new texture to the relevant parts of code (both in C++ and in GLSL).

Next, change the PointLightComponent class, the PointLightComponent::Draw function, and the shader code for point lights and the global light. For the point lights, use the intensity to interpolate the specular color, as is done for the diffuse color. Calculate the specular component according to the Phong equations, as before.

### Exercise 13.2

Adding a new type of light to deferred shading requires a new type of light geometry. Add support for spotlights. To do so, you need to create a SpotLightComponent as well as a corresponding shader to draw these lights after the point lights.

Use the provided SpotLight.gpmesh file (which is a cone) as the mesh for spotlights. A spotlight should have parameters like those of a point light, but it also needs a variable for its angle. To be able to change the angle, the mesh needs to also scale non-uniformly. The default mesh has a half angle of 30 degrees.
