

头文件 `fmod_studio.hpp` 定义了 FMOD Studio API 类型。但是，为了避免这个包含，`AudioSystem.h` 反而为 FMOD 类型创建了前向声明。这样，你只需要在 `AudioSystem.cpp` 中包含 FMOD 头文件。

初始化 FMOD（由 `AudioSystem::Initialize` 处理）涉及多个步骤。首先，调用 `Debug_Initialize` 来设置错误日志：

点击此处查看代码图片

```
FMOD::Debug_Initialize(
    FMOD_DEBUG_LEVEL_ERROR, // Log only errors
    FMOD_DEBUG_MODE_TTY // Output to stdout
);
```

`Debug_Initialize` 的第一个参数控制日志消息的详细程度。（默认值相当详细。）第二个参数指定写入日志消息的位置。在此示例中，日志消息写入 `stdout`。对于带有自定义调试代码的游戏，也可以为所有 FMOD 日志消息声明自定义回调函数。

> **注意**
> 初始化调试日志仅在使用 FMOD 的日志构建版本时才相关，本章即为这种情况。在开发期间启用错误日志非常有用，但游戏的发布版本不应包含日志。

接下来，使用以下代码构建 FMOD Studio 系统的实例：

点击此处查看代码图片

```
FMOD_RESULT result;

result = FMOD::Studio::System::create(&mSystem);

if (result != FMOD_OK)
{
    SDL_Log("Failed to create FMOD system: %s",
        FMOD_ErrorString(result));

    return false;
}
```

请注意，该函数调用返回一个 `FMOD_RESULT`。FMOD 函数始终返回一个结果值，以便调用者知道一切是否正常。`FMOD_ErrorString` 函数将错误代码转换为人类可读的消息。在此示例中，如果系统创建失败，`AudioSystem::Initialize` 返回 `false`。

构建系统后，下一步是在 FMOD 系统上调用 `initialize`：

点击此处查看代码图片

```
result = mSystem->initialize(
    512, // Max number of concurrent
    FMOD_STUDIO_INIT_NORMAL, // Use default settings
    FMOD_INIT_NORMAL, // Use default settings
    nullptr // Usually null
);
// Validate result == FMOD_OK...
```

此处的第一个参数指定最大通道数。接下来的两个参数可以调整 FMOD Studio 和 FMOD Low Level API 的行为。目前，请使用默认参数。如果你想使用额外的驱动程序数据，则使用最后一个参数，但由于通常不需要，因此此参数通常是 `nullptr`。

> **注意**
> FMOD 使用一种命名约定，其中成员函数以小写字母开头。这与本书的命名约定不同，后者对成员函数的首字母使用大写字母。

最后，获取并保存 Low Level 系统指针以完成初始化：

点击此处查看代码图片

```
mSystem->getLowLevelSystem(&mLowLevelSystem);
```

目前，AudioSystem 的 Shutdown 和 Update 函数各只进行一次函数调用。Shutdown 调用 `mSystem->release()`，而 Update 调用 `mSystem->update()`。FMOD 要求每帧调用一次更新函数。该函数执行诸如更新 3D 音频计算之类的操作。

与 Renderer 类似，然后将 AudioSystem 指针作为成员变量添加到 Game 中：

点击此处查看代码图片

```
class AudioSystem* mAudioSystem;
```

Game::Initialize 随后创建并调用 `mAudioSystem->Initialize()`，UpdateGame 调用 `mAudioSystem->Update(deltaTime)`，Shutdown 调用 `mAudioSystem->Shutdown()`。

为方便起见，Game::GetAudioSystem 函数返回 AudioSystem 指针。

有了这些函数，FMOD 现在可以初始化和更新。当然，目前还没有声音播放。

## 银行和事件

在 FMOD Studio 中，事件对应游戏中播放的声音。一个事件可以有多个关联的声音文件、参数、关于事件时机的信息等等。游戏不是直接播放声音文件，而是播放这些事件。

**银行** 是事件、采样数据和流数据的容器。**采样数据** 是事件引用的原始音频数据。这些数据来自声音设计师导入 FMOD Studio 的声音文件（例如 WAV 或 OGG 文件）。在运行时，采样数据要么预加载，要么按需加载。但是，在关联的采样数据加载到内存之前，事件无法播放。大多数游戏内音效都使用采样数据。**流数据** 是分小块流入内存的采样数据。使用流数据的事件可以在不预加载数据的情况下开始播放。音乐和对话文件通常使用流数据。

声音设计师在 FMOD Studio 中创建一个或多个银行。然后游戏运行时需要加载这些银行。加载银行后，其中包含的事件即可访问。

FMOD 中与事件关联的有两个不同的类。**EventDescription** 包含关于事件的信息，例如其关联的采样数据、音量设置、参数等等。**EventInstance** 是事件的活动实例，它负责播放事件。换句话说，`EventDescription` 就像事件的一种类型，而 `EventInstance` 是该类型的一个实例。例如，如果存在一个爆炸事件，它在全局范围内将只有一个 `EventDescription`，但可以根据活动爆炸实例的数量拥有任意数量的 `EventInstances`。

为了跟踪已加载的银行和事件，你需要在 AudioSystem 的私有数据中添加两个映射：

点击此处查看代码图片

```
// Map of loaded banks
std::unordered_map<std::string, FMOD::Studio::Bank*>

// Map of event name to EventDescription
std::unordered_map<std::string, FMOD::Studio::EventDescription*>
```

两个映射都使用字符串作为键。mBanks 中的字符串是银行的文件名，而 mEvents 中的字符串是 FMOD 为事件分配的名称。FMOD 事件的名称采用路径形式，例如 event:/Explosion2D。

## 加载/卸载银行

加载银行最少只需在 mSystem 对象上调用 loadBank 函数。但是，这不会加载采样数据，也无法轻松访问事件描述。在 AudioSystem 中创建一个名为 LoadBank 的新函数是有意义的，如清单 7.2 所示，它比最小的 loadBank 调用多做了一些事情。银行加载后，你将银行添加到 mBanks 映射中。然后加载银行的采样数据。接着使用 getEventCount 和 getEventList 获取银行中所有事件描述的列表。最后，将每个事件描述添加到 mEvents 映射中，以便轻松访问。

### 清单 7.2 AudioSystem::LoadBank 实现

点击此处查看代码图片

```
void AudioSystem::LoadBank(const std::string& name)
{
    // Prevent double-loading
    if (mBanks.find(name) != mBanks.end())
    {
        return;
    }

    // Try to load bank
    FMOD::Studio::Bank* bank = nullptr;
    FMOD_RESULT result = mSystem->loadBankFile(
        name.c_str(), // File name of bank
        FMOD_STUDIO_LOAD_BANK_NORMAL, // Normal loading
        &bank // Save pointer to bank
    );

    const int maxPathLength = 512;

    if (result == FMOD_OK)
    {
        // Add bank to map
        mBanks.emplace(name, bank);

        // Load all non-streaming sample data
        bank->loadSampleData();

        // Get the number of events in this bank
        int numEvents = 0;
        bank->getEventCount(&numEvents);

        if (numEvents > 0)
        {
            // Get list of event descriptions in this bank
            std::vector<FMOD::Studio::EventDescription*> events(numEvents);
            bank->getEventList(events.data(), numEvents);
            char eventName[maxPathLength];
            for (int i = 0; i < numEvents; i++)
            {
                FMOD::Studio::EventDescription* e = events[i];
                // Get the path of this event (like event:/Explosion2D)
                e->getPath(eventName, maxPathLength, nullptr);
                // Add to event map
                mEvents.emplace(eventName, e);
            }
        }
    }
}
```

同样，你创建一个 `AudioSystem::UnloadBank` 函数。该函数首先从 `mEvents` 映射中删除银行的所有事件，卸载采样数据，卸载银行，并从 `mBanks` 映射中删除银行。

为了方便清理，你还创建一个 `AudioSystem::UnloadAllBanks` 函数。该函数只是卸载所有银行并清空 `mEvents` 和 `mBanks`。

每个 FMOD Studio 项目都有两个名为 "Master Bank.bank" 和 "Master Bank.strings.bank" 的默认银行文件。除非先加载这两个主银行，否则 FMOD Studio 运行时无法访问任何其他银行或事件。由于主银行始终存在，你在 `AudioSystem::Initialize` 中使用以下代码加载它们：

