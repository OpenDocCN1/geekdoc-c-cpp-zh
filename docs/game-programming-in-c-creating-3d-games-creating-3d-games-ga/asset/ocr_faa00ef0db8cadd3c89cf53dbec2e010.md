```
```cpp
std::vector<GLenum> attachments;
for (int i = 0; i < NUM_GBUFFER_TEXTURES; i++)
{
    attachments.emplace_back(GL_COLOR_ATTACHMENT0 +
}
// Set the list of buffers to draw to
glDrawBuffers(static_cast<GLsizei>(attachments.siz
attachments.data()));
// Make sure everything worked
if (glCheckFramebufferStatus(GL_FRAMEBUFFER) !=
GL_FRAMEBUFFER_COMPLETE)
{
    Destroy();
    return false;
}
return true;
}
```
```

Next, you loop over each type of texture desired in the G-buffer and create one Texture instance for each type of