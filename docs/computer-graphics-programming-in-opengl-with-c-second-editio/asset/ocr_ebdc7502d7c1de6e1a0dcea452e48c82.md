One way of restoring some of this lost detail is to use *anisotropic filtering* (AF). Whereas standard mipmapping samples a texture image at a variety of square resolutions (e.g., 256x256, 128x128, etc.), AF samples the textures at a number of rectangular resolutions as well, such as 256x128, 64x128, and so on. This enables viewing at various angles while retaining as much detail in the texture as possible.

Anisotropic filtering is more computationally expensive than standard mipmapping and is not a required part of OpenGL. However, most graphics cards support AF (this is referred to as an *OpenGL extension*), and OpenGL does provide both a way of querying the card to see if it supports AF, and a way of accessing AF if it does. The code is added immediately after generating the mipmap:

```
```cpp
// if mipmapping
glBindTexture(GL_TEXTURE_2D, textureID);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR_MIPMAP_LINEAR);
glGenerateMipmap(GL_TEXTURE_2D);

// if also anisotropic filtering
if (glewIsSupported("GL_EXT_texture_filter_anisotropic")) {
    GLfloat anisoSetting = 0.0f;
    glGetFloatv(GL_MAX_TEXTURE_MAX_ANISOTROPY_EXT, &anisoSetting);
    glTexParameterf(GL_TEXTURE_2D, GL_TEXTURE_MAX_ANISOTROPY_EXT, anisoSetting);
}
```
```

![](bbox=[0.14, 0.63, 0.45, 0.8])

Figure 5.13
Anisotropic filtering.

The call to glewIsSupported() tests whether the graphics card supports AF. If it does, we set it to the maximum degree of sampling supported, a value retrieved using glGetFloatv() as shown. It is then applied to the active texture object using glTexParameterf(). The result is shown in Figure 5.13. Note that much of the lost detail from Figure 5.8 has been restored, while still removing the sparkling artifacts.

# ### 5.10 WRAPPING AND TILING

So far we have assumed that texture coordinates all fall in the range [0..1]. However, OpenGL actually supports texture coordinates of any value. There are