
```cpp
// Position is 3 floats
glEnableVertexAttribArray(0);
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 8 * sizeof(float), 0);
// Normal is 3 floats
glEnableVertexAttribArray(1);
glVertexAttribPointer(1, 3, GL_FLOAT, GL_FALSE, 8 * sizeof(float),
reinterpret_cast<void*>(sizeof(float) * 3));
// Texture coordinates is 2 floats
glEnableVertexAttribArray(2);
glVertexAttribPointer(2, 2, GL_FLOAT, GL_FALSE, 8 * sizeof(float),
reinterpret_cast<void*>(sizeof(float) * 6));
```

```cpp
// Attribute 0 is position, 1 is normal, 2 is tex coords
layout(location = 0) in vec3 inPosition;
layout(location = 1) in vec3 inNormal;
layout(location = 2) in vec2 inTexCoord;
```

```cpp
class Mesh
{
public:
    Mesh();
    ~Mesh();
    // Load/unload mesh
    bool Load(const std::string& fileName, class Game* game);
    void Unload();
    // Get the vertex array associated with this mesh
    class VertexArray* GetVertexArray() { return mVertexArray; }
    // Get a texture from specified index
    class Texture* GetTexture(size_t index);
    // Get name of shader
    const std::string& GetShaderName() const { return mShaderName; }
    // Get object space bounding sphere radius
    float GetRadius() const { return mRadius; }
private:
    // Textures associated with this mesh
    std::vector<class Texture*> mTextures;
    // Vertex array associated with this mesh
    class VertexArray* mVertexArray;
    // Name of shader specified by mesh
    std::string mShaderName;
    // Stores object space bounding sphere radius
    float mRadius;
};
```

```cpp
class Renderer
{
public:
    Renderer();
    ~Renderer();
    // Initialize and shutdown renderer
    bool Initialize(float screenWidth, float screenHeight);
    void Shutdown();
    // Unload all textures/meshes
    void UnloadData();
    // Draw the frame
    void Draw();
    void AddSprite(class SpriteComponent* sprite);
    void RemoveSprite(class SpriteComponent* sprite);
    class Texture* GetTexture(const std::string& fileName);
    class Mesh* GetMesh(const std::string& fileName);
private:
    bool LoadShaders();
    void CreateSpriteVerts();
    // Member data omitted
};
```

```cpp
// Location of camera
Vector3 eye = mCameraActor->GetPosition();
// Point 10 units in front of camera
Vector3 target = mCameraActor->GetPosition() +
    mCameraActor->GetForward() * 10.0f;
Matrix4x4 view = Matrix4x4::CreateLookAt(eye, target, Vector3::UnitZ);
```

```cpp
// zBuffer[x][y] grabs depth at that pixel
foreach MeshComponent m in scene
    foreach Pixel p in m
        float depth = p.Depth()
        if zBuffer[p.x][p.y] < depth
            p.draw
        endif
    endfor
endfor
```

```cpp
SDL_GL_SetAttribute(SDL_GL_DEPTH_SIZE, 24);
```

```cpp
glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
```

```cpp
mMeshShader->SetActive();

// Set the view-projection matrix
mView = Matrix4::CreateLookAt(
    Vector3::Zero,    // Camera position
    Vector3::UnitZ,   // Target position
    Vector3::UnitZ    // Up
);

mProjection = Matrix4::CreatePerspectiveFOV(
    Math::ToRadians(70.0f), // Horizontal FOV
    mScreenWidth,    // Width of view
    mScreenHeight,   // Height of view
    25.0f,           // Near plane distance
    10000.0f         // Far plane distance
);

mMeshShader->SetMatrixUniform("uViewProj", mView * mProjection);
```

```cpp
class MeshComponent : public Component
{
public:
    MeshComponent(class Actor* owner);
    ~MeshComponent();
    // Draw this mesh component with provided shader
    virtual void Draw(class Shader* shader);
    // Set the mesh/texture index used by mesh component
    virtual void SetMesh(class Mesh* mesh);
    // Set texture index(size_t index);
protected:
    class Mesh* mMesh;
    size_t mTextureIndex;
};
```

```cpp
void MeshComponent::Draw(Shader* shader)
{
    if (mMesh)
    {
        // Set the world transform
        shader->SetMatrix4x4("uWorldTransform",
            mOwner->GetWorldTransform());
        // Set the active texture
        Texture* t = mMesh->GetTexture(mTextureIndex);
        if (t) { t->SetActive(); }
        // Set the mesh's vertex array as active
        VertexArray* va = mMesh->GetVertexArray();
        va->SetActive();
        // Draw
        glDrawElements(GL_TRIANGLES, va->GetNumIndices(),
            GL_UNSIGNED_INT, nullptr);
    }
}
```

```cpp
// Enable depth buffering/disable alpha blend
glEnable(GL_DEPTH_TEST);
glDisable(GL_BLEND);
// Set the basic mesh shader active
mMeshShader->SetActive();
// Update view-projection matrix
mMeshShader->SetMatrixUniform("uViewProj", mView * mProjection);
for (auto mc : mMeshComps)
{
    mc->Draw(mMeshShader);
}
```

```cpp
// Create a struct for directional light
struct DirectionalLight
{
    // Direction of light
    vec3 mDirection;
    // Diffuse color
    vec3 mDiffuseColor;
    // Specular color
    vec3 mSpecularColor;
};

// Uniforms for lighting
// Camera position (in world space)
uniform vec3 uCameraPos;
// Ambient light level
uniform vec3 uAmbientLight;
// Specular power for this surface
uniform float uSpecPower;
// Directional light (only one for now)
uniform DirectionalLight uDirLight;
```

```cpp
void Renderer::SetLightUniforms(Shader* shader)
{
    // Camera position is from inverted view
    Matrix4x4 inView = mView;
    inView.Invert();
    shader->SetVectorUniform("uCameraPos", inView.GetTranslation());
    // Ambient light
    shader->SetVectorUniform("uAmbientLight", mAmbientLight);
    // Directional light
    shader->SetVectorUniform("uDirLight.mDirection", mDirLight.mDirection);
    shader->SetVectorUniform("uDirLight.mDiffuseColor",
        mDirLight.mDiffuseColor);
    shader->SetVectorUniform("uDirLight.mSpecColor", mDirLight.mSpecColor);
}
```

```cpp
void main()
{
    // Convert position to homogeneous coordinates
    vec4 pos = vec4(inPosition, 1.0);

    // Transform position to world space
    pos = pos * uWorldTransform;

    // Save world position
    fragWorldPos = pos.xyz;

    // Transform to clip space
    gl_Position = pos * uViewProj;

    // Transform normal into world space (w = 0)
    fragNormal = (vec4(inNormal, 0.0f) * uWorldTransform).xyz;

    // Pass along the texture coordinate to frag shader
    fragTexCoord = inTexCoord;
}
```

```cpp
void main()
{
    // Surface normal
    vec3 N = normalize(fragNormal);
    // Vector from surface to light
    vec3 L = normalize(uDirLight.mDirection);
    // Vector from surface to camera
    vec3 V = normalize(uEyePosition - fragWorldPos);
    // Reflection of -L about N
    vec3 R = normalize(reflect(-L, N));

    // Compute phong reflection
    vec3 Phong = uAmbientLight;
    float NdotL = dot(N, L);
    if (NdotL > 0)
    {
        vec3 Diffuse = uDirLight.mDiffuseColor * NdotL;
        vec3 Specular = uDirLight.mSpecularColor *
            pow(max(0.0, dot(R, V)), uSpecPower);
        Phong = Diffuse + Specular;
    }

    // Final color is texture color times phong light (alpha = 1)
    outColor = texture(uTexture, fragTexCoord) * vec4(Phong, 1.0f);
}
```

```cpp
class AudioSystem
{
public:
    AudioSystem(class Game* game);
    ~AudioSystem();

    bool Initialize();
    void Shutdown();
    void Update(float deltaTime);

private:
    class Game* mGame;
    // FMOD studio system
    FMOD::Studio::System* mSystem;
    FMOD::Studio::Bank* mMasterBank;
    // FMOD Low-level system (in case needed)
    FMOD::System* mLowLevelSystem;
};
```

```cpp
FMOD::Debug_Initialize(
    FMOD_DEBUG_LEVEL_ERROR, // Log only errors
    FMOD_DEBUG_MODE_TTY // Output to stdout
);

FMOD_RESULT result;
result = FMOD::Studio::System::create(&system);
if (result != FMOD_OK)
{
    SDL_Log("Failed to create FMOD system: %s",
        FMOD_ErrorString(result));
    return false;
}

result = mSystem->initialize(
    512,                        // Max number of concurrent sounds
    FMOD_STUDIO_INIT_NORMAL,   // Use default settings
    FMOD_INIT_NORMAL,          // Use default settings
    nullptr                    // Usually null
);
// Validate result == FMOD_OK...
```
