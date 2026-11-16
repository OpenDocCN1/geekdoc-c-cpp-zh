
要解决这个问题，可以让 `InputSystem` 类在名为 `InputState` 的辅助类中填充数据。然后可以通过 `ProcessInput` 函数将此 `InputState` 以 `const` 引用的形式传递给角色/组件。还可以向 `InputState` 添加几个辅助函数，以便轻松查询角色/组件关心的任何状态。

清单 8.1 显示了相关部分的初始声明。首先，声明一个 `ButtonState` 枚举，对应表 8.1 中概述的四种不同状态。接下来，声明一个 `InputState` 结构体（目前没有成员）。最后，声明 `InputSystem`，它包含 `Initialize`/`Shutdown` 函数（类似于 `Game`）。它还有一个在 `SDL_PollEvents` 之前调用的 `PrepareForUpdate` 函数，然后是一个在轮询事件后调用的 `Update` 函数。`GetState` 函数返回其作为成员数据持有的 `InputState` 的 `const` 引用。

## 清单 8.1 基本 `InputSystem` 声明

点击此处查看代码图片

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

要将此代码集成到游戏中，请向 Game 的成员数据中添加一个名为 mInputSystem 的 InputSystem 指针。Game::Initialize 分配并初始化 InputSystem，Game::Shutdown 关闭并删除它。

接下来，将 Actor 和 Component 中 ProcessInput 的声明更改为以下内容：

点击此处查看代码图片

```cpp
void ProcessInput(const InputState& state);
```

请记住，在 Actor 中，ProcessInput 不可覆盖，因为它会对所有附加的组件调用 ProcessInput。但是，角色还有一个可覆盖的 ActorInput 函数，用于处理特定于该角色的任何输入。因此，你同样更改 ActorInput 的声明，使其接受一个常量 InputState 引用。

最后，Game::ProcessInput 的实现更改为以下步骤大纲：

点击此处查看代码图片

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

有了 `InputSystem`，你现在具备了添加对多种输入设备支持所需的基础。对于这些设备中的每一个，你都需要添加一个新类来封装状态，并将该类的实例添加到 `InputState` 结构体中。

## 键盘输入

请记住，`SDL_GetKeyboardState` 函数返回一个指向键盘状态的指针。值得注意的是，`SDL_GetKeyboardState` 的返回值在应用程序生命周期内不会改变，因为它指向内部 SDL 数据。因此，要跟踪键盘的当前状态，你只需要一个初始化一次的单一指针。但是，因为当你调用 `SDL_PollEvents` 时 SDL 会覆盖当前键盘状态，所以你需要一个单独的数组来保存上一帧的状态。

这自然导致了 `KeyboardState` 声明中的成员数据，如清单 8.2 所示。你有一个指向当前状态的指针和一个用于上一状态的数组。数组的大小对应于 SDL 用于键盘扫描码的缓冲区大小。对于 `KeyboardState` 的成员函数，你提供了一个获取键基本当前值的方法（`GetKeyValue`）和一个返回四个按钮状态之一的方法（`GetKeyState`）。最后，你将 `InputSystem` 设为 `KeyboardState` 的友元。这使得 `InputSystem` 可以轻松直接操作 `KeyboardState` 的成员数据。

### 清单 8.2 KeyboardState 声明

点击此处查看代码图片

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

接下来，将一个名为 `Keyboard` 的 `KeyboardState` 实例添加到 `InputState` 的成员数据中：

```cpp
struct InputState
{
    KeyboardState Keyboard;
};
```

接下来，你需要在 `InputSystem` 的 `Initialize` 和 `PrepareForUpdate` 中添加代码。在 `Initialize` 中，你需要先设置 `mCurrState` 指针，然后还要将 `mPrevState` 的内存清零（因为游戏开始前，按键没有之前的状态）。你从 `SDL_GetKeyboardState` 获取当前状态指针，并可以使用 `memset` 清除内存：

点击此处查看代码图片

```cpp
// (In InputSystem::Initialize...)
// Assign current state pointer
mState.Keyboard.mCurrState = SDL_GetKeyboardState(NULL);
// Clear previous state memory
memset(mState.Keyboard.mPrevState, 0, SDL_NUM_SCANCODES);
```

然后在 `PrepareForUpdate` 中，你需要将所有“当前”数据复制到上一缓冲区。请记住，当你调用 `PrepareForUpdate` 时，“当前”数据是上一帧的过时数据。这是因为你在新帧上调用 `PrepareForUpdate`，但尚未调用 `SDL_PollEvents`。这很关键，因为 `SDL_PollEvents` 是更新内部 SDL 键盘状态数据（你正通过 `mCurrState` 指向它）的东西。因此，在 SDL 覆盖当前状态之前，使用 `memcpy` 从当前缓冲区复制到上一缓冲区：

点击此处查看代码图片

```cpp
// ( In InputSystem::PrepareForUpdate... )
memcpy(mState.Keyboard.mPrevState,
       mState.Keyboard.mCurrState,
       SDL_NUM_SCANCODES);
```

接下来，你需要实现 `KeyboardState` 中的成员函数。`GetKeyValue` 很简单。它只是索引到 `mCurrState` 缓冲区，如果值为 1 则返回 `true`，如果值为 0 则返回 `false`。

如清单 8.3 所示，`GetKeyState` 函数稍微复杂一些。它同时使用当前帧和上一帧的按键状态来确定返回哪个按钮状态。这只是将表 8.1 中的条目映射到源代码中。

### 清单 8.3 `KeyboardState::GetKeyState` 实现

点击此处查看代码图片

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

有了这个 `KeyboardState` 代码，你仍然可以使用 `GetKeyValue` 函数访问键的值。例如，以下代码检查空格键的当前值是否为 `true`：

点击此处查看代码图片

```cpp
if (state.Keyboard.GetKeyValue(SDL_SCANCODE_SPACE))
```

但是，`InputState` 对象的优势在于你还可以查询键的按钮状态。例如，`Game::ProcessInput` 中的以下代码检测 Esc 键的按钮状态是否为 `EReleased`，并且仅在该点退出：

点击此处查看代码图片

```cpp
if (state.Keyboard.GetKeyState(SDL_SCANCODE_ESCAPE) == EReleased)
{
    mIsRunning = false;
}
```

这意味着最初按下 Esc 键不会立即退出游戏，但释放按键会导致游戏退出。

## 鼠标输入

对于鼠标输入，有三种主要类型的输入需要关注：按钮输入、鼠标移动和滚轮移动。按钮输入
