```
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