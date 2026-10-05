

```csharp
get {
  // 获取暂停状态
  return paused;
}set {
  // 设置暂停状态
  paused = value;
  if (paused) {
    // 暂停时间
    Time.timeScale= 0f;
  } else {
    // 解除Unity暂停
    Time.timeScale = 1f;
  }
}
```

## 2.2.1.1 脚本解析

BaseGameController.cs 中的许多关键函数都是 `virtual`（虚拟的），包含这些函数是为了作为处理不同类型游戏活动的既定协议。也就是说，它们在这个特定的文件中不包含代码，但意图是让你以后在自己的派生游戏控制器版本中对它们进行重写。

`BaseGameController` 类继承自 `MonoBehaviour`，这样它就可以接入自动调用的系统函数，如 `Awake()`、`Start()`、`Update()` 和 `FixedUpdate()`：

```csharp
public class BaseGameController : MonoBehaviour
{
```

这些函数在这里作为占位符。其意图是用于实际游戏项目的游戏控制器脚本将继承自此类，并用功能填充这些接口函数：

```csharp
bool paused;
public GameObject explosionPrefab;
```

```csharp
public virtual void PlayerLostLife()
{
  // 处理玩家生命值丢失（更新用户界面等）
}
```

```csharp
public virtual void SpawnPlayer()
{
  // 需要生成玩家
}
```

```csharp
public virtual void Respawn()
{
  // 玩家正在重生
}
public virtual void StartGame()
{
  // 执行开始开始的函数
}
```

`BaseGameController` 中的其他函数是你在许多不同的游戏中都会使用的，将它们全部包含在像这样的脚本中（你可以从该脚本派生所有游戏控制器）可能会节省时间。这避免了在多个项目之间反复编写相同的代码。其中一个例子是 `Explode()` 函数，它仅仅执行了该操作：

```csharp
public void Explode ( Vector3 aPosition)
{
  // 在传入此函数的位置实例化
  // 爆炸效果
  Instantiate(explosionPrefab,aPosition,Quaternion.identity);
}
```

`Explode()` 所做的只是在函数调用者传递的位置实例化一个 `GameObject`。后续版本的游戏控制器脚本将使用单独的生成管理器（spawn manager）来处理实例化，尽管在现阶段，尽可能通用且不依赖于任何其他脚本是恰当的。

在 `Explode` 之后，我们又看到了两个空函数，用于告诉控制器何时普通敌人被销毁以及何时 Boss 被销毁：

```csharp
public virtual void EnemyDestroyed ( Vector3 aPosition, int pointsValue, int hitByID)
{
  // 处理敌人被销毁
}
```

```csharp
public virtual void BossDestroyed()
{
  // 处理 Boss 战斗结束
}
```

所有游戏都需要一些函数，例如重启按钮和暂停函数。以最简单的形式来说：

```csharp
public virtual void RestartGameButtonPressed()
{
  // 处理重启按钮（默认行为重新加载当前
  // 加载的场景）
  Application.LoadLevel(Application.loadedLevel);
}
```

`RestartGameButtonPressed` 使用 Unity 的 `Application.LoadLevel` 函数来重新加载当前场景。`Application.loadedLevel` 返回一个字符串，指向游戏当前内存中加载的场景名称。你也可以通过 `Application.name` 获取一个指向场景的索引。此索引编号与 Build Settings（File -> Build Settings）中的场景组织方式相关，这意味着如果你以后选择使用索引号来引用特定场景，那么构建设置中的更改可能会影响你游戏的运行方式。为了避免混淆，我倾向于在处理关加载时始终使用名称。

`BaseGameController` 的最后部分处理游戏暂停和取消暂停的机制：

```csharp
public bool Paused {
    get {
        // 获取暂停状态
        return paused;
    }
    set {
        // 设置暂停状态
        paused = value;
        if (paused) {
            // 暂停时间
            Time.timeScale = 0f;
        } else {
            // 解除Unity暂停
            Time.timeScale = 1f;
        }
    }
}
```

名为 `paused` 的布尔变量在内部持有游戏暂停状态。与其提供直接访问，不如使用 getter-setter（访问器属性）函数，这样我们可以在暂停状态改变时采取行动，而无需对其进行监控。

`Get` 部分只是返回该布尔变量。
`Set` 部分设置该布尔变量，并将 `Time.timeScale` 设置为 0（暂停）或 1（取消暂停）。设置 `Time.timeScale` 会影响时间的流逝。例如，将 `timescale` 设置为 0.5 意味着时间比真实时间慢 2 倍。Unity 文档规定：

除了 realtimeStartup 外，timescale 会影响 `Time` 类中所有的时间和增量时间测量。

如果你降低了 timescale，建议按相同幅度降低 `Time.fixedDeltaTime`。
当 `timescale` 被设为 0 时，`FixedUpdate` 函数将不会被调用。

普通的视频游戏会在游戏暂停时显示某种消息告诉玩家，但此脚本仅提供暂停机制，我们将在第 14 章之前不会过多考虑用户界面。

## 2.2.2 场景管理器

管理器控制物理场景之间的游戏流程。菜单界面上的按钮不直接加载场景；而是由下方的场景管理器脚本来加载它们：

```csharp
public class SceneManager : MonoBehaviour
{
    public string[] levelNames;
    public int gameLevelNum;

    public void Start ()
    {
        // 保持此对象存活
        DontDestroyOnLoad(this.gameObject);
    }

    public void LoadLevel(string sceneName)
    {
        // 加载场景
        Application.LoadLevel(sceneName);
    }

    public void GoNextLevel()
    {
        // 如果我们的索引超过了数组中关卡的总数，
        // 我们重置它
        if(gameLevelNum >= levelNames.Length)
            gameLevelNum = 0;
    }

    private void LoadLevel( int indexNum)
    {
        // 通过索引号加载场景
        Application.LoadLevel(levelNames[indexNum]);
    }

    public void resetGame()
    {
        // 重置关卡计数器
        gameLevelNum = 0;
    }
}
```

