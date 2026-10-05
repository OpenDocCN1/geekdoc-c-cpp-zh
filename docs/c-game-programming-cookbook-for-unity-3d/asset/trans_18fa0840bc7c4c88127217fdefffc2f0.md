

## 2 构建核心游戏框架

在本章中，我们将查看基础项目的结构，我们将向该项目添加所有的游戏脚本组件，并探讨其背后的设计思路。本章将为核心框架中做出的设计决策提供背景，并为理解各个代码配方如何协同工作，以及它们为何有时会依赖其他组件提供良好的基础。

本书的框架（如图 2.1 所示）包含六个主要区域：

- 1. 游戏控制器 (Game Controller)
游戏控制器充充当游戏中所有不同部分之间的中央通信脚本。在某种程度上，它是将组成游戏的各种组件结合在一起的主要“胶水”。

- 2. 场景管理器 (Scene Manager)
该脚本处理场景的加载和保存。场景是 Unity 对关卡文件的称呼。

- 3. UI 管理 (UI Manager)
UI 管理器绘制所有的游戏内主要用户界面元素，例如分数显示和生命值。

- 4. 音效管理器 (Sound Manager)
音效管理器处理音频播放。管理器持有一个包含可能播放声音的 `AudioClips` 数组。当游戏开始时，

![](img/041dca164b58875f4f1a64abb3328f5c_31_0.png)

图 2.1 游戏框架图。

音效管理器为数组中的每个声音创建一个独立的 `AudioSource`。当我们需要播放声音时，会将引用声音在数组中位置的索引号传递给管理器。它使用自己独立的 `AudioSource` 来播放源，这有助于缓解从单个源播放过多音频文件可能引起的问题。

- 5. 玩家 (Players)
玩家可能已经存在于游戏场景中，也可能由游戏控制器实例化。玩家具有较为复杂的结构，将在第 3 章中进行探讨。

- 6. AI 与敌人 (AI and Enemies)
与玩家一样，AI 控制的字符或敌人可能在加载时已经存在于场景中，或者由游戏控制器或其他脚本在运行时创建。

尽管你可能选择使用自己的框架，但理解组件之间如何协同工作以及它们如何结合是非常重要的。为了最大限度地提高灵活性，基类需要能够适应各种不同的配置。例如，玩家控制脚本应该允许从另一个脚本传递输入，以便可以轻松切换控制系统。主玩家脚本不需要知道输入来自哪里，但它需要为输入脚本提供一个通信的通用接口。输入脚本可以从键盘、鼠标、人工智能、网络输入等获取输入，只要使用通用接口与玩家控制器通信；对于玩家控制器来说，输入实际上来自哪里并不重要。

## 2.1 控制器与管理器 (Controllers and Managers)

通过将任务专门化给特定的管理器，可以在不影响核心功能的情况下更换组件，这反过来使得很容易将相同的代码从一个游戏带到另一个游戏而无需重写；从第一人称射击游戏到赛车游戏，相同的代码可以存储用户会话数据、加载关卡或控制武器。在本书中，我使用术语来指定类的类型：控制器 (controllers) 和管理器 (managers)。

### 2.1.1 控制器 (Controllers)

控制器专门负责特定任务，例如帮助脚本之间相互通信、持有特定游戏的玩家信息，或处理会话数据。例如，本书中所有示例游戏的中心都是游戏控制器脚本，它作为游戏脚本的中央位置。每个游戏都有自己的控制器脚本，充当那些本没有内置通信方法的不同组件之间的“胶水”。

### 2.1.2 管理器 (Managers)

管理器在书中用于代表专门管理对象或数据的脚本（以处理玩家、音频或其他游戏元素，类似于管理器可能管理公司员工的方式）。例如，`GlobalBattleManager.cs` 脚本被 `RaceController.cs` 实例使用，用于在示例游戏《坦克大战》(Tank Battle) 中跟踪死亡战战斗。管理器脚本负责计算玩家在得分板上的位置，并通知玩家游戏当前的运行状态。

## 2.2 构建核心框架脚本

`Scripts/BASE` 文件夹中有几个脚本，旨在作为你自己的版本的模板，或者作为你自己的游戏中可以从中派生出的类。在本节中，我们将查看构成主框架的脚本。
`BASE` 文件夹中在本章将涵盖的核心框架脚本如下：

- 2.2.1 `BaseGameController.cs`
- 2.2.2 `SceneManager.cs`
- 2.2.3 `ExtendedCustomMonoBehavior.cs`
- 2.2.4 `BaseUserManager.cs`
- 2.2.5 `BasePlayerManager.cs`
- 2.2.6 `BaseInputController.cs`

示例游戏 `BASE` 文件夹中的脚本比上述脚本多；那些落在基础核心框架之外的脚本将在书中逐案处理，例如在第 9 章中处理的 AI 脚本（那里我们将完整介绍 AI 系统），或者在第 8 章中探索的音频。

### 2.2.1 `BaseGameController.cs`

游戏控制器充当活动枢纽，以及那些无法直接连接的脚本无法向对方发送消息的地方。通过通过游戏控制器路由脚本，它们保持了独立性，改变它们的行为是一个简单的更改处理消息方式的过程，而不是跨多个脚本进行更改。

游戏控制器的核心功能如下：

- 1. 跟踪游戏状态
    a. 存储游戏状态
    b. 提供更改游戏状态函数
    c. 根据 `EndGame()`、`StartGame()` 或 `PauseGame()` 调用更改游戏状态
- 2. 创建玩家对象
- 3. 设置相机（例如跟随哪个玩家等）
- 4. 处理会话管理器、用户管理器和游戏之间的通信
- 5. 处理所有保持独立且不直接通信的脚本

游戏控制器是定义整体玩法以及持有当前游戏状态的地方。典型的游戏可能有几种不同的核心状态，例如：

1. 运行中 (running)
2. 暂停 (paused)
3. 加载中 (loading)
4. 已结束 (ended)

可能还有适用于特定游戏类型的自定义状态，例如用于显示过场动画或播放特殊音频。建议为任何影响一个或多个脚本的游戏动作创建一个新状态。这样你始终可以让脚本依赖游戏控制器来知道如何运行。

位于 `Scripts/BASE` 的基础游戏控制器脚本所示：

```csharp
public class BaseGameController : MonoBehaviour
{
    bool paused;
    public GameObject explosionPrefab;

    public virtual void PlayerLostLife()
    {
        // 处理玩家失去生命（更新 U.I. 等）
    }

    public virtual void SpawnPlayer()
    {
        // 需要生成玩家
    }

    public virtual void Respawn()
    {
        // 玩家正在重生
    }
    public virtual void StartGame()
    {
        // 执行开始游戏函数
    }

    public void Explode ( Vector3 aPosition )
    {
        // 在传入此函数的位置实例化爆炸效果
        Instantiate( explosionPrefab,aPosition, Quaternion.identity );
    }

    public virtual void EnemyDestroyed( Vector3 aPosition, int pointsValue, int hitByID)
    {
        // 处理敌人被毁
    }

    public virtual void BossDestroyed()
    {
        // 处理 Boss 战斗结束
    }

    public virtual void RestartGameButtonPressed()
    {
        // 处理重置按钮（默认行为是重新加载当前加载的场景）
        Application.LoadLevel(Application.loadedLevelName);
    }

    public bool Paused
    {
    }
}
```