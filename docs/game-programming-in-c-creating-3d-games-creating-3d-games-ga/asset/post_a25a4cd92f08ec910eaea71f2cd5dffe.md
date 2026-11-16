
## Chapter 13, “Intermediate Graphics.”

Listing 5.15 shows the final version of Texture::Load.

### Listing 5.15 Texture::Load Implementation

Click here to view code image

```
bool Texture::Load(const std::string& fileName)
{
    int channels = 0;

    unsigned char* image = SOIL_load_image(fileName.c_str(),
    &mWidth, &mHeight, &channels, SOIL_LOAD_AUTO);

    if (image == nullptr)
    {
        SDL_Log("SOIL failed to load image %s: %s",
        fileName.c_str(), SOIL_last_result());

        return false;
    }

    int format = GL_RGB;
    if (channels == 4)
    {
        format = GL_RGBA;
}
```

```
glGenTextures(1, &mTextureID);
glBindTexture(GL_TEXTURE_2D, mTextureID);
glTexImage2D(GL_TEXTURE_2D, 0, format, mWidth, mHeight,
GL_UNSIGNED_BYTE, image);
SOIL_free_image_data(image);
// Enable bilinear filtering
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER,
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER,
return true;
}
```

The Texture::Unload and Texture::SetActive functions are each just a single line. Unload deletes the texture object, and SetActive calls glBindTexture:

**Click here to view code image**

```
void Texture::Unload()
{
glDeleteTextures(1, &mTextureID);

}

void Texture::SetActive()
{
    glBindTexture(GL_TEXTURE_2D, mTextureID);
}
```

You can then load textures into a map in Game, much as you did for SDL_Texture previously. The Game::GetTexture function then returns a Texture* for the requested texture. Next, SpriteComponent needs a Texture* member variable instead of SDL_Texture*.

Finally, in SpriteComponent::Draw, add a call to SetActive on mTexture, right before drawing the vertices. This means you can now set a different active texture for each sprite component you draw:

Click here to view code image

```
// In SpriteComponent::Draw...

// Set current texture
mTexture->SetActive();

// Draw quad
```

```
glDrawElements(GL_TRIANGLES, 6,
GL_UNSIGNED_INT, nullptr);
```

## Updating the Vertex Format

To use texture mapping, the vertices need to have texture coordinates, so you need to update the sprite VertexArray:

Click here to view code image

```
float vertices[] = {
    -0.5f, 0.5f, 0.f, 0.f, 0.f, // top left
    0.5f, 0.5f, 0.f, 1.f, 0.f, // top right
    0.5f, -0.5f, 0.f, 1.f, 1.f, // bottom right
    -0.5f, -0.5f, 0.f, 0.f, 1.f // bottom left
};
```

Remember that the V texture coordinate is flipped to account for OpenGL's idiosyncrasy with how it expects the image data.

For each vertex, the first three floating-point values are the position and the next two floating-point values are the texture coordinates. Figure 5.11 shows the memory layout of this new vertex format.

| | Vertex 0 | | | | | Vertex 1 | | | | | Vertex 2 | | | | | ... |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Byte | x | y | z | u | v | x | y | z | u | v | x | y | z | u | v | |
| 0 | 4 | 8 | 12 | 16 | 20 | 24 | 28 | 32 | 36 | 40 | 44 | 48 | 52 | 56 | 60 | |

Offset to UV = sizeof(float) * 3

Stride = sizeof(float) * 5

Figure 5.11 Vertex memory layout with position and texture coordinates

Because you're changing the vertex layout, you must change code in the `VertexArray` constructor. For simplicity, assume that all vertices must have a 3D position and 2D texture coordinates. (You'll change this in subsequent chapters.)

Because the size of each vertex has changed, you need to update the `glBufferData` call to specify that each vertex now has five floats per vertex:

Click here to view code image

```
glBufferData(GL_ARRAY_BUFFER, numVerts * 5 * sizeof(float),
verts, GL_STATIC_DRAW);
```

Because the index buffer is still the same, the `glBufferData` call for that doesn't change. However, you must change vertex attribute 0 to specify that the stride of the vertex is now five floats:

Click here to view code image

```
glEnableVertexAttribArray(0);
```

```
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE,
    sizeof(float) * 5, // The stride is now 5 floats
    0); // Vertex position is still offset
```

This only fixes the position vertex attribute. However, because you now have a second vertex attribute for the texture coordinate, you must enable vertex attribute 1 and specify its format:

Click here to view code image

```
glEnableVertexAttribArray(1);
glVertexAttribPointer(
    1, // Vertex attribute index
    2, // Number of components (2 because
    GL_FLOAT, // Type of each component
    GL_FALSE, // Not used for GL_FLOAT
    sizeof(float) * 5, // Stride (usually size of each vertex)
    reinterpret_cast<void*>(sizeof(float) * 3) // Offset
);
```

The last parameter to this glVertexAttribPointer call is rather ugly. OpenGL needs to know the number of bytes from the start of a vertex to this attribute. That's where the sizeof(float) * 3 comes from. However, OpenGL wants this as an offset pointer. Thus, you must use reinterpret_cast to coerce the type into a void* pointer.

> tip
> If you use a struct in C++ code to represent the format of the vertices, you can use the offsetof macro to determine the offsets to a vertex attribute rather than manually computing them. This is especially helpful if there is padding between vertex elements.

## Updating the Shaders

Because the vertex format now uses texture coordinates, you should create two new shaders: Sprite.vert (initially a copy of Transform.vert) and Sprite.frag (initially a copy of Basic.frag).

### The Sprite.vert Shader

There previously was only one vertex attribute, so you could just declare position as an in variable, and GLSL knew which vertex attribute it corresponded to. However, now that there are multiple vertex attributes, you must specify which attribute slot corresponds to which in variable. This changes the variable declarations to the following:

Click here to view code image

```
layout(location=0) in vec3 inPosition;
layout(location=1) in vec2 inTexCoord;
```

The `layout` directive specifies which attribute slot corresponds to which `in` variable. Here, you specify that there's a 3D vector of floats for vertex attribute slot 0 and a 2D vector of floats for vertex attribute slot 1. This corresponds to the slot numbers in the `glVertexAttribPointer` calls.

Next, although the texture coordinates are an input to the vertex shader (because it's in the vertex layout), the fragment shader also needs to know the texture coordinates. This is because the fragment shader needs to know the texture coordinates to determine the color at the pixel. Luckily, you can pass data from the vertex shader to the fragment shader by declaring a global `out` variable in the vertex shader:

```
out vec2 fragTexCoord;
```

Then, inside the vertex shader's `main` function, add the following line, which copies the texture coordinates directly from the vertex input variable to the output variable:

```
fragTexCoord = inTexCoord;
```

The reason this ultimately works is that OpenGL automatically interpolates vertex shader outputs across the face of the triangle. Therefore, even though a triangle has only three vertices, any arbitrary pixel on the face of a triangle will know its corresponding texture coordinates in the fragment shader.

For completeness, Listing 5.16 gives the full source code for Sprite.vert.

### Listing 5.16 Sprite.vert Implementation

Click here to view code image

```
#version 330

// Uniforms for world transform and view-proj
uniform mat4 uWorldTransform;
uniform mat4 uViewProj;

// Attribute 0 is position, 1 is tex coords.
layout(location = 0) in vec3 inPosition;
layout(location = 1) in vec2 inTexCoord;

// Add texture coordinate as output
out vec2 fragTexCoord;

void main()
{
// Convert position to homogeneous coordinates
vec4 pos = vec4(inPosition, 1.0);

// Transform position to world space, then clip space
gl_Position = pos * uWorldTransform * uViewProj;

// Pass along the texture coordinate to frag shader
fragTexCoord = inTexCoord;
}
```

### The Sprite.frag Shader

As a rule, any out variables in the vertex shader should have a corresponding in in the fragment shader. The name and type of the in variable in the fragment shader must have the same name and type as the corresponding out variable in the vertex shader:

```
in vec2 fragTexCoord;
```

Next, you need to add a uniform for a texture sampler (that can get the color from a texture given a texture coordinate):

```
uniform sampler2D uTexture;
```

The sampler2D type is a special type that can sample 2D textures. Unlike with the world transform and view-
