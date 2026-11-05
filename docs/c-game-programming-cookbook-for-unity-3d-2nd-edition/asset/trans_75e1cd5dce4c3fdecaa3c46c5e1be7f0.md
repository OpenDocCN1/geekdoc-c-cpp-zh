
我们遍历 _playerList 中的所有玩家，并做两件事：第一件事是将 AIControlled 设置为 true；如果这是我们的玩家载具，它现在将被 AI 接管。接下来，我们使用 GetComponent() 查找该载具上的 RaceInputController 组件。这些都在一行中完成，因此我们假设所有载具都会有 RaceInputController；如果不是这样，这一行将产生错误。一旦我们使用 GetComponent 找到 RaceInputController，就在其上调用 SetInputType()。SetInputType 使用枚举器 RaceInputController.InputTypes（该组件支持的输入类型列表），在这里我们将载具的输入类型设置为 RaceInputController.InputTypes.noInput，这样用户将不再能够对载具的驾驶方式施加任何输入。

```
if (!doneFinalMessage)
{
    doneFinalMessage = true;
    _soundController.PlaySoundByIndex(2);
    // show final text
    _uiManager.ShowFinalMessage();
    // drop out of the race scene completely in
    Invoke("FinishRace", 10);
}
```

在上面的代码中，doneFinalMessage 是一个布尔值，我们检查它以确保这段代码在一场比赛中只会运行一次。重复调用本不应发生，但以防万一，我们的 doneFinalMessage 会确保代码不会陷入反复调用却永远无法完成的循环。

我们在条件的花括号内将 doneFinalMessage 设置为 true，然后通过 _soundController 播放声音，让玩家知道比赛已完成。_uiManager.ShowFinalMessage() 将向用户显示“比赛结束”消息，最后我们安排完全关闭场景——使用 Invoke() 在 10 秒后调用 FinishRace()。

被调用时，FinishRace() 将加载主菜单，从而有效地完全结束游戏：

```
void FinishRace()
{
    SceneManager.LoadScene(mainMenuSceneName);
}
```

ShowCount1()、ShowCount2() 和 ShowCount3() 函数会在比赛开始时的 3、2、1 倒计时期间切换用于显示数字的用户界面对象的激活状态，并且每个函数都会通过 BaseSoundController 组件播放声音：

```
void ShowCount1()
{
    _uiManager.ShowCount(1);
    _soundController.PlaySoundByIndex(0);
}
void ShowCount2()
{
    _uiManager.ShowCount(2);
    _soundController.PlaySoundByIndex(0);
}
```

```
void ShowCount3()
{
    _uiManager.ShowCount(3);
    _soundController.PlaySoundByIndex(0);
}
```

HideCount() 会隐藏所有 3、2、1 倒计时图像：

```
void HideCount()
{
    _uiManager.ShowCount(0);
}
```

Race Game Manager 类的下一部分是一个用于在关卡场景中查找玩家起点的函数：

```
void GetStartPoints()
{
    _startPoints = new List<Transform>();
}
```

你可能还记得，这个游戏每个关卡分为两个场景——包含游戏逻辑的核心场景，以及包含环境本身和起始位置等关卡特定内容的关卡场景。由于我们在运行时加载关卡，无法在编辑器中通过 Inspector 设置起始位置（因为它们会随关卡变化），因此自动化系统是必要的。

在上面的代码中，GetStartPoints() 首先在变量 _startPoints 中新建一个 List。这是 SetupPlayers() 函数使用的一个变量，因为该函数会创建玩家、将它们添加到场景中，并且需要为每个玩家提供一个起始位置。

```
GameObject _startParent =
GameObject.Find("StartPoints");
```

我们玩家的起始点被设置为名为 StartPoints 的对象的子对象。起始点 GameObject 本身叫什么并不太重要，只要它们是名为 StartPoints 的 GameObject 的子对象即可。原因是我们使用 GameObject.Find() 在场景中查找名为 StartPoints 的 GameObject。找到之后，我们像这样遍历它的所有子对象：

```
foreach (Transform sp in _startParent.transform)
{
    _startPoints.Add(sp);
}
```

上面的 foreach 循环会遍历 StartPoints GameObject 下的所有 Transform——但需要注意的是，此方法不是递归的；如果任何起始点位于更下一层（即 StartPoints 的子对象的子对象），它们将被忽略。

当循环遍历每个子对象时，我们使用 _startPoints.Add() 将它们添加到我们的起始点 List 中。在此函数结束时，_startPoints 应该是一个 List，其中包含任何已打开场景中的所有起始点。

```
void GetWaypointsController()
{
    _waypointController =
FindObjectOfType<WaypointsController>();
}
```

在上面的代码中，我们使用 Unity 内置函数 FindObjectOfType() 查找附有 WaypointsController 组件的 GameObject。FindObjectOfType() 将返回它找到的第一个——幸运的是，在这个游戏的任何关卡中都应该只有一个 WaypointsController。它找到的第一个 WaypointsController 将是我们使用的那个。

为了向用户隐藏或显示主玩家在赛道上逆行的消息；UpdateWrongWay() 函数如下：

```csharp
public void UpdateWrongWay ( bool isWrongWay )
{
    if( isWrongWay==oldIsWrongWay )
        return;
```

为了跟踪变化，我们有两个变量：oldIsWrongWay 和 isWrongWay。我们在该函数末尾设置 oldIsWrongWay。随着游戏进行，该函数会被反复调用，因此如果 isWrongWay 不等于 oldIsWrongWay，我们就知道从上一次调用到这一次调用之间发生了变化。当 isWrongWay 和 oldIsWrongWay 相同时，我们知道自上次更新显示以来，玩家是否逆行的状态没有改变。在上面的情况下，当 isWrongWay==oldIsWrongWay 时，我们可以直接退出此函数。

如果 isWrongWay 不等于 oldIsWrongWay，我们就知道 isWrongWay 的状态已改变，需要更新用户界面显示以反映这一点。

如果脚本执行到达这里，说明逆行状态值一定已经改变，因此脚本可以继续告诉 _uiManager 要显示什么：

```csharp
    if ( isWrongWay )
    {
        _uiManager.ShowWrongWay();
    }
    else
    {
        _uiManager.HideWrongWay();
    }

    oldIsWrongWay = isWrongWay;
}
```

在上面的代码中，处理完显示状态后，我们将 oldIsWrongWay 设置为 isWrongWay，以便跟踪状态变化。在 RaceGameManager 类的底部，是 Spawn() 函数：

```csharp
Transform Spawn(Transform spawnObject, Vector3 spawnPosition, Quaternion spawnRotation)
{
    return Instantiate(spawnObject, spawnPosition, spawnRotation);
}
```

我们之前稍微谈到过，像这样将 Spawn() 函数分离出来，可以很容易地将对 Instantiate() 的调用替换为性能更友好的方案，例如对象池管理器。这个函数所做的全部事情就是根据传入的参数向场景中添加一个 GameObject，然后返回对新 GameObject 的引用。

## 14.4.2 竞速控制——GlobalRaceManager 类

你可以在 GPC_Framework/Scripts/COMMON/GAME MANAGEMENT 文件夹中找到 GlobalRaceManager.cs。

GlobalRaceManager 依赖于每个玩家都附有 RacePlayerController 组件。RacePlayerController 组件在初始化时会向 GlobalRaceManager 注册自身。然后，我们的 GlobalRaceManager 类负责管理更宏观的层面，处理玩家位置的比较以计算比赛名次、计算已完成圈数并提供比赛状态。

GlobalRaceManager 存在于 GPC 命名空间中，并派生自 MonoBehaviour，因此它可以附加到 GameObject 上并访问 Unity 的一些内置函数：

```
namespace GPC
{
    public class GlobalRaceManager : MonoBehaviour
    {
        public int totalLaps;
        public bool raceAllDone;
        public int racersFinished;
        private int currentID;
        private Hashtable raceControllers;
        private Hashtable racePositions;
        private Hashtable raceLaps;
        private Hashtable raceFinished;
        private int numberOfRacers;
        private int myPos;
        private bool isAhead;
        private RaceController _tempRC;
        public static GlobalRaceManager instance;
    }
}
```

可以通过其静态变量 instance 访问此类。

```
public void Awake()
{
    if (instance != null)
        Destroy(instance);
    
    instance = this;
    
    // we set this to -1 so that the first returned id will be 0 (since it gets incremented on request)
    currentID = -1;
}
```

它的 Awake() 函数通过检查名为 instance 的静态变量是否为 null，确保任何时候只有一个脚本实例存在。如果 instance 为 null，我们就知道尚未创建此脚本的实例。如果 instance 不为 null，并且已经引用了一个现有组件，我们就在这里销毁它。

在上面的代码中，我们将 instance 设置为引用这个 GlobalRaceManager 实例。接下来，将变量 currentID 设置为 -1。

currentID 是一个整数，用于为游戏中的每个玩家生成唯一 ID。每当 RacePlayerController 请求一个 ID 号时，currentID 就会递增，以便玩家按照生成顺序拥有递增的 ID 号。随着数字递增
