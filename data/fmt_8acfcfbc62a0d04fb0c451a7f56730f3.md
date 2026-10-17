
音频选项菜单与我们在本章为止看到的那些有所不同，因为它调用了两个水平滑块来设置音效和音乐音量：

```cs
case 3:
// 音频选项
GUI.BeginGroup(new Rect (default_width / 2 - 150, default_height / 2 - 250, 500, 500));
GUI.Label(new Rect(0, 50, 300, 50), "AUDIO OPTIONS", "textarea");
GUI.Label(new Rect(0, 170, 300, 20), "SFX volume:");
```

在设置好 GUI 并渲染两个标签后，我们移动到渲染水平滑块的代码，如下所示：

```cs
audioSFXSliderValue = GUI.HorizontalSlider(new Rect (0, 200, 300, 50 ), audioSFXSliderValue, 0.0f, 1f);
```

在这里，我们使用 `audioSFXSliderValue` 变量（`float` 类型）来返回 `GUI.HorizontalSlider` 返回的值。一个滑块可以接受最多五个参数，如下：

- 1. 定义区域的 `Rect`。
- 2. `GUI.HorizontalSlider` 返回的值所在的 `audioSFXSliderValue` 变量。
- 3. `variableMenu` 设置为 1 时，我们的 `OnGUI` 函数包含了渲染简单选项菜单的代码。
- 4. 这里的 `totalPlayers` 键值。
- 5. 滑块可以接受的五个参数。

```csharp
public int player_highscore;
public string gamePrefsName= "DefaultGame"; // 切记忘记设置
// 在编辑器中设置这个！！
public void UpdateScorePl( int aScore ) {
    player_score=aScore;
    if( player_score>player_highscore ) {
        player_highscore = player_score;
    }
}
public void UpdateLivesPl( int alifeNum ) {
    player_lives = alifeNum;
}
public void UpdateScore( int aScore ) {
    player_score = aScore;
}
public void UpdateLives( int alifeNum ) {
    player_lives = alifeNum;
}
public void LoadHighScore() {
    // 从偏好设置中获取高分
    if( PlayerPrefs.HasKey( gamePrefsName+"_highScore" ) {
        player_highscore = PlayerPrefs.GetInt(
            gamePrefsName+"_highScore"
        );
    }
}
public void SaveHighScore() {
    // 既然我们知道游戏结束了，让我们也保存高分
    PlayerPrefs.SetInt( gamePrefsName+"_highScore", player_highscore );
}
```

关于使用此系统的游戏内用户界面脚本示例，请查看下一章或任何其他示例游戏以获取完整拆解。

# 11 章节：激光射击生存 (Lazer Blast Survival)

20世纪70年代后期，出现了一款由伯利软件发行版（BSD）出品的名为 *Robots* 的回合游戏。在 *Robots* 中，玩家必须逃避一群敌人，这些敌人每回合都会向玩家靠近。在游戏的原始版本中，玩家在竞技场内移动，试图避免与敌人接触，接触会导致游戏结束。

*Robots* 通常被认为是竞技场射击游戏（arena shooter）的开端——这个术语用于描述一种俯视视角、动作被锁定在类似竞技场的有限区域内的射击游戏。*Robots* 的概念有许多衍生版本，但在封闭区域内逃避敌群的总体思想保持不变，并且非常适合当时当时的低配置计算机。很快，它演变成速度更快速——而且是实时的游戏是不可避免的。1980年，Stern 向世界引入了 *Berserk*。

*Berserk* 最初是一款街机游戏，但迅速移动到 Atari 2600、5200 和 Vectrex 等家用主机上。从本质上说这是 *Robots* 演变为实时街机射击游戏。在这个版本中，玩家在随机生成的迷宫中穿行并击杀敌人。每个屏幕包含若干敌人，当玩家移动到屏幕边缘进入迷宫的下一部分时，敌人可以被摧毁或被留在。Berserk 最出色且令人记忆深刻的特征之一是街机上的语音合成系统，它让机器人能够说话。各地的街机厅回荡着随机的机器人短语，像我这样的孩子会用最棒的机器人声音说“抓住那个类人”、“入侵者绝不能逃脱”以及“像机器人一样飞翔！”

## 11.2 主游戏场景

游戏并没有为每一波攻击加载不同的场景，而是通过不断在同一个场景中实例化敌人的预制体（prefabs），直到玩家没有剩余生命为止。

主菜单由单个 `gameObject` 组成，主菜单脚本在第 10 章。

主游戏场景的层级（Hierarchy）结构如下：

- ARENA（竞技场）
  - （构成环境的模型）
- Arena_Colliders（竞技场碰撞体）
  - （关卡的碰撞体）
- Directional light（平行光）
- GameController（游戏控制器）
- Main Camera（主摄像机）
- MusicController（音乐控制器）
- Player_Startpoint（玩家起始点）
- SoundController（声音控制器）
- SpawnController（生成控制器）
- UI（界面）
  - Game Over Graphic（游戏结束图形）
  - Get Ready Graphic（准备好了图形）

注意，游戏控制器在游戏开始时动态创建玩家和敌人。Unity 窗口设置了多个预制体和 `gameObject` 的引用：

- 游戏控制器预制体
- 爆炸预制体（爆炸的粒子效果）
- `Player Prefab List` 数组，包含对 `Top_Down_Player` 预制体的引用
- `StartPoints` 数组，包含对场景中 `Player_Startpoint` `gameObject` 的引用

- 雷达控制脚本（雷达控制脚本）包含对 `Main Camera` 的引用（其绑定了 `RadarGUI.cs` 组件实例）

- 挂载在 `Sound Controller` `gameObject` 上的 `BaseSoundController.cs` 脚本有一个名为 `Game Sounds` 的数组，包含引用：
  - `shoot`（射）
  - `explode2`（爆炸2）
  - `player_explode`（玩家爆炸）
  - `powerup`（强化）
  - `spawner 1`（生成器1）

- `Spawn Controller` `gameObject` 挂载了 `WaveSpawner.cs` 实例，其 `Spawn Object Prefabs` 数组中包含以下引用：
  - `Spawn_Structure1`
  - `Spawn_Structure2`
  - `Spawn_Structure3`

- `UI` `gameObject` 挂载了名为 `UI_LBS.cs` 的脚本。它引用：
  - `GAMEOVER_GRAPHIC` `gameObject`
  - `GETREADY_GRAPHIC` `gameObject`

## 11.3 预制体 (Prefabs)

构成游戏的预制体有：

ENEMIES（敌人）
`EnemyBot`

ENEMY WAVES（敌波）
`Spawn_Structure 1`
`Spawn_Structure 2`
`Spawn_Structure 3`

PLAYERS（玩家）
`Top_down_player`
`Top_down_player_ALT`

PROJECTLES（弹药）
`Blast`
`Blast2`

WEAPONS（武器）
`Blaster`
`Blaster_1`

EXPLOSION PREFAB（爆炸预制体 - 不特定于此）

本章剩余部分将介绍预制体和 `gameObject`；本节将不再涵盖已详细介绍的组件。

## 11.4 核心材料

Lazer Blast 使用了：

1. `Game Controller`（游戏控制器）。见第 10 章。
2. `Player`（玩家）。见第 10 章。
3. `Enemies`（敌人）。见第 9 章。
4. `Wave spawning`（生成）。见第 9 章。
5. `Projectiles`（弹药）。见第 5 章。
6. `User Interface`（用户界面）。见第 10 章。
7. `Top Down Camera`（俯视摄像机）。
8. `Sound Controller`（声音控制器）。见第 8 章。
9. `Music Controller`（音乐控制器）。

## 11.5 游戏控制器 (Game Controller)

游戏控制器是游戏的中央枢纽。它继承自 `BaseController`，重写了一些基类函数并添加了自己的函数。

完整的 `GameController_LBS.cs` 脚本如下：

```csharp
using UnityEngine;
using System.Collections;
public class GameController_LBS : BaseController
{
    public mainMenuName = "menu_LBS";
    public GameObject[] playerPrefabList;
    public Wave_Spawner WaveSpawnController;
    public Transform playerParent;
    public Transform [] startPoints;
    [System.NonSerialized]
    public GameObject playerGO1;
    private Vector3[] playerStarts;
    private Quaternion[] playerRotations;
    private ArrayList playerList;
    private ArrayList playerTransforms;
    private Player_LBS thePlayerScript;
    private Player_LBS focusPlayerScript;
    [System.NonSerialized]
    public BaseUserManager mainPlayerDataManager;
    private int numberOfPlayers;
    public UI_LBS UIControl;
    [System.NonSerialized]
    public static GameController_LBS Instance;
    public float gameSpeed=1;
    public RadarGUI theRadarControl;
    public GameController_LBS()
    {
        Instance=this;
    }
    public void Start()
    {
        Init();
        Time.timeScale=gameSpeed;
    }
    public void Init()
    {
        Invoke("StartPlayer",1);
        SpawnController.Instance.Restart();
        numberOfPlayers=playerPrefabList.Length;
        // 初始化一些我们可以用来设置玩家的临时数组
        Vector3[] playerStarts = new Vector3[numberOfPlayers];
        Quaternion[] playerRotations = new Quaternion[numberOfPlayers];
        // 我们将使用那些必须在编辑器中设置的起始位置数组，
        // 这意味着我们总是需要
```

```cs
// 确保为玩家数量提供足够的起点
for ( int i = 0; i < numberOfPlayers; i++ )
{
  // 从检查器（inspector）设置的起始变换
  // 中获取位置和旋转值
  playerStarts(i) = (Vector3)startPoints[i].position;
  playerRotations(i) = (Quaternion)startPoints[i].rotation;
}
SpawnController.Instance.SetupPlayers(playerPrefabList,
playerStarts, playerRotations, playerParent, numberOfOfPlayers);
playerTransforms=new ArrayList();
// 现在获取每个玩家控制脚本
// 的引用
playerTransforms =
SpawnController.Instance.GetAllSpawnedTransforms();
playerList=new ArrayList();
for ( int i = 0; i < numberOfPlayers; i++ )
{
  Transform tempT=(Transform)playerTransforms[i];
  Player_LBS tempController=
  tempT.GetComponent<Player_LBS>();
  playerList.Add(tempController);
  tempController.Init();
}
// 获取玩家游戏对象的引用供以后使用
playerGO1 = SpawnController.Instance.GetPlayerGO( 0 );
// 获取聚焦玩家的控制脚本，
// 这样我们就可以执行访问速度变量等操作
tPlayerScript = { Player_LBS }
playerGO1.GetComponent<Player_LBS>();
// 为此玩家分配 ID 为 0
tPlayerScript.SetID( 0 );
// 设置玩家控制
tPlayerScript.SetUserInput(true );
// 因为这是用户，我们希望在 UI 等方面关注此玩家
focusPlayerScript = thePlayerScript;
// 检查是否有可以观察的相机目标对象
Transform aarget=
playerGO1.transform.FindChild("CamTarget");
if(aTarget!=null)
{
  // 如果有相机目标对象，而不是
  // 主玩家，我们使用该目标
  Camera.main.SendMessage("SetTarget", aTarget);
} else {
    // 告诉相机脚本目标是玩家
    Camera.main.SendMessage("SetTarget",
    playerGO1.transform);
}
// 最后，告诉雷达新玩家
tRadarControlsScript.SetCenterObject( playerGO1.transform );
void StartPlayer() {
    // 获取主玩家数据管理器引用，以便
    // 稍后更新其值（得分、生命值等）
    mainPlayerDataManager = 
    playerGO1.GetComponent<BasePlayerManager>().DataManager;
    // 准备就绪，开始吧！
    thePlayerScript.GameStart();
}
public override void EnemyDestroyed( Vector3 aPosition, int pointsValue, int hitByID) {
    // 告诉我们的音频控制器播放爆炸声
    BaseSoundController.Instance.PlaySoundByIndex(1, aPosition);
    // 告诉主数据管理器增加分数
    mainPlayerDataManager.AddScore( pointsValue );
    // 更新 UI 分数
    UpdateScoreUI( mainPlayerDataManager.GetScore() );
    // 在敌人位置播放爆炸效果
    Explode( aPosition );
    // 告诉生成控制器我们离下一波
    // 近了一个敌人
    WaveSpawnController.Fragged();
}
public void PlayerHit(Transform whichPlayer) {
    // 告诉我们的音频控制器播放爆炸声
    BaseSoundController.Instance.PlaySoundByIndex(2, whichPlayer.position);
    // 调用爆炸函数！
    Explode( whichPlayer.position );
}
public void AddEnemyToRadar( Transform aTransform) {
```
