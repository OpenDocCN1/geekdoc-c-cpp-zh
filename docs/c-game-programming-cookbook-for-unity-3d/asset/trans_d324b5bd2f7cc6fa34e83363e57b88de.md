

```csharp
{
  Instantiate( powerUpPrefab, aPosition, Quaternion.identity);
  powerupExplosionCounter=0;
}
```

```csharp
public void Explode ( Vector3 aPosition )
{
  // 在传入此函数的的位置实例化
  // 一个爆炸效果
  Instantiate( explosionPrefab, aPosition, Quaternion.identity);
}
```

```csharp
public void PlayerHit(Transform whichPlayer)
{
  // 告诉我们的声音控制器播放爆炸音
  BaseSoundController.Instance.PlaySoundByIndex( 2,
  whichPlayer.position );

  // 调用爆炸函数！
  Explode(whichPlayer.position );
}
```

```csharp
public void UpdateScoreP1( int aScore )
{
  if ( UIControl != null )
  UIControl.UpdateScoreP1( aScore );
}
```

```csharp
public void UpdateLivesP1( int aScore )
{
  if ( UIControl != null )
  UIControl.UpdateLivesP1( aScore );
}
```

```csharp
public void UpdateScoreP2( int aScore )
{
  if ( UIControl != null )
  UIControl.UpdateScoreP2( aScore );
}
```

```csharp
public void UpdateLivesP2( int aScore )
{
  if ( UIControl != null )
  UIControl.UpdateLivesP2( aScore );
}
```

```csharp
private void StopPlayers()
{
  playerScript.GameFinished();
}
```

```csharp
private bool player1Dead;
private bool player2Dead;
```

```csharp
public void PlayerDied(int whichID)
{
    if (whichID==1)
        player1Dead=true;
    if (whichID==2)
        player2Dead=true;
    if(player1Dead && player2Dead && totalPlayers>1)
    {
        // 两个玩家都死了，所以结束游戏
        UIControl.ShowGameOver();
        Invoke("Exit",5);
    } else if(totalPlayers==1)
    {
        // 这是单人游戏，所以直接结束游戏
        // 现在玩家都死了，所以结束游戏
        UIControl.ShowGameOver();
        Invoke("Exit",5);
    }
}
```

```csharp
void Exit()
{
    SpawnController.Instance.Restart();
    Destroy(this.gameObject);

    // 确保我们有一个可以通信的场景管理器
    GetSceneManager().LoadLevel(mainSceneName);
}
```

## 14.3.2.1 脚本详解

`GameController_IP`get基于 `BaseGameController`：

```csharp
using UnityEngine;
using System.Collections;
```

```csharp
public class GameController_IP : BaseGameController
{}
```

当 `GameController_IP` 被实例化时，静态变量 `Instance` 会被赋予对此脚本的引用，以便从场景中的其他脚本访问它：

```csharp
public GameController_IP()
{
    Instance=this;
}
```

为了在场景之间保持游戏控制器存活，`Start()` 函数调用了 `DontDestroyOnLoad()`：

```csharp
public void Start()
{
    // 我们希望让游戏控制器贯穿
    // 整个游戏，所以我们使用 DontDestroyOnLoad 来保持它存活
    DontDestroyOnLoad(this.gameObject);
}
```

当加载新场景时，`LevelSetup.cs` 的实例会调用 `LevelLoadingComplete()` 函数。此处的脚本可以重新初始化自己和用户界面，以便游戏可以在新场景中继续：

```csharp
public void LevelLoadingComplete()
{
    Init();
    UIControl.Init();
}
```

`Init()` 函数的构造方式使其是可复用的，并在每个关卡的开始时被调用：

```csharp
public void Init()
{
```

玩家开始时处于固定位置。对 `StartPlayer` 的 `Invoke` 调用将安排在函数被调用 4 秒后释放玩家：

```csharp
// 告诉玩家它可以在 4 秒后移动
Invoke("StartPlayer",4);
```

`Time.timeScale` 值会影响整个游戏手感。某些射击游戏需要更多的敌人和更慢的移动速度，而有些游戏则移动速度更快且敌人更少；游戏的移动和更新取决于你正在构建的游戏类型（包括艺术风格、世界类型以及任何其他游戏元素）。可以通过设置 `GameSpeed` 变量来更改时间比例，代码将物理引擎设置改为：

```csharp
// 以防我们需要更改时间比例，它会运行这里
Time.timeScale=gameSpeed;
```

此游戏允许一个或两个玩家进行。主菜单显示了一个用于合作游戏的额外按钮。通过此额外按钮启动游戏，一个偏好键会被写入 `totalPrefs`。然后以相同的方式加载第一个主场景。玩家开始时被固定。在 `Init()` 的此阶段，获取了 `totalPrefs` 的值（整数 `totalPlayers`），并用它来设置不同的游戏：

```csharp
// 将当前游戏的玩家数量存储在 totalPrefs 中
// 并带入游戏的每个关卡。
if(PlayerPrefs.HasKey("totalPlayers")) // 这个偏好项是否存在？
{
    totalPlayers=PlayerPrefs.GetInt("totalPlayers"); // 然后使用该值
} else {
    totalPlayers=1; // 默认为单人
```

此处的生成逻辑与其他游戏相同，尽管它没有使用起始位置数组，而是只使用单个 `transform` 作为生成位置。Unity 的 `GameObject.Find()` 函数被用于查找 `Player_Object`。它的 `transform` 信息将在所有关卡中作为起点使用：

```csharp
// 查找玩家 transform
playerParent= GameObject.Find("Player_Object").transform;
```

```csharp
Vector3[] playerStarts=new Vector3[totalPlayers];
Quaternion[] playerations=new Quaternion[totalPlayers];
```

在所有其他游戏中，使用 `SpawnControllerSetUpPlayers()` 函数将玩家实例化到游戏中。它需要一个位置数组和一个旋转数组，这些数组是在这里创建的。此游戏只有一个起始点和一个像其他游戏可能拥有的点位数组，但为了保持全书的一致性，它使用了相同的系统。当然，如果你是想要获取此游戏并添加更多玩家的读者，那么无疑将会有：

```csharp
for(int i=0; i<totalPlayers; i++)
{
    tempQuat=Quaternion.identity;

    if(i==0)
    {
        // 玩家 1 的位置
        tempVec3= new Vector3(-5, 0, 0);
    }
    else
    {
        // 玩家 2 的位置
        tempVec3= new Vector3(-5 + i*5, 0, 0);
    }
    playerStarts[i]=tempVec3;
    playerations[i]=tempQuat;
}
```

玩家只在 `didInit` 仍为 `false` 时才生成。为了避免场景中的混乱，我们确保只生成一次：

```csharp
// 如果我们还没有设置好玩家，didInit
// 将仍为 false
(didInit)
```

```csharp
SpawnController.Instance.SetUpPlayers(playerStarts,
playerations, playerParent, totalPlayers);
```

变量 `playerGO1` 持有的引用将在后续使用。`SpawnController` 根据传入的索引返回一个 `GameObject`：

```csharp
// 获取玩家的游戏对象供以后使用
playerGO1= SpawnController.Instance.GetPlayer(0);
```

## 14.3 Prefabs

当从主菜单选择合作游戏且 `totalPlayers` 大于 1 时，`playerGO2` 将持有玩家的引用：

```csharp
// 如果是双人游戏，也获取那个// 玩家的游戏对象
if(totalPlayers>1)
    playerGO2=SpawnController.Instance.GetPlayer(1);
```

当关卡开始时，会实例化一个游戏控制器制体。在游戏控制器制体的子对象中有多个对象，其中一个名为 `GameCamera` 的相机。在游戏控制器制体添加到场景之前，游戏关卡没有相机。当 `Init()` 函数在游戏控制器脚本上运行时，它获取相机的引用并将其放置在开始关卡的正确位置。`CameraTransform` 用于持有引用：

```csharp
// 查找游戏相机
CameraTransform = GameObject.Find("GameCamera").transform;
```

```csharp
// 将相机放在指定的位置
//（在 Unity 编辑器窗口的此
// 组件上设置）
tempVec3 = CameraTransform.localPosition;
tempVec3.z = CameraStartPositionZ;
CameraTransform.localPosition = tempVec3;
```

`cameracontrol` 持有脚本的引用：

```csharp
// 如果没有通过编辑器设置相机脚本对象，尝试查找一个
cameracontrol=
CameraTransform.GetComponent<BaseCameraControl>();
```

作为一款俯视卷射游戏，关卡的滚动是持续的，直到被停止。`isStopped` 布尔变量将在玩家到达 Boss 战时停止滚动：

```csharp
isStopped=false;
```

为了能够更改游戏场景，此脚本需要场景管理器的引用。它在 `GetSceneManager()` 函数中查找场景管理器：

```csharp
// 确保我们有一个可以通信的场景管理器
GetSceneManager();
didInit=true;
```

