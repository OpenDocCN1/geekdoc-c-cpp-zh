
代码中值得注意的唯一之处在于我们使用了 GPC 框架命名空间，并且使用了 Unity 的 RequireComponent() 来确保在同一个 GameObject 上附加了 BaseProfileManager 组件。

```
public class MenuWithProfiles : BaseMainMenuManager
{
    public BaseProfileManager _profileManager;
    public override void Init()
    {
        _profileManager = GetComponent<BaseProfileManager>();
    }
}
```

如前所述，类继承自 BaseMainMenuManager 以提供其菜单功能。接下来是一个变量 _profileManager，用于存储对 BaseProfileManager 组件的引用，该引用在 Init() 函数中使用 GetComponent() 设置以查找它。

```
// init the profile manager to get preferences from
_profileManager.Init();
```

ProfileManager 需要初始化，因为它存储并访问配置文件数据，如果在数据被加载或首次设置之前，我们将无法访问数据。

```
// need to grab profile volumes before base.Init sets up the UI sliders
LoadProfileVolumes();
```

在此函数中，我们调用函数 LoadProfileVolumes() 从 ProfileManager 获取音量信息并在 AudioMixer 上设置音量。

```
// now we can run the base init - we've set up the profile info
base.Init();
}
```

由于此类派生自 BaseMainMenuManager，一旦它在 Init() 函数中完成了自己的额外初始化，我们就需要调用基类的 Init()，以便主菜单也能运行其主菜单的初始化。

```
void LoadProfileVolumes()
{
    // get volume values from profile manager
    _theAudioMixer.SetFloat("SoundVol",
    _profileManager.GetSFXVolume());

    _theAudioMixer.SetFloat("MusicVol",
    _profileManager.GetMusicVolume());
}
```

以上，LoadProfileVolumes() 函数使用 AudioMixer 上的 SetFloat 来设置其 SoundVol 属性。音量级别来自对 ProfileManager 的 GetSFXVolume() 函数的调用，该级别要么是在上一次运行中设置并保存到保存配置文件中的级别，要么是其默认值 0。此值以分贝为单位，因此 0 并不是静音，而是 AudioMixer 在 Unity 中的默认可听音量。

以上，设置音乐音量的过程与设置音效相同，只是音量来自 GetMusicVolume()，我们这次设置 AudioMixer 上的 MusicVol 属性以影响音乐级别。

```csharp
public override void SetSFXVolumeLevel(float aValue)
{
    float dbVol = Mathf.Log10(aValue) * 20f;
    _theAudioMixer.SetFloat("SoundVol", dbVol);
    // write the volume change to the profile
    _profileManager.SetSFXVolume(dbVol);
}
public override void SetMusicVolumeLevel(float aValue)
{
    float dbVol = Mathf.Log10(aValue) * 20f;
    _theAudioMixer.SetFloat("MusicVol", dbVol);
    // write the volume change to the profile
    _profileManager.SetMusicVolume(dbVol);
}
```

SetSFXVolumeLevel() 和 SetMusicVolumeLevel() 函数在派生自的 BaseMainMenuManager 类中声明。这里，我们重写基类的版本以添加对 _profileManager 对象上的 SetSFXVolume() 和 SetMusicVolume() 的调用。这将在保存配置文件时与保存配置文件一起保存音量级别。

```csharp
public override void OptionsBackToMainMenu()
{
    // save updated settings
    _profileManager.SaveProfiles();
    // return to main menu from options
    _canvasManager.LastCanvas();
}
```

最后，对于 MenuWithProfiles 类，我们重写来自基类的 OptionsBackToMainMenu()，以便在用户退出选项菜单返回主菜单时保存配置文件。调用 SaveProfiles() 将保存 ProfileManager 存储数据的所有配置文件（默认为 3 个配置文件）。

### 11.3 游戏内用户界面

本书中的示例游戏处理用户界面的方式是为 UI 操作（如更新分数显示的文本等）提供一个专用脚本，由 Game Manager 调用以将用户界面与其它游戏逻辑分离。

主游戏界面位于其自己的 Canvas 上，当我们需要执行诸如显示消息（例如游戏开始前准备就绪的消息）之类的操作时，消息位于其自己的 Canvas 上，这样我们就可以先淡出主游戏 Canvas。CanvasManager 用于在它们之间切换，并且它还通过在游戏首次启动时淡入主 UI 来提供很好的润色效果。

## 12 保存和加载配置文件

保存和加载用户数据可以通过多种方式处理。例如，您可能只将所有内容存储在一个静态类中，并在需要时将其转储到 JSON 文件中。也许您想使用 .xml 格式的文件，甚至是数据库？在本章中，我们将介绍一种保存和加载用户数据的方法，该方法使用 ScriptableObject 结合 JSON 作为其格式。ScriptableObject 包含一个数据类 ProfileData 的实例数组。ProfileData 类保存我们想要保存和加载到配置文件的全部内容。通过在 ScriptableObject 中使用 ProfileData 数组，我们可以轻松地加载并保存到多个保存配置文件。

本章中的系统使用保存槽，但没有示例用户界面来选择不同的槽。示例游戏只是使用第一个配置文件，但如果您决定进一步扩展并为多个槽构建界面，您可以调用 ChooseProfile(<slot number>) 来选择与您的用户界面对应的槽。

### 12.1 保存配置文件 ScriptableObject

我们使用 ScriptableObject 有两个原因。一个是为了使数据在游戏中的任何地方都易于访问——对 ScriptableObject 的引用就给了您对数据的引用。您可以修改 ScriptableObject 实例上的数据，无论从哪里访问它，数据都将与最新修改保持一致。使用 ScriptableObject 的第二个原因是我们可以在 Unity 编辑器中立即看到它更新，从而更容易调试存储。ScriptableObject 是存储数据并从任何地方访问它的绝佳方式。

您可以在文件夹 Assets/GPC_Framework/Scripts/COMMON/SCRIPTABLEOBJECTS 中找到此 ProfileScriptableObject.cs 文件。

此脚本引用的命名空间是 UnityEngine 和 System：

```
using UnityEngine;
using System;
namespace GPC
{
```

该类存在于 GPC 命名空间中，本书的框架使用该命名空间。您可以同样轻松地更改或删除本章脚本所在的命名空间，但我发现将所有内容放在这样的命名空间中很有帮助，这样 a) 您就知道脚本最初来自哪里，b) 脚本不会因变量名或函数名等而相互重叠。

```
[CreateAssetMenu(fileName = "ProfileData", menuName = "CSharpFramework/ProfileScriptableObject")]
```

以上，这是熟悉 ScriptableObjects 的人会认识的东西，尽管对刚开始使用它们的人来说可能没有多大意义。当我们声明一个 ScriptableObject 时，我们并不会像通常那样使用此类的一个实例。发生的情况是我们改为在 Unity 编辑器中创建一个对象，该对象将成为我们在游戏中使用 ScriptableObject。Unity 中创建的对象将保存并显示我们在脚本文件中概述的数据。

为了使 ScriptableObject 对像我们这样的 Unity 编辑器用户可访问，我们需要使用 CreateAssetMenu() 为 Unity 的菜单添加一个新菜单选项。在上面的情况下，我们向 CreateAssetMenu() 传递两个参数。它们是：

-   **文件名** – 当您使用菜单将 ScriptableObject 添加到项目时，这将被用作 ScriptableObject 的默认名称。
-   **菜单名称** – 这定义了该项在 Unity 菜单中应如何显示以及应位于何处。默认情况下，该项将出现在 Assets/Create 菜单中。然后，您可以在该文件夹内指定子文件夹以对菜单资源进行分类和组织。在上面的示例代码中，该资源将出现在 Assets/Create/CSharpFramework/ProfileScriptableObject 中。

```
[Serializable]
public class ProfileScriptableObject : ScriptableObject
{
    public Profiles theProfileData;
}
```

以上，代码块以 [Serializable] 开始。这非常重要，特别是因为我们正在保存和加载数据。序列化，简单来说，就是将此类这样的类作为适合传输的序列数据进行读取或写入，例如保存和加载到或从磁盘。如果我们不告诉 Unity 我们想要序列化什么，我们的配置文件保存和加载代码将无法工作。

类声明确保我们派生自 ScriptableObject，然后在类内部有一个用于 ProfileData 的单个变量声明。ProfileScriptableObject ScriptableObject 只需要这个名为 theProfileData 的单个变量。其类型 Profiles 引用在同一 C# 文件中接下来声明的名为 Profiles 的类：

```
[Serializable]
public class Profiles
```
