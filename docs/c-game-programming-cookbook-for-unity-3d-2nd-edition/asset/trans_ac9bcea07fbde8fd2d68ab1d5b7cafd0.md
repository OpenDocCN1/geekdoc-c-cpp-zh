

## 11.2.2 BaseMainMenuManager 脚本

BaseMainMenuManager 提供了处理主菜单的基本功能。BaseMainMenuManager 类比平时需要多一些额外的命名空间，它们是：

```
using UnityEngine;
using UnityEngine.Audio;
using UnityEngine.SceneManagement;
using UnityEngine.UI;
```

音量滑块需要访问 AudioMixer 对象，因此我们需要用到 UnityEngine.Audio。要在 Unity 中加载不同场景，我们使用 UnityEngine.SceneManagement 来访问 SceneManager 类。最后，上述用户界面组件只有在使用 UnityEngine.UI 命名空间时才能访问。

该类本身派生自 MonoBehaviour：

```
namespace GPC
{
    public class BaseMainMenuManager : MonoBehaviour
    {

```

接下来是变量声明：

```
public CanvasManager _canvasManager;
public AudioMixer _theAudioMixer;

public Slider _sfxSlider;
public Slider _musicSlider;
public string gameSceneName;
```

上面，我们首先引用 CanvasManager，用于显示和隐藏画布。AudioMixer 也需要在此脚本中被引用，以便我们能够通过滑块访问和设置其音量属性。接下来引用这些滑块。滑块本身使用 Unity 事件 On Value Changed() 来调用此类上更改 AudioMixer 音量级别的函数。该事件以及对应到此脚本函数的引用必须在 Inspector 中滑块的 Slider 组件上进行设置。

```
void Start()
{
    Init();
}
public virtual void Init()
{
    if (_canvasManager == null)
        Debug.LogError("You need to add a reference to a _canvasManager Component on your main menu Component!");
    // set the values of the UI (visible) sliders to those of the audio mixers
    SetupSliders();
    Invoke("ShowMainMenu", 0.5f);
}
```

上面，Start() 调用 Init()。Init() 检查 _canvasManager 中是否有引用，然后调用 SetupSliders() 来根据当前音量级别设置滑块值。最后，会调用一个在任意时间后显示主菜单的函数。我们使用延迟调用，这样菜单不会在场景加载后立即转换——如果能在转换开始前看到当前画面，看起来会更整洁一些。

```
```csharp
void SetupSliders()
{
    // now set the UI sliders to match the values in the mixer
    float value;
    _theAudioMixer.GetFloat("SoundVol", out value);
```
```

SetupSliders() 由上面的 Init() 函数调用，它首先从 _theAudioMixer 中引用的 AudioMixer 获取名为 SoundVol 的组的当前音量级别。默认情况下，AudioMixer 的任何属性都不会暴露给脚本，你需要在编辑器中设置。有关如何执行此操作的说明，请参见前面的第 9 章。

AudioMixer 以分贝为单位存储电平，范围从最小值 –80 到最大 20db，而滑块使用我们可以在 Inspector 中设置的任意值。在本书的示例中，我们使用 0 到 1 之间的值表示百分比。然而，我们的音量系统之所以复杂，不仅因为 AudioMixer 的范围是 –80 到 20，还因为分贝量不是线性的，而是对数的——这本质上意味着我们不能依赖最小和最大分贝之间的中点作为静音和响亮之间的中点。如果我们用滑块来设置分贝值，滑块与实际音量之间的关系就会偏离。当然，这不会是一个很直观的界面。用户期望滑块在 0 到 100% 音量之间呈线性比例，所以我们需要做一些工作来实现这一点。需要将 AudioMixer 值转换成我们可以使用的东西。

上面，我们从 AudioMixer 中获取音量并放入名为 value 的变量中，因此下一步是将 value 转换为百分比：

```
```csharp
_sfxSlider.value = DecibelToLinear(value);
```
```

下一部分代码以类似方式处理音乐音量，当然它使用了不同的滑块和 AudioMixer 上不同的公开属性（MusicVol）：

```
```csharp
_theAudioMixer.GetFloat("MusicVol", out value);
_musicSlider.value = DecibelToLinear(value);
}
```

接下来是两个用于根据滑块中的值设置音量的函数：

```
```csharp
public virtual void SetSFXVolumeLevel(float aValue)
{
    float dbVol = Mathf.Log10(aValue) * 20f;
```

上面，SetSFXVolumeLevel 接收通过 aValue 传入的百分比值，并将其转换为分贝。

```
```csharp
_theAudioMixer.SetFloat("SoundVol", dbVol);
}
```
```

AudioMixer.SetFloat() 用于将我们的 AudioMixer 的音量级别设置为 dbVol 中的分贝值。接下来，我们对音乐音量做同样的操作：

```
```csharp
public virtual void SetMusicVolumeLevel(float aValue)
{
    float dbVol = Mathf.Log10(aValue) * 20f;
    _theAudioMixer.SetFloat("MusicVol", dbVol);
}
```
```

上面，音乐音量的设置方式与我们之前设置声音音量的方式相同。

```
```csharp
private float DecibelToLinear(float dB)
{
    float linear = Mathf.Pow(10.0f, dB / 20.0f);
    return linear;
}
```
```

如本节前面所述，在此示例中，用户界面滑块的值在 0 到 1 之间。上面的实用函数 DecibelToLinear 将接收一个以分贝为单位的值，并返回一个 0 到 1 之间的数字，具体取决于音量应有多大或多小——范围在 -80 到 20db 之间。

```
```csharp
void ShowMainMenu()
{
    _canvasManager.TimedSwitchCanvas(2,0);
}
```
```

```
```csharp
public virtual void StartGame()
{
    _canvasManager.HideCanvas(0, false);
    _canvasManager.ShowCanvas(2, false);
    Invoke("LoadGameScene", 1f);
}
```
```

ShowMainMenu() 调用 CanvasManager 组件将活动画布从加载屏幕（本示例中索引为 2）切换到主菜单（索引为 0）。索引号指的是 MenuManager GameObject 上的 Canvas Manager 组件的 UI Canvas Groups 列表中画布的位置。

StartGame() 首先隐藏主菜单画布，然后继续显示加载屏幕。我们使用 Invoke() 调用将游戏安排在 1 秒后加载，这给了 CanvasManager 足够的时间淡出菜单并在跳转到下一个场景之前淡入加载屏幕。

```
```csharp
public virtual void LoadGameScene()
{
    // Load your game here!
    SceneManager.LoadScene(gameSceneName);
}
```
```

LoadGameScene() 正是这样做的，它利用 SceneManager.LoadScene() 来加载场景。要加载的场景名称存储在 gameSceneName 中——这是一个你可以在 Inspector 中设置的字符串，这样可以更容易地让菜单用于不同的游戏，而无需修改任何代码。

```
```csharp
public virtual void ShowOptions()
{
    // switch to options menu
}
```
```

```
```csharp
    _canvasManager.TimedSwitchCanvas(0, 1);
}

public virtual void ShowExitConfirm()
{
    _canvasManager.TimedSwitchCanvas(0, 3);
}

public virtual void CloseExitConfirm()
{
    _canvasManager.TimedSwitchCanvas(3, 0);
}
```
```

上面，三个函数 ShowOptions()、ShowExitConfirm() 和 CloseExitConfirm() 都使用 CanvasManager.TimedSwitchCanvas() 从一个画布切换到另一个画布。ShowOptions() 和 ShowExitConfirm() 从主菜单切换到它们各自的画布，而 CloseExitConfirm() 从退出确认画布（3）切换回主菜单。

```
```csharp
public virtual void ExitGame()
{
    // close the app down
    Application.Quit();
}
```
```

ExitGame() 使用 Application.Quit() 退出游戏，这只会发生在独立构建中。在编辑器中它不会做任何事情。

```
```csharp
public virtual void OptionsBackToMainMenu()
{
    // return to main menu from options
    _canvasManager.LastCanvas();
}

public virtual void BackToMainMenu()
{
    // return to main menu from options
    _canvasManager.LastCanvas();
}
}
```

上面的最后两个函数处理返回主菜单的问题，使用 CanvasManager.LastCanvas() 函数隐藏当前画布并显示上一个画布。

## 11.2.3 结合 BaseMainMenuManager 与 ProfileManager 脚本来保存和加载音频设置

BaseMainMenuManager.cs 脚本负责菜单功能，但它没有内置的保存或加载音频设置的方法。本书中的框架包含一个 ProfileManager，专门用于处理用户配置文件以及游戏数据的保存和加载。我们将在此节中构建的类 MenuWithProfiles 使用 ProfileManager 将音量值保存为用户数据的一部分，并继承自 BaseMainMenuManager。

MenuWithProfiles 的开头如下：

```
```csharp
using UnityEngine;
using GPC;

[RequireComponent(typeof(BaseProfileManager))]
```

