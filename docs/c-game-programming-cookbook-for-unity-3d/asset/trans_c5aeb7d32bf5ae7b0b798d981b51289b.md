

正如本节提到的，`TellGCEnemyDestroyed()` 函数（以及 `TellGCBossDestroyed()` 函数）设计用于在使用新的游戏控制器时进行重写。这些函数会调用其对象的 `EnemyDestroyed()` 或 `BossDestroyed()`。

`GameController_IP.EnemyDestroyed()` 取三个参数：被摧毁的敌人、玩家击中它应获得的分数，最后玩家可能识别出的弹药所有者 ID。如果没有该 ID，游戏控制器将不知道给哪个玩家分配分数：

```java
public virtual void TellGCEnemyDestroyed()
```

```java
GameController_IP.Instance.EnemyDestroyed(myTransform.position,
pointsValue, tempINT);
```

```java
public virtual void TellGCBossDestroyed()
```

```java
GameController_IP.Instance.BossDestroyed();
```

# 14.3.5 途点跟随者 (Waypoint Follower)

敌方飞船沿着途点路径移动，向屏幕底部的玩家发射。`BaseEnemy` 脚本控制发射，而 AI 控制器通过其 `translate_along_waypoint_path` 状态处理路径跟随。为了让 AI 控制器执行此操作，它需要知道使用哪个途点控制器，并拥有其 `AIState`（其默认状态是巡逻而非跟随途点），而 `BasepointFollower.cs` 脚本正此此目的。

`BaseWaypointFollower.cs` 脚本：

```csharp
// 使用 AIController 的 translate_along_waypoint_path 函数
// 沿路径跟随
```

```csharp
public class BaseWaypointFollower : ExtendedCustomMonoBehavior
{
    public BaseAIController AIController;

    public virtual void Start () {
        if(didInit)
            Init (
    }

    public virtual void Init () {
        // 缓存我们的 transform
        myTransform= transform;

        // 缓存我们的 gameObject
        myGO= gameObject;

        // 缓存对 AI 控制器的引用
        AIController= myGO.GetComponent<BaseAIController>();
    }
}
```

```csharp
if (AIController==null)
    AIController= myGO.AddComponent<BaseAIController>();
```

```csharp
// 运行我们基类中的 Init 函数
// (BaseAIController.cs)
AIController.Init();
```

```csharp
// 告诉 AI 我们想要控制这个对象
AIController.SetAIControl(true);
```

```csharp
// 告诉我们的 AI 跟随途点
AIController.SetAIState(AIStates.AIState.translate_along_waypoint_path);
```

```csharp
// 设置标记告诉我们 init 已经发生
didInit=true;
```

```csharp
public virtual void SetWaypointController(Waypoints _aWaypointPoint)
{
    if (AIController==null)
        Init();

    // 将此传递给我们的途点控制器，以便它可以
    // 跟随途点
AIController.SetWaypointController(aWaypointPoint);
}
```

# 14.3.5.1 脚本解析

`BaseWaypointFollower` 类派自 `ExtendedCustomMonoBehavior`，该后者添加了一些额外功能和自定义变量：

```csharp
public class BaseWaypointFollower : ExtendedCustomMonoBehavior
{
```

与书中的大多数脚本一样，`Start()` 调用了 `Init()`：

```csharp
    public virtual void Start()
    {
        if(!didInit)
            Init();
    }
```

`Init()` 创建了对 `transform` 和 `gameObjects` 的引用，并设置了变量 `AIController`（通过 `GameObject.GetComponent<T>` 查找 `BaseAIController`）：

```csharp
    public virtual void Init()
    {
        // 缓存我们的 transform
        myTransform= transform;

        // 缓存我们的 gameObject
        myGO= gameObject;

        // 缓存对 AI 控制器的引用
        AIController= myGO.GetComponent<BaseAIController>();
    }
```

在这个游戏中，有一些属性需要通过 Unity 窗口设置，敌人 prefab 上总是会挂载 `AIController` 组件，但在对象上未挂载 `AIController` 的情况下，该脚本使用 `GameObject.AddComponent()` 创建。这主要是为了让脚本可以在其他游戏中复用：

```csharp
if (AIController==null)
    myGO.AddComponent<BaseAIController>();
```

`AIController` 需要初始化：

```csharp
// 运行我们基类中的 Init 函数
// (BaseController.cs)
AIController.Init();
```

`AIController.SetAIControl()` 告诉 AI 控制器它可以控制这个敌人。它的 `SetState()` 函数会被调用，将状态设置为 `translate_along_waypoint_path`（参见本书第 9 章关于 `AIStates` 和 `BaseAIController.cs` 的完整解析）：

```csharp
// 告诉 AI 控制器我们要控制这个对象
AIController.SetAIControl(true);
```

```csharp
// 告诉我们的 AI 跟随途点
AIController.SetAIState(AIStates.AIState.translate_along_waypoint_path);
```

```csharp
// 设置标记告诉我们它已经发生
didInit=true;
```

`SetWaypointController()` 由游戏控制器调用以告诉此脚本 `Waypoints_Controller` 实例。一旦该函数执行，就会调用 `AIController.SetWaypointController()` 传递引用：

```csharp
public void SetWaypointController(Waypoints_Controller waypointControl)
{
    if (AIController==null)
        Init();

    // 将此传递给我们的途点控制器，以便它可以
    // 跟随途点
AIController.SetWaypointController(waypointControl);
}
```

# 结语

本书到此结束，但我希望这只是你如何使用书中内容的开始。这里有大量的代码，至少应该是任何类型游戏的良好起点。我鼓励你使用代码，使用资源——创造你的游戏。

记住，本书只提供做某事的方法。在制作游戏十多年后，我仍然将每一个新游戏看作是充满新课程和待解决问题的冒险。程序员不断演进；以跟上最新的技术、硬件或趋势，并为开发者寻找更好的方法。工程知识可以带你路，但道路并不总是如你预期的那样。找到适合你的方法并享受制作游戏的旅程。感谢阅读本书，并选择做一些精彩创作的事。完成后，请通过 Twitter 或网站给我发消息。

祝好，
Jeff

# 索引

页码后跟 f 表示图表。

## A
- AddEnemyToList(), 248
- AddEnemyToRadar(), 248
- AddExplosionForce(), 340
- AddRaceController(), 329, 321
- AttackStates.cs 脚本, 206–214, 210–214
- AIStates.cs 脚本, 171
- Angry, 250
- Animations, 104–105. *另见 Humanoid character*
- Animation.CrossFade(), 104, 组件, 97–198
- Apple Store, 215–216
- ArrayList(), 245
- 人工智能 (AI) 计数器，管理器, 169–214
- 添加武器控制到, 206–214
- AIStates.cs 脚本, 171
- BaseAIController.cs 脚本, 169–171, 172–206, 238, 259, 185–206, 206–214, 238, 259, 260, 331
- 基类 (Base class), 7
- BASE 核心框架, 1–27
- BaseGameController 脚本, 12–16, 238, 239, 275, 282, 349, 401, 14–16
- BaseInputController 脚本, 22–27, 26–27, 玩家结构和, 32–33, 34
- BasePlayerManager 脚本, 22–24, 98, 110, 238, 23–24
- Camera_Third_Person.cs, 69–74, 69–74
- CancelInvoke(function), 64, 264
- CanSee(function), 198, 201, 388
- CarController_MVD.cs 脚本, 283, 318–344
- CarController_TB 脚本, 373–383, 382–383
- CharacterState 动画状态, 105
- Check_If_Cs_Is_Follow(function), 333, 343
- Check(function), 34–35, 77
- CheckLock(function), 112, 113–114, 334
- CheckWrongWay(function), 304, 305
- 碰撞体 (Colliders), 109, 142, 236, 238, 239, 266, 271, 305–306, 338, 339, 409, 414, 425, 轮, 85–109
- 碰撞标记 (Collision_Flags), 102
- COMMON 文件夹, 41
- CompletedCompletedLap(function), 306, 313
- ConfirmExitGame(function), 227
- ContinueForward(function), 406
- 控制器 (Controller) AI. 另见 人工智能 (AI)，管理器, 361–364, 游戏. 游戏控制器, 在游戏框架内, 1, 移动. 玩家移动控制器，玩家, 250–259, 游戏特定的, 29, 31–32, 移动. 比赛, 291–306, 297–306, 脚本, 2–3, 简单生成. 查看 生成控制器，声音, 158–163
- 核心游戏框架 (Core game framework). 另见 游戏框架
- 创建者 (Creators), 53–54
- BaseSoundController 脚本, 158–163, 237, 248, 348, 407, 409, 160–163
- BaseTopown sc, 96–238, 250, 253, 96–105
- BaseIDataManager 脚本, 231–232, 267
- BaseUserManager sc, 脚本 20–22, 22, 玩家结构和, 37–38, 39
- Vehicle.cs 脚本, 106–114, 332, 109–114
- BaseWaypointFollower.cs 脚本, 426–428, 427–428
- BaseWeaponController.cs, 122–134, 127–134
- BaseWeaponScript.cs 脚本, 121, 128, 133, 134–142, 266, 138–142

