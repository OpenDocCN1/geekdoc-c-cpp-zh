abbreviated declaration of Renderer.

# Listing 6.5 Abbreviated Renderer Declaration

Click here to view code image

```
class Renderer
{
public:
    Renderer();
    ~Renderer();
    // Initialize and shutdown renderer
    bool Initialize(float screenWidth, float screenHei
    void Shutdown();
    // Unload all textures/meshes
    void UnloadData();
    // Draw the frame
    void Draw();
    void AddSprite(class SpriteComponent* sprite);
    void RemoveSprite(class SpriteComponent* sprite);
    class Texture* GetTexture(const std::string& file
```