

```cpp
Matrix4 viewProj = Matrix4::CreateSimpleViewProj(1024.f, 768.f);
mShader.SetMatrixUniform("uViewProj", viewProj);
```

```cpp
void SpriteComponent::Draw(Shader* shader)
{
    // Scale the quad by the width/height of texture
    Matrix4x4 scaleMat = Matrix4x4::CreateScale(
        static_cast<float>(mTexWidth),
        static_cast<float>(mTexHeight),
        1.0f);
    Matrix4x4 world = scaleMat * mOwner->GetWorldTransform();
    // Set world transform
    shader->SetMatrixUniform("mWorldTransform", world);
    // Draw quad
    glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, nullptr);
}
```

```cpp
class Texture
{
public:
    Texture();
    ~Texture();

    bool Load(const std::string& fileName);
    void Unload();

    void SetActive();

    int GetWidth() const { return mWidth; }
    int GetHeight() const { return mHeight; }

private:
    // OpenGL ID of this texture
    // unsigned int mTextureID;

    // Width/height of the texture
    int mWidth;
    int mHeight;
};
```

```cpp
int channels = 0;
unsigned char* image = SOIL_load_image(
    fileName.c_str(),     // Name of file
    &mWidth,              // Stores width
    &mHeight,             // Stores height
    &channels,            // Stores number of channels
    SOIL_LOAD_AUTO        // Type of image file, or auto for any
);
```

```cpp
glGenTextures(1, &mTextureID);
glBindTexture(GL_TEXTURE_2D, mTextureID);
```

```cpp
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

```cpp
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
```

```cpp
bool Texture::load(const std::string& fileName)
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

    glGenTextures(1, &mTextureID);
    glBindTexture(GL_TEXTURE_2D, mTextureID);
    glTexImage2D(GL_TEXTURE_2D, 0, format, mWidth, mHeight, 0, format,
                 GL_UNSIGNED_BYTE, image);
    SOIL_free_image_data(image);

    // Enable bilinear filtering
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);

    return true;
}
```

```cpp
void Texture::Unload()
{
    glDeleteTextures(1, &mTextureID);
}

void Texture::SetActive()
{
    glBindTexture(GL_TEXTURE_2D, mTextureID);
}
```

```cpp
// In SpriteComponent::Draw...
// Set current texture
mTexture->SetActive();
// Draw quad
glDrawElements(GL_TRIANGLES, 6,
    GL_UNSIGNED_INT, nullptr);
```

```cpp
float vertices[] = {
    -0.5f, 0.5f, 0.f, 0.f, // top left
    0.5f, 0.5f, 0.f, 1.f, 0.f, // top right
    0.5f, -0.5f, 0.f, 1.f, 1.f, // bottom right
    -0.5f, -0.5f, 0.f, 0.f, 1.f // bottom left
};
```

```cpp
glBufferData(GL_ARRAY_BUFFER, numVerts * 5 * sizeof(float),
verts, GL_STATIC_DRAW);
```

```cpp
glEnableVertexAttribArray(0);
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE,
sizeof(float) * 5, // The stride is now 5 floats
0); // Vertex position is still offset 0
```

```cpp
glEnableVertexAttribArray(1);
glVertexAttribPointer(
    1,                            // Vertex attribute index
    2,                            // Number of components (2 because UV)
    GL_FLOAT,                     // Type of each component
    GL_FALSE,                     // Not used for GL_FLOAT
    sizeof(float) * 5,            // Stride (usually size of each vertex)
    reinterpret_cast<void*>(sizeof(float) * 3) // Offset pointer
);
```

```glsl
layout(location=0) in vec3 inPosition;
layout(location=1) in vec2 inTexCoord;
```

```glsl
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
  // Convert position to homogenous coordinates
  vec4 pos = vec4(inPosition, 1.0);
  // Transform position to world space, then clip space
  gl_Position = pos * uWorldTransform * uViewProj;
  // Pass along the texture coordinate to frag shader
  fragTexCoord = inTexCoord;
}
```

```glsl
outColor = texture(uTexture, fragTexCoord);
```

```glsl
#version 330
// Tex coord input from vertex shader
in vec2 fragTexCoord;
// Output color
out vec4 outColor;
// For texture sampling
uniform sampler2D uTexture;

void main()
{
    // Sample color from texture
    outColor = texture(uTexture, fragTexCoord);
}
```

```cpp
glEnable(GL_BLEND);
glBlendFunc(
    GL_SRC_ALPHA,    // srcFactor is srcAlpha
    GL_ONE_MINUS_SRC_ALPHA // dstFactor is 1 - srcAlpha
);
```

```cpp
Quaternion result = Quaternion::Concatenate(q, p);
```

```cpp
class Quaternion
{
public:
    // functions/data omitted
    // ...

    // Construct the quaternion from an axis and angle
    explicit Quaternion(const Vector3& axis, float angle);
    // Spherical Linear Interpolation
    static Quaternion Slerp(const Quaternion& a, const Quaternion& b,
        float f);

    // Concatenate (rotate by q FOLLOWED BY p, uses Grassmann product pq)
    static Quaternion Concatenate(const Quaternion& q, const Quaternion&
    p);
    // v = (0, 0, 0); s = 1
    static const Quaternion Identity;
};

// In Matrix4...
// Create Matrix4 from Quaternion
static Matrix4 CreateFromQuaternion(const class Quaternion& q);
// In Vector3...
// Transform a Vector3 by a Quaternion
static Vector3 Transform(const Vector3& v, const class Quaternion& q);
```

```cpp
// Scale, then rotate, then translate
mWorldTransform = Matrix4::CreateScale(mScale);
mWorldTransform *= Matrix4::CreateFromQuaternion(mRotation);
mWorldTransform *= Matrix4::CreateTranslation(mPosition);
```

```cpp
Vector3 GetForward() const
{
    return Vector3::Transform(Vector3::UnitX, mRotation);
}
```

```cpp
void MoveComponent::Update(float deltaTime)
{
    if (!Math::NearZero(mAngularSpeed))
    {
        Quaternion rot = mOwner->GetRotation();
        float angle = mAngularSpeed * deltaTime;
        // Create quaternion for incremental rotation
        // Rotate about up axis
        Quaternion inc(Vector3::UnitZ, angle);
        // Concatenate old and new quaternion
        rot = Quaternion::Concatenate(rot, inc);
        mOwner->SetRotation(rot);
    }

    // Updating position based on forward speed stays the same
    // ...
}
```

```json
{
    "version": 1,
    "vertexformat": "PosNormTex",
    "shader": "BasicMesh",
    "textures": [
        "Assets/Cube.png"
    ],
    "vertices": [
        [1.0, 1.0, -1.0, 0.57, 0.57, -0.57, 0.66, 0.33],
        [1.0, -1.0, -1.0, 0.57, -0.57, -0.57, 0.66, 0.0],
        [-1.0, -1.0, -1.0, -0.57, -0.57, -0.57, 1.0, 0.33],
        [-1.0, 1.0, -1.0, -0.57, 0.57, -0.57, 0.66, 0.66],
        [1.0, 0.99, 1.0, 0.57, 0.57, 0.57, 0.33, 0.33],
        [0.99, -1.0, 1.0, 0.57, -0.57, 0.57, 0.0, 0.0],
        [-1.0, -1.0, 1.0, -0.57, -0.57, 0.57, 0.66, 0.33],
        [-1.0, 1.0, 1.0, -0.57, 0.57, 0.57, 0.33, 0.66]
    ],
    "indices": [
        [1, 3, 0],
        [7, 5, 4],
        [4, 1, 0],
        [5, 2, 1],
        [2, 7, 3],
        [0, 7, 4],
        [1, 2, 3],
        [4, 5, 0],
        [4, 5, 1],
        [5, 6, 2],
        [2, 6, 7],
        [0, 3, 7]
    ]
}
```

