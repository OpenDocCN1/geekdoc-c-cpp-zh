
```cpp
void Actor::RotateToNewForward(const Vector3& forward)
{
    // Figure out difference between original (unit x) and new
    float dot = Vector3::Dot(Vector3::UnitX, forward);
    float angle = Math::Acos(dot);

    // Are we facing down X?
    if (dot > 0.9999f)
    {
        SetRotation(Quaternion::Identity);
    }
    // Are we facing down -X?
    else if (dot < -0.999f)
    {
        SetRotation(Vector3::UnitZ, Math::Pi);
    }
    else
    {
        // Rotate about axis from cross product
        Vector3 axis = Vector3::Cross(Vector3::UnitX, forward);
        axis.Normalize();
        SetRotation(Quaternion(axis, angle));
    }
}
```

```cpp
void BallMove::Update(float deltaTime)
{
    // Construct segment in direction of travel
    const float segmentLength = 30.0f;
    Vector3 start = mOwner->GetPosition();
    Vector3 dir = mOwner->GetForward();
    Vector3 end = start + dir * segmentLength;
    LineSegment l(start, end);

    // Test segment vs world
    PhysWorld* phys = mOwner->GetGame()->GetPhysWorld();
    PhysWorld::CollisionInfo info;
    if (phys->SegmentCast(l, info))
    {
        // If we collided, reflect the direction about the normal
        dir = Vector3::Reflect(dir, info.mNormal);
        mOwner->RotateToNewForward(dir);
    }

    // Base class update moves based on forward speed
    MoveComponent::Update(deltaTime);
}
```

```cpp
void PhysWorld::TestPairwise(std::function<void(Actor*, Actor*)> f)
{
    // Naive implementation O(n^2)
    for (size_t i = 0; i < mBoxes.size(); i++)
    {
        // Don't need to test vs. itself and any previous i values
        for (size_t j = i + 1; j < mBoxes.size(); j++)
        {
            BoxComponent* a = mBoxes[i];
            BoxComponent* b = mBoxes[j];
            if (Intersect(a->GetWorldBox(), b->GetWorldBox()))
            {
                // Call supplied function to handle intersection
                f(a->GetOwner(), b->GetOwner());
            }
        }
    }
}
```

```cpp
void PhysWorld::TestSweepAndPrune(std::function<void(Actor*, Actor*)> f)
{
    // Sort by min.x
    std::sort(mBoxes.begin(), mBoxes.end(),
        [](BoxComponent* a, BoxComponent* b) {
            return a->GetWorldBox().mMin.x <
                b->GetWorldBox().mMin.x;
        });
    for (size_t i = 0; i < mBoxes.size(); i++)
    {
        // Get max.x for box[i]
        BoxComponent* a = mBoxes[i];
        float max = a->GetWorldBox().mMax.x;
        for (size_t j = i + 1; j < mBoxes.size(); j++)
        {
            BoxComponent* b = mBoxes[j];
            // if box[j] min.x is past the max.x bounds of box[i],
            // then there aren't any other possible intersections
            // against box[i]
            if (b->GetWorldBox().mMin.x > max)
            {
                break;
            }
            else if (Intersect(a->GetWorldBox(), b->GetWorldBox()))
            {
                f(a->GetOwner(), b->GetOwner());
            }
        }
    }
}
```

```cpp
void PFSActor::FixCollisions()
{
    // Need to recompute my world transform to update world box
    ComputeWorldTransform();

    const AABox& playerBox = mBoxComp->GetWorldBox();
    Vector3 pos = GetPosition();

    auto planes = GetGame()->GetPlanes();
    for (auto pa : planes)
    {
        // Do we collide with this PlaneActor?
        const AABox& planeBox = pa->GetBox()->GetWorldBox();
        if (Intersect(playerBox, planeBox))
        {
            // Calculate all our differences
            float dx1 = planeBox.mMin.x - playerBox.mMax.x;
            float dx2 = planeBox.mMax.x - playerBox.mMin.x;
            float dy1 = planeBox.mMin.y - playerBox.mMax.y;
            float dy2 = planeBox.mMax.y - playerBox.mMin.y;
            float dz1 = planeBox.mMin.z - playerBox.mMax.z;
            float dz2 = planeBox.mMax.z - playerBox.mMin.z;

            // Set dx to whichever of dx1/dx2 have a lower abs
            float dx = (Math::Abs(dx1) < Math::Abs(dx2)) ? dx1 : dx2;
            // Ditto for dy
            float dy = (Math::Abs(dy1) < Math::Abs(dy2)) ? dy1 : dy2;
            // Ditto for dz
            float dz = (Math::Abs(dz1) < Math::Abs(dz2)) ? dz1 : dz2;

            // Whichever is closest, adjust x/y position
            if (Math::Abs(dx) <= Math::Abs(dy) &&
                Math::Abs(dx) <= Math::Abs(dz))
            {
                pos.x += dx;
            }
            else if (Math::Abs(dy) <= Math::Abs(dx) &&
                     Math::Abs(dy) <= Math::Abs(dz))
            {
                pos.y += dy;
            }
            else
            {
                pos.z += dz;
            }

            // Need to set position and update box component
            SetPosition(pos);
            mBoxComp->OnUpdateWorldTransform();
        }
    }
}
```

```cpp
class Font
{
public:
    Font();
    ~Font();

    // Load/unload from a file
    bool Load(const std::string& fileName);
    void Unload();

    // Given string and this font, draw to a texture
    void RenderText(const std::string& text,
                    const Vector2& color = Color::White,
                    int pointSize = 30);

private:
    // Map of point sizes to font data
    std::unordered_map<int, TTF_Font*> mFontData;
};
```

```cpp
bool Font::Load(const std::string& fileName)
{
    // Support these font sizes
    std::vector<int> fontSizes = {
        8, 9, 10, 11, 12, 14, 16, 18, 20, 22, 24, 26, 28,
        30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 52, 56,
        60, 64, 68, 72
    };
    // Call TTF_OpenFont once per every font size
    // (autos size = fontSizes)
    for (int size : fontSizes)
    {
        TTF_Font* font = TTF_OpenFont(fileName.c_str(), size);
        if (font == nullptr)
        {
            SDL_Log("Failed to load font %s in size %d", fileName.c_str(), size);
            return false;
        }
        mFontData.emplace(size, font);
    }
    return true;
}

Texture* Font::RenderText(const std::string& text,
             const Vector2& color, int pointSize)
{
    Texture* texture = nullptr;
    // Convert to SDL_Color
    SDL_Color sdlColor;
    sdlColor.r = static_cast<Uint8>(color.x * 255);
    sdlColor.g = static_cast<Uint8>(color.y * 255);
    sdlColor.b = static_cast<Uint8>(color.y * 255);
    sdlColor.a = 255;
    // Find the font data for this point size
    auto iter = mFontData.find(pointSize);
    if (iter != mFontData.end())
    {
        TTF_Font* font = iter->second;
        // Draw this to a surface (blended for alpha)
        SDL_Surface* surf = TTF_RenderText_Blended(font, text.c_str(),
                                                    sdlColor);
        if (surf != nullptr)
        {
            // Convert from surface to texture
            texture = new Texture();
            texture->CreateFromSurface(surf);
            SDL_FreeSurface(surf);
        }
        else
        {
            SDL_Log("Point size %d is unsupported", pointSize);
        }
    }
    return texture;
}
```

```cpp
class UIScreen
{
public:
    UIScreen(class Game* game);
    virtual ~UIScreen();

    // UIScreen subclasses can override these
    virtual void Update(float deltaTime);
    virtual void Draw(class Shader* shader);
    virtual void ProcessInput(const uint8_t* keys);
    virtual void HandleKeyPress(int key);

    // Tracks if the UI is active or closing
    enum UIState { EActive, EClosing };
    // Set state to closing
    void Close();

    // Get state of UI screen
    UIState GetState() const { return mState; }
    // Change the title text
    void SetTitle(const std::string& text,
        const Vector4& color = Color::White,
        int pointSize = 40);

protected:
    // Helper to draw a texture
    void DrawTexture(class Shader* shader, class Texture* texture,
                     const Vector2& offset = Vector2::Zero,
                     float scale = 1.0f);

    class Game* mGame;

    // For the UI screen's title text
    class Font* mFont;
    class Texture* mTitleTex;

    // State machine
    class State* mState;
    UIState mState;
};
```

```cpp
// UI stack for game
std::vector<class UIScreen*> mUIStack;
// Returns entire stack by reference
const std::vector<class UIScreen*>& GetUIStack();
// Push specified UIScreen onto stack
void PushUI(class UIScreen* screen);
```

```cpp
for (auto ui : mUIStack)
{
    if (ui->GetState() == UIScreen::EActive)
    {
        ui->Update(deltaTime);
    }
}
```
