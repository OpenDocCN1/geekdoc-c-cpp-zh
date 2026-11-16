```
void Renderer::Draw3DScene(unsigned int framebuffer,
    const Matrix4x4 view, const Matrix4x4 proj,
    float viewportScale)
{
    // Set the current framebuffer
    glBindFramebuffer(GL_FRAMEBUFFER, framebuffer);

    // Set viewport size based on scale
    glViewport(0, 0,
        static_cast<int>(mScreenWidth * viewPortScale),
        static_cast<int>(mScreenHeight * viewPortScale)
    );

    // Clear color buffer/depth buffer
    glClearColor(0.0f, 0.0f, 0.0f, 1.0f);
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

    // Draw mesh components
    // (Same code as Chapter 6)
    // ...

    // Draw any skinned meshes now
    // (Same code as Chapter 12)
    // ...
}
```