```
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
    const Vector3& color = Color::White,
    int pointSize = 40);

protected:

// Helper to draw a texture
void DrawTexture(class Shader* shader, class Textu
    const Vector2& offset = Vector2::Zer
    float scale = 1.0f);

class Game* mGame;

// For the UI screen's title text
```