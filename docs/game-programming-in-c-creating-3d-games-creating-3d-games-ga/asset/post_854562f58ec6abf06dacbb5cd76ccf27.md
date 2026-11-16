
To solve this problem, you can have the `InputSystem` class populate data in a helper class called `InputState`. You can then pass this `InputState` by `const` reference to actors/components via their `ProcessInput` function. You can also add several helper functions to `InputState` to make it easy to query whatever state the actor/component cares about.

Listing 8.1 shows the initial declaration of the relevant pieces. First, declare a `ButtonState` enum to correspond to the four different states outlined in Table 8.1. Next, declare an `InputState` struct (which currently has no members). Finally, you declare `InputSystem`, which contains `Initialize`/`Shutdown` functions (much like `Game`). It also has a `PrepareForUpdate` function that is called before `SDL_PollEvents`, and then an `Update` function that is called after polling events. The `GetState` function returns a `const` reference to the `InputState` it holds as member data.

## Listing 8.1 Basic `InputSystem` Declarations

Click here to view code image

```cpp
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

    const InputState& GetState() const { return mState; }

private:
    InputState mState;
};
```

To integrate this code into the game, you add an InputSystem pointer to the member data of Game called mInputSystem. Game::Initialize allocates and initializes InputSystem and Game::Shutdown shuts down and deletes it.

Next, you change the declaration of ProcessInput in both Actor and Component to the following:

Click here to view code image

```cpp
void ProcessInput(const InputState& state);
```

Recall that in Actor, ProcessInput is not overridable because it calls ProcessInput on all the attached components. However, actors also have an overridable ActorInput function for any input specific to that actor. So, you similarly change the declaration of ActorInput to take in a constant InputState reference.

Finally, the implementation of Game::ProcessInput changes to the following outline of steps:

Click here to view code image

```cpp
void Game::ProcessInput()
{
    mInputSystem->PrepareForUpdate();

    // SDL_PollEvent loop...

    mInputSystem->Update();

    const InputState& state = mInputSystem->GetState();

    // Process any keys here as desired...

    // Send state to all actor's ProcessInput...
}
```

With the `InputSystem` in place, you now have the basics needed to add support for several input devices. For each of these devices, you need to add a new class to encapsulate the state and add an instance of this class to the `InputState` struct.

## KEYBOARD INPUT

Recall that the `SDL_GetKeyboardState` function returns a pointer to the keyboard state. Notably, the return value of `SDL_GetKeyboardState` does not change throughout the lifetime of the application, as it points to internal SDL data. Therefore, to track the current state of the keyboard, you merely need a single pointer that you initialize once. However, because SDL overwrites the current keyboard state when you call `SDL_PollEvents`, you need a separate array to save the previous frame state.

This leads naturally to the member data in the declaration of `KeyboardState`, shown in Listing 8.2. You have a pointer that points to the current state and an array for the previous state. The size of the array corresponds to the size of the buffer that SDL uses for keyboard scan codes. For the member functions of `KeyboardState`, you provide both a method to get the basic current value of a key (`GetKeyValue`) and one that returns one of the four button states (`GetKeyState`). Finally, you make `InputSystem` a friend of `KeyboardState`. This makes it easy for `InputSystem` to directly manipulate the member data of `KeyboardState`.

### Listing 8.2 KeyboardState Declaration

Click here to view code image

```cpp
class KeyboardState
{
public:

// Friend so InputSystem can easily update it
friend class InputSystem;

// Get just the boolean true/false value of key
bool GetKeyValue(SDL_Scancode keyCode) const;

// Get a state based on current and previous frame
ButtonState GetKeyState(SDL_Scancode keyCode) const;

private:

// Current state
const Uint8* mCurrState;

// State previous frame
Uint8 mPrevState[SDL_NUM_SCANCODES];

};
```

Next, you add a `KeyboardState` instance called `Keyboard` to the member data of `InputState`:

```cpp
struct InputState
{
    KeyboardState Keyboard;
};
```

Next, you need to add code to both `Initialize` and `PrepareForUpdate` within `InputSystem`. In `Initialize`, you need to first set the `mCurrState` pointer and then also zero out the memory of `mPrevState` (because before the game starts, the keys have no previous state). You get the current state pointer from `SDL_GetKeyboardState`, and you can clear the memory with `memset`:

Click here to view code image

```cpp
// (In InputSystem::Initialize...)
// Assign current state pointer
mState.Keyboard.mCurrState = SDL_GetKeyboardState(NULL);
// Clear previous state memory
memset(mState.Keyboard.mPrevState, 0, SDL_NUM_SCANCODES);
```

Then in `PrepareForUpdate`, you need to copy all the "current" data to the previous buffer. Remember that when you call `PrepareForUpdate`, the "current" data is stale from the previous frame. This is because you call `PrepareForUpdate` when you're on a new frame but haven't called `SDL_PollEvents` yet. This is critical because `SDL_PollEvents` is what updates the internal SDL keyboard state data (which you're pointing to with `mCurrState`). So, before SDL overwrites the current state, use `memcpy` to copy from the current buffer to the previous buffer:

Click here to view code image

```cpp
// ( In InputSystem::PrepareForUpdate... )
memcpy(mState.Keyboard.mPrevState,
       mState.Keyboard.mCurrState,
       SDL_NUM_SCANCODES);
```

Next, you need to implement the member functions in `KeyboardState`. `GetKeyValue` is straightforward. It simply indexes into the `mCurrState` buffer and returns `true` if the value is 1 and `false` if the value is 0.

The `GetKeyState` function, shown in Listing 8.3, is slightly more complex. It uses both the current frame's and previous frame's key state to determine which of the four button states to return. This simply maps the entries in Table 8.1 into source code.

### Listing 8.3 `KeyboardState::GetKeyState` Implementation

Click here to view code image

```cpp
ButtonState KeyboardState::GetKeyState(SDL_Scancode keyCode)
{
    if (mPrevState[keyCode] == 0)
    {
        if (mCurrState[keyCode] == 0)
        { return ENone; }
        else
        { return EPressed; }
    }
    else // Prev state must be 1
    {
        if (mCurrState[keyCode] == 0)
        { return EReleased; }
        else
        { return EHeld; }
    }
}
```

With this `KeyboardState` code, you can still access the value of a key with the `GetKeyValue` function. For example, the following checks if the current value of the spacebar is `true`:

Click here to view code image

```cpp
if (state.Keyboard.GetKeyValue(SDL_SCANCODE_SPACE))
```

However, the advantage of the `InputState` object is that you can also query the button state of a key. For example, the following code in `Game::ProcessInput` detects if the button state of the Escape key is `EReleased`, and it exits only at that point:

Click here to view code image

```cpp
if (state.Keyboard.GetKeyState(SDL_SCANCODE_ESCAPE) == EReleased)
{
    mIsRunning = false;
}
```

This means that initially pressing Escape does not immediately quit the game, but releasing the key causes the game to quit.

## MOUSE INPUT

For mouse input, there are three main types of input to focus on: button input, movement of the mouse, and movement of the scroll wheel. The button input
