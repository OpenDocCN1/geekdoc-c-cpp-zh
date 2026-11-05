
![](img/e4b578cd512539e7261e070d87b6550a_282_0.png)

*图 15.1 Blaster 游戏示例。*

![](img/e4b578cd512539e7261e070d87b6550a_282_1.png)

*图 15.2 Blaster 游戏的游戏结构。*

## 15.1 构成要素

Blaster 游戏使用以下构成要素：

- 1. 主菜单 – 菜单代码基于第 11 章第 11.1.2 节中的 MenuWithProfiles.cs。我们使用的模板菜单与我们在第 2 章中为 RunMan 游戏菜单使用的模板相同。
- 2. 场景加载器 – MultiLevelLoader.cs 用于场景加载，派生自 LevelLoader.cs（见第 13 章第 13.2 节）。LevelVars 类用于保存要加载的关卡信息。
- 3. BlasterGameManager 派生自 BaseGameManager，并在游戏开始时使用 BaseUserManager 进行生成（以及玩家有多少条生命等）。它还将使用来自 GPC_Framework/COMMON/USER INTERFACE 的 ScreenAndAudioFader 类来淡入或淡出场景。
- 4. 音效控制器 – 来自第 9 章第 9.1 节的 BaseSoundController 类用于播放游戏结束和关卡完成音效，而各个预制体则发出自己的音效，如射击声或爆炸声。
- 5. 用户界面 – 游戏内用户界面将派生自第 11 章第 11.1 节的 CanvasManager 脚本，以淡入或淡出 UI 元素。
- 6. BlasterPlayer 类（玩家的主要类）派生自 BasePlayerStatsController，后者也使用 BaseUserManager 为玩家提供生命值和分数等统计数据。
- 7. CameraThirdPerson 使用 BaseCameraController。

请注意，本书其他地方已详细描述的这些组件在本章中不会重复介绍，预计您会在各自的章节中找到它们。

## 15.2 主菜单场景概述

主菜单由位于 GPC_Framework/TemplateScenes 文件夹中的模板主菜单制作而成。

主菜单加载另一个充当游戏加载器的场景。游戏加载场景再加载两个额外的场景——一个核心场景和一个额外的关卡场景。场景加载器将核心场景和关卡场景合并并启动游戏。

## 15.3 核心场景概述

游戏的主要部分分为两个场景。一个包含关卡——即墙壁和敌人生成位置（如果愿意，可以扩展为完整的 3D 环境）——另一个是核心场景，包含游戏逻辑以及游戏中每个场景共有的任何内容，如竞技场的主要外墙和摄像机。

在大多数情况下，您会将完整的 3D 关卡放入关卡场景中，但在这种游戏中我们将竞技场和灯光放在核心场景中。我们这样做只是因为竞技场（游戏区域的外墙和地面平面）在所有关卡中都是共享的。如果您将此作为自己游戏的模板，您很可能会从核心场景中移除竞技场和灯光，并将所有关卡对象保留在关卡场景中。

### 15.3.1 BlasterGameManager 类

BlasterGameManager 是游戏的中央通信枢纽。它派生自 BaseGameManager，并重写了一些基函数，同时添加了一些自己的函数。

BlasterGameManager 派生自 BaseGameManager，而 BaseGameManager 又派生自 MonoBehaviour，以便它可以利用 Unity 内置的对 Update()、Awake() 和 Start() 等函数的调用：

```csharp
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;
using GPC;

public class BlasterGameManager : BaseGameManager
{
    public Transform _playerPrefab;
    public Transform _playerSpawnpoint;
    public BaseCameraController _cameraManager;
    public Transform _thePlayer;
    public BlasterPlayer _thePlayerScript;
    public List<BlasterPlayer> _playerScripts;
    public BlasterUI_Manager ui_Manager;
    public ScreenAndAudioFader _fader;
    public int enemyCounter;
    public BaseUserManager _baseUserManager;
    public BaseSoundManager _soundComponent;
}
```

上面，我们需要 System.Collections.Generic 来使用列表，UnityEngine.SceneManagement 在游戏结束时返回主菜单，以及 GPC 用于框架。

上面的类声明显示我们派生自 BaseGameManager。接下来，我们跳过除一个之外的所有变量声明并进入构造函数：

```csharp
public static BlasterGameManager instance { get; private set; }

public void Awake()
{
    instance = this;
}
```

与本书中制作的任何其他单例风格类一样，上文我们声明了一个名为 instance 的变量，该变量在 Awake() 函数中被设置为此实例。

```csharp
private void Start()
{
    // start with audio muted and fade covering the screen
    _fader.SetFadedOut();
    // schedule a fade in after a little time
    Invoke("StartFadeIn", 1f);
    SetTargetState(Game.State.Loaded);
}
```

当 Start() 函数运行时，由 Unity 自动调用，我们需要做的第一件事是确保屏幕初始为全黑，以便实现良好的淡入效果。为此，我们调用 _fader 中的 ScreenAndAudioFader 类引用并运行其 SetFadedOut() 函数。这将立即把淡入淡出器的状态设为黑色。

下一行是 Invoke 语句，将在一秒后调用 StartFadeIn() 函数。我们延迟此操作以使其工作良好——如果

```csharp
void CreatePlayers()
{
    // refresh our player script list
    _playerScripts = new List<BlasterPlayer>();
    List<UserData> _playerInfo = _baseUserManager.GetPlayerList();
    // for editor testing...
    if (_playerInfo.Count == 0)
        _baseUserManager.AddNewPlayer();
}
```

上面，我们通过创建一个新的 List 来开始 CreatePlayers()，以存储对玩家的引用。为了确定需要创建哪些玩家并获取其统计数据，我们使用 BaseUserManager 类（见本书第 4 章第 4.3 节）。BaseUserManager 应包含游戏要创建的玩家列表，我们可以通过 BaseUserManager.GetPlayerList() 函数获取。GetPlayerList() 将返回一个 UserData 对象列表（用户统计数据——有关此内容的更多信息，请参阅第 4 章第 4.4 节）。

如果我们在编辑器中测试游戏且尚未通过主菜单，BaseUserManager 中的玩家列表将为空。这会在此处导致问题，因此与其使测试变得不可能，我在上面添加了代码来检查 _playerInfo.Count 是否为 0（我们的玩家列表为空），如果是，则使用 BaseUserManager.AddNewPlayer() 添加一个新玩家。

```csharp
// iterate through the player list and add the players to the scene ..
for (int i = 0; i < _playerInfo.Count; i++)
{
    // remember to name your spawnpoints correctly! PlayerSpawnPoint_1, PlayerSpawnPoint_2 etc. depending on how many players!
    string spawnPointString = "PlayerSpawnPoint_" + (i + 1).ToString();
    _playerSpawnpoint = GameObject.Find(spawnPointString).transform;
}
```

下一步是遍历从 BaseUserManager 获取的玩家列表并为每个玩家生成一个角色。但在生成玩家之前，我们需要确定放置位置，为此，关卡场景应至少包含一个名为 PlayerSpawnPoint_ 后跟数字的生成点。在示例场景中，生成点名为 PlayerSpawnPoint_1。

上面，我们构造一个名为 spawnPointString 的字符串来查找生成位置。一旦获得该字符串，就会使用 GameObject.Find 将 _playerSpawnpoint（一个 Transform 类型变量）填充为其找到的 GameObject 的 Transform。

```csharp
_thePlayer = Instantiate(_playerPrefab, _playerSpawnpoint.position, _playerSpawnpoint.rotation, transform);
```

上面，玩家被实例化，使用 _playerPrefab 预制体（在检查器中设置）以及 _playerSpawnpoint Transform 的位置和旋转。请注意，我们在此处还设置了要实例化对象的父级。如果您不像这样为新实例化的对象设置父级，由于 Unity 处理合并的核心和关卡场景初始化的方式，新 GameObject 将
