```
enum ButtonState
{
    ENone,
    EPressed,
    EReleased,
    EHeld
};

// Wrapper that contains current state of input
struct InputState
{
    KeyboardState Keyboard;
};

class InputSystem
{
public:
    bool Initialize();
    void Shutdown();

    // Called right before SDL_PollEvents loop
    void PrepareForUpdate();

    // Called right after SDL_PollEvents loop
    void Update();

private:
    const InputState& GetState() const { return mState; }
    InputState mState;
};
```