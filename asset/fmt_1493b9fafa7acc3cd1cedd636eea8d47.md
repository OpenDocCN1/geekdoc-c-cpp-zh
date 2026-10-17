
```cs
    theRadarControlScript.AddEnemyBlipToList( aTransform);

}

public void RemoveEnemyFromRadar( Transform aTransform )

{

    theRadarControlScript.RemoveEnemyBlip( aTransform );

}

public Player_LBS GetMainPlayerScript ()

{

    return focusPlayerScript;

}

public Transform GetMainPlayerTransform()

{

    return playerGO1.transform;

}

public GameObject GetMainPlayerGO ()

{

    return playerGO1;

}

public void PlayerDied(int whichID)

{

    // 这是单人游戏，所以现在结束游戏
    // 两个玩家都死亡了，结束游戏
    UIControl.ShowGameOver();
    Invoke("Exit",5);

}

void Exit ()

{

    Application.LoadLevel( mainSceneName);

}

// UI 更新调用
// public void UpdateScoreP1( int aScore )

{

    UIControl.UpdateScoreP1( aScore);

}

public void UpdateLivesP1( int aScore )

{

    UIControl.UpdateLivesP1( aScore);

}
```

### 11.5.1 脚本详解

`Controller_LBS.cs` 继承自 `BaseGameController`，后者又继承自 `MonoBehaviour`，以便它可以接入 Unity 的某些内置函数调用，如 `Update()`、`Awake()` 和 `Start()`。

```cs
using UnityEngine;
using System.Collections;
public class Controller_LBS : BaseGameController
{
    public string mainSceneName = "menu";
    private int numberOfPlayers;
    private Vector3[] playerStarts;
    private Quaternion[] playerRotations;
    private GameObject playerGO1;
    private Player_LBS thePlayerScript;
    private Player_LBS focusPlayerScript;
    private BasePlayerManager mainPlayerDataManager;
    // 不是硬编码值，我们使用变量 
    // 来定义玩家数量
    void Init()
    {
        // 不是硬编码值，我们使用变量 
        // 来定义玩家数量
    }
}
```

添加到 Unity 编辑器 Inspector 面板列表中的第一个玩家对象必须是主玩家，在游戏术语中，我们称之为“1 号玩家”。当玩家生成时，`SpawnController` 将它们的对象存储在数组中，以便以后从其他脚本访问。数组的访问通过 `GetPlayerGO(index number)` 函数提供。在这里，我们调用 `SpawnController` 返回主玩家对象并存储在 `playerGO1`：

```
// grab a reference to player's gameObject for later
playerGO0 = SpawnController.Instance.GetPlayerGO( 0 );
```

`GetComponent()` 用于获取主玩家控制脚本的引用，存储在名为 `thePlayerScript` 的变量中：

```
// grab a reference to the focussed player's controller script, so
// that we can do things like access its speed variable
// thePlayerScript = ( Player_LBS ) playerGO1.GetComponent<Player_LBS>();
```

下一行为玩家分配一个 ID 号，稍后用于识别弹体的来源：

```
// assign this player the id of 0
thePlayerScript.SetID( 0 );
```

为了允许用户控制主玩家，调用了 `SetUserInput`。我们还在变量 `focusPlayerScript` 中保留了该玩家脚本的引用，因为当游戏控制器向 UI 提供数据以及相机需要对焦时，聚焦的是这个玩家：

```
// set player control
thePlayerScript.SetInput( true);
// as this is the user, we want to focus on this for UI etc.
focusPlayerScript = thePlayerScript;
```

脚本会寻找 `GameObject` 对象的引用以查看主玩家。如果存在，它将作为摄像机的目标。如果不存在，则将玩家设置为相机目标：

```
// if we have a camera target to look at
Transform aTarget=playerGO1.transform.FindChild("CamTarget");
if(aTarget==null)
```

```
// if we have a camera target to aim for, instead of
// the main player, we use that instead
Camera.main.SendMessage("SetTarget", aTarget);
} else {
// tell the camera script to target the player
Camera.main.SendMessage("SetTarget",
playerGO1.transform );
```

雷达系统需要知道以哪个对象为中心。通过快速调用 `SetCenterObject()` 函数，参数为玩家的 `transform`：

```
// finally, tell the radar about the new player
theRadarControlScript.SetCenterObject( playerGO01 );
}
```

`StartPlayer()` 函数由 `Start()` 调用，它将告诉玩家何时开始游戏。该函数还获取了玩家数据管理器的引用并将其存储在名为 `playerDataDataManager` 的变量中。这以后将被游戏控制器用于在 UI 中显示玩家得分等操作：

```
void StartPlayer()
    // grab a reference to the main player's data manager so we
    // can update its values later on (scoring, lives etc.)
    mainPlayerDataManager = 
        playerGO01.GetComponent<BasePlayerManager>().DataManager;
```

每个玩家脚本都包含一个 `GameStart()` 函数，用于完成启动游戏所需的所有工作：

```
// all ready to play, let's go!
thePlayerScript.GameStart();
```

`EnemyDestroyed()` 函数重写了 `BaseGameController.cs` 脚本中的原始形式。每当敌人被摧毁时，它就会被调用，用于制作爆炸效果、更新得分，并告诉波次生成器玩家距离完成该波次又近了一个敌人。它的参数是敌人受击时的位置、敌人分数以及它被击中的弹体 ID：

```
public override void EnemyDestroyed ( Vector3 aPosition,
    int pointsValue, int hitByID)
```

爆炸音是 Unity 编辑器中数组中的第二个项目，索引为 1：

```
// tell our sound controller to play explosion sound
BaseSoundController.Instance.PlayByIndex( 1, aPosition );
```

将得分添加到主玩家的数据管理器：

```
// tell main data manager to add score
mainPlayerDataManager.AddScore( pointsValue );
```

通过脚本中的 `UpdateScoreUI()` 函数更新 UI。为了获取玩家得分，数据管理器提供了 `GetScore()` 函数：

```
// update the score on the UI
UpdateScoreUI( mainPlayerDataManager.GetScore() );
```

```
// play explosion effect at enemy position
Explode ( aPosition );
```

波次生成器（在 `SpawnController` 中）跟踪有多少个敌人，以便它知道何时生成新敌人。每当敌人被摧毁时，游戏控制器需要调用其 `Fragged()` 函数：

```
// tell spawn controller that we're one enemy closer to
// next wave
SpawnController.Fragged();
```

`PlayerHit()` 函数通过 `BaseSoundController` 实例播放爆炸音，然后在玩家所在的位置产生爆炸。当玩家脚本与弹体碰撞时，会调用此函数：

```
public void PlayerHit(Transform whichPlayer)
{
    // tell our sound controller to play explosion sound
    BaseSoundController.Instance.PlayByIndex(2,
    whichPlayer.position);
    // call the explosion function!
    Explode(whichPlayer.position);
}
```
（注：提供的文本包含大量重复和 OCR 错误，已根据逻辑进行了清理，以提供连贯的文档。）

## 11.6 玩家控制器 (Player Controller)

Lazer Blast 使用了 Unity 自带的 Angry Bots 教程中的动画人物模型。它使用继承自第 5 章所示俯视角控制器脚本的类，并为其添加了自定义的游戏特定脚本，以及一个独立的类来处理角色模型的动画。

玩家类 `_LBS` 继承自控制器脚本 `BaseTopDown.cs*`，后者是 Unity 自带的第三称控制器脚本的修改版本，该脚本使用 Unity 内置的字符控制器来处理物理效果。`BaseTopDown.cs` 在第 5 章（构建玩家移动控制器）中有详细的介绍。

`Player_LBS.cs` 看起来如下：

```csharp
using UnityEngine;
using System.Collections;
public class Player_LBS : BaseTopDown
{
    private bool isInvulnerable;
    private bool isRespawning;
    public BasePlayerManager myPlayerManager;
    public BaseUserManager myDataManager;
    public bool godMode = false;
    public GameObject meshGO;
    public Standard.SlotWeaponController weaponControl;
    public bool canFire;
    public bool isFinished;
    public override void Init()
    {
        base.Init();
        // 如果需要，开启无敌模式
        if(godMode)
        {
            MakeVulnerable();
        } else {
            MakeInvulnerable();
        }
        // 初始不允许玩家控制
        canControl = false;
        // 获取武器控制器的引用
        weaponControl = myGO.GetComponent<Standard.SlotWeaponController>();
        // 如果在编辑器中没有设置玩家管理器，尝试获取
        if(myPlayerManager == null)
            myPlayerManager = myGO.GetComponent<BasePlayerManager>();
    }
}
```

```csharp
//为我们的玩家设置数据
myDataManager = myDataManager.DataManager;
myDataManager.SetName("Player");
myDataManager.SetHealth(3);
isFinished = false;
// 告诉游戏控制器更新生命 UI
GameController_LBS.Instance.UpdateLivesPl(myDataManager.GetHealth());
}
public override void GetInput()
{
    if(isFinished || isRespawning)
    {
        horz = 0;
        vert = 0;
        return;
    }
    // 如果我们不应该控制这个玩家，则退出
    if(!canControl)
        return;
}
// 从输入提供程序获取输入
horz = Mathf.Clamp(default_input.GetHorizontal(), -1, 1);
vert = Mathf.Clamp(default_input.GetVertical(), -1, 1);
// 如果需要则射击
if(default_input.GetFire() && canFire)
{
    // 告诉武器控制器处理射击
    weaponController.Fire();
}
public void GameStart()
{
    // 此函数由游戏控制器调用，告诉我们
    // 什么时候可以开始移动
    canControl = true;
}
void LostLife()
{
    isRespawning = true;
    // 让我们爆炸！
    GameController_LBS.Instance.PlayerHit(myTransform);
    // 减少一个生命值
    myDataManager.ReduceHealth(1);
    myController_LBS.Instance.UpdateLivesPl(myDataManager.GetHealth());
    if(myDataManager.GetHealth() < 1) // 游戏结束
    {
        // 停止移动，只要刚体不是
        // 运动学（否则它将没有速度，
        // 我们尝试设置它会产生错误消息）
        if (!PlayerController.rigidbody.isKinematic)
            PlayerController.rigidbody.velocity = Vector3.zero;
        // 隐藏船体
        theMeshGO.SetActive(false);
        // 禁用并隐藏武器
        weaponControl.DisableCurrentWeapon();
        // 执行游戏结束需要做的任何操作
        PlayerFinished();
    }
    else {
        // 隐藏船体
        theMeshGO.SetActive(false);
        // 禁用并隐藏武器
        weaponControl.DisableCurrentWeapon();
        // 重生
        Invoke("Respawn", 2f);
    }
}
void Respawn() 
{
    // 重置重生标记
    isRespawning = false;
```
