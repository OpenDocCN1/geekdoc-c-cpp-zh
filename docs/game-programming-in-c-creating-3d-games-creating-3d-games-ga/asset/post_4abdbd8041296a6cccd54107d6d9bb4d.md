
```cpp
void PointLightComponent::Draw(Shader* shader, Mesh* mesh)
{
    // Scale world transform to the outer radius (divided by
    // the mesh radius and positioned to the world position
    Matrix4x4 scale = Matrix4x4::CreateScale(mOwner->GetScale() *
        mOuterRadius / mesh->GetRadius()));

    Matrix4x4 trans = Matrix4x4::CreateTranslation(mOwner->GetPosition());
    Matrix4x4 worldTransform = scale * trans;
    shader->SetMatrixUniform("uWorldTransform", worldTransform);

    // Set point light shader constants
    shader->SetVectorUniform("uPointLight.mWorldPos",
        mOwner->GetPosition());
    shader->SetVectorUniform("uPointLight.mDiffuseColor", mDiffuseColor);
    shader->SetFloatUniform("uPointLight.mInnerRadius", mInnerRadius);
    shader->SetFloatUniform("uPointLight.mOuterRadius", mOuterRadius);

    // Draw the sphere
    glDrawElements(GL_TRIANGLES, mesh->GetVertexArray()->GetNumIndices(),
        GL_UNSIGNED_INT, nullptr);
}
```

```json
{
  "version": 1,
  "globalProperties": {
    "ambientLight": [0.2, 0.2, 0.2],
    "directionalLight": {
      "direction": [0.0, -0.707, -0.707],
      "color": [0.78, 0.88, 1.0]
    }
  }
}
```

```cpp
class LevelLoader
{
public:
    // Load the level -- returns true if successful
    static bool LoadLevel(class Game* game, const std::string& fileName);
};
```

```cpp
bool LevelLoader::loadJSON(const std::string& fileName,
                         rapidjson::Document& outDoc)
{
    // Load the file from disk into an ifstream in binary mode,
    // loaded with stream buffer at the end (ate)
    std::ifstream file(fileName, std::ios::in |
                     std::ios::binary | std::ios::ate);
    if (!file.is_open())
    {
        SDL_Log("File %s not found", fileName.c_str());
        return false;
    }

    // Get the size of the file
    std::ifstream::pos_type fileSize = file.tellg();

    // Seek back to start of file
    file.seekg(0, std::ios::beg);

    // Create a vector of size + 1 (for null terminator)
    std::vector<char> bytes(static_cast<size_t>(fileSize) + 1);

    // Read bytes into vector
    file.read(bytes.data(), static_cast<size_t>(fileSize));

    // Load raw data into RapidJSON document
    outDoc.Parse(bytes.data());

    if (!outDoc.IsObject())
    {
        SDL_Log("File %s is not valid JSON", fileName.c_str());
        return false;
    }

    return true;
}
```

```cpp
rapidjson::Document doc;
if (!LoadJSON(fileName, doc))
{
    SDL_Log("Failed to load level %s", fileName.c_str());
    return false;
}
```

```cpp
bool JsonHelper::GetInt(const rapidjson::Value& inObject,
                 const char* inProperty, int& outInt)
{
    // Check if this property exists
    auto itr = inObject.FindMember(inProperty);
    if (itr == inObject.MemberEnd())
    {
        return false;
    }

    // Get the value type, and check it's an integer
    auto& property = itr->value;
    if (!property.IsInt())
    {
        return false;
    }

    // We have the property
    outInt = property.GetInt();
    return true;
}
```

```cpp
int version = 0;
if (!JsonHelper::GetInt(doc, "version", version) ||
    version != LevelVersion)
{
    SDL_Log("Incorrect level file version for %s", fileName.c_str());
    return false;
}
```

```cpp
void LevelLoader::LoadGlobalProperties(Game* game,
    const rapidjson::Value& inObject)
{
    // Get ambient light
    Vector3 ambient;
    if (JsonHelper::GetVector3(inObject, "ambientLight", ambient))
    {
        game->GetRenderer()->SetAmbientLight(ambient);
    }

    // Get directional light
    const rapidjson::Value& dirObj = inObject["directionalLight"];
    if (dirObj.IsObject())
    {
        DirectionalLight* light = game->GetRenderer()->GetDirectionalLight();
        // Set direction/color, if they exist
        JsonHelper::GetVector3(dirObj, "direction", light->mDirection);
        JsonHelper::GetVector3(dirObj, "color", light->mDiffuseColor);
    }
}
```

```cpp
// Handle any global properties
// const rapidjson::Value& globals = doc["globalProperties"];
if (globals.IsObject())
{
    LoadGlobalProperties(game, globals);
}
```

```cpp
LevelLoader::LoadLevel(this, "Assets/Level0.gplevel");
```

```json
{
    "actors": [
        {
            "type": "TargetActor",
            "properties": {
                "position": [1450.0, 0.0, 100.0]
            }
        },
        {
            "type": "TargetActor",
            "properties": {
                "position": [0.0, -1450.0, 200.0],
                "rotation": [0.0, 0.0, 0.7071, 0.7071]
            }
        },
        {
            "type": "TargetActor",
            "properties": {
                "position": [0.0, 1450.0, 200.0],
                "rotation": [0.0, 0.0, -0.7071, 0.7071]
            }
        }
    ]
}
```

```cpp
void Actor::LoadProperties(const rapidjson::Value& inObj)
{
    // Use strings for different states
    std::string state;
    if (JsonHelper::GetString(inObj, "state", state))
    {
        if (state == "active")
        {
            SetState(EActive);
        }
        else if (state == "paused")
        {
            SetState(EPaused);
        }
        else if (state == "dead")
        {
            SetState(EDead);
        }
    }
    // Load position, rotation, and scale, and compute transform
    JsonHelper::GetVector3(inObj, "position", mPosition);
    JsonHelper::GetQuaternion(inObj, "rotation", mRotation);
    JsonHelper::GetFloat(inObj, "scale", mScale);
    ComputeWorldTransform();
}
```

```cpp
void SomeActor::LoadProperties(const rapidjson::Value& inObj)
{
    // Load base actor properties
    Actor::LoadProperties(inObj);

    // Load any of my custom properties
    // ...
}
```

```cpp
template <typename T>
static Actor* Create(class Game* game, const rapidjson::Value& inObj)
{
    // Dynamically allocate actor of type T
    T* t = new T(game);
    // Call LoadProperties on new actor
    t->LoadProperties(inObj);
    return t;
}
```

```cpp
using ActorFunc = std::function<
    class Actor*(class Game*, const rapidjson::Value&)
>;
```

```cpp
static std::unordered_map<std::string, ActorFunc> sActorFactoryMap;
```

```cpp
std::unordered_map<std::string, ActorFunc> LevelLoader::sActorFactoryMap
{
    { "Actor", &Actor::Create<Actor> },
    { "BallActor", &Actor::Create<BallActor> },
    { "FollowActor", &Actor::Create<FollowActor> },
    { "PlaneActor", &Actor::Create<PlaneActor> },
    { "TargetActor", &Actor::Create<TargetActor> },
};
```

```cpp
void LevelLoader::loadActors(Game* game, const rapidjson::Value& inArray)
{
    // Loop through array of actors
    for (rapidjson::SizeType i = 0; i < inArray.Size(); i++)
    {
        const rapidjson::Value& actorObj = inArray[i];
        if (actorObj.IsObject())
        {
            // Get the type
            std::string type;
            if (JsonHelper::GetString(actorObj, "type", type))
            {
                // Is this type in the map?
                auto iter = sActorFactoryMap.find(type);
                if (iter != sActorFactoryMap.end())
                {
                    // Construct with function stored in map
                    Actor* actor = iter->second(game, actorObj["properties"]);
                }
                else
                {
                    SDL_Log("Unknown actor type %s", type.c_str());
                }
            }
        }
    }
}
```

```cpp
const rapidjson::Value& actors = doc["actors"];
if (actors.IsArray())
{
    loadActors(game, actors);
}
```

```json
{
    "actors": [
        {
            "type": "Actor",
            "properties": {
                "position": [0.0, 0.0, 0.0],
                "scale": 5.0
            },
            "components": [
                {
                    "type": "MeshComponent",
                    "properties": { "meshFile": "Assets/Sphere.gpmesh" }
                }
            ]
        },
        {
            "type": "TargetActor",
            "properties": { "position": [1450.0, 0.0, 100.0] },
            "components": [
                {
                    "type": "MeshComponent",
                    "properties": { "meshFile": "Assets/Sphere.gpmesh" }
                }
            ]
        }
    ]
}
```
