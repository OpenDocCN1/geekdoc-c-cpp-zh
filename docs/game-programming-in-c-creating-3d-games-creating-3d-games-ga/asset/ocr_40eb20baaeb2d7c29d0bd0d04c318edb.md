declaration of SpriteComponent.

# Listing 2.4 SpriteComponent Declaration

Click here to view code image

```
class SpriteComponent : public Component
{
public:
    // (Lower draw order corresponds with further back)
    SpriteComponent(class Actor* owner, int drawOrder
    ~SpriteComponent();

    virtual void Draw(SDL_Renderer* renderer);
    virtual void SetTexture(SDL_Texture* texture);

    int GetDrawOrder() const { return mDrawOrder; }
    int GetTexHeight() const { return mTexHeight; }
    int GetTexWidth() const { return mTexWidth; }

protected:
    // Texture to draw
    SDL_Texture* mTexture;

    // Draw order used for painter's algorithm
    int mDrawOrder;
}
```