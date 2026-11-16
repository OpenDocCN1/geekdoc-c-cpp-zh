```
glTexImage2D(
    GL_TEXTURE_2D,    // Texture target
    0,                // Level of detail (for now, assume 0)
    format,           // Color format OpenGL should use
    mWidth,           // Width of texture
    mHeight,          // Height of texture
    0,                // Border - "this value must be 0"
    format,           // Color format of input data
    GL_UNSIGNED_BYTE, // Bit depth of input data
    // Unsigned byte specifies 8-bit channels
    image             // Pointer to image data
);
```