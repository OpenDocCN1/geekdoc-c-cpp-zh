```
```cpp
void Renderer::DrawFromBuffer()
{
    // Disable depth testing for the global lighting pass
    glDisable(GL_DEPTH_TEST);

    // Activate global G-Buffer shader
    mGlobalShader->SetActive();

    // Activate sprite verts quad
    mSpriteVerts->Activate();

    // Set the G-buffer textures to sample
    mBuffer->SetTexturesActive();

    // Set the lighting uniforms
    SetLightUniforms(mGlobalShader, mView);

    // Draw the triangles for the quad
    glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, nullptr);
}
```
```