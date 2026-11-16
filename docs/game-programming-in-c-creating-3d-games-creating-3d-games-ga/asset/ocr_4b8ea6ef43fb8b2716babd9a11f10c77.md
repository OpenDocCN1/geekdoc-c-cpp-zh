```
```cpp
if (GLEW_EXT_texture_filter_anisotropic)
{
    // Get the maximum anisotropy value
    GLfloat largest;
    glGetFloatv(GL_MAX_TEXTURE_MAX_ANISOTROPY_EXT, &largest);
    // Enable it
    glTexParameterf(GL_TEXTURE_2D, GL_TEXTURE_MAX_ANISOTROPY_EXT,
                    largest);
}
```
```