

![](img/041dca164b58875f4f1a64abb3328f5c_366_0.png)

图 13.2 坦克战结构。

轮子和不同的模型模型。它们的工作原理与汽车完全相同，只是设置了不同的参数，使得加速和转向更像坦克而不是汽车。

每个玩家都附载了一个战斗控制器组件，并由一个全局战斗管理器管理整个比赛状态；这与 *Metal Vehicle Doom* 中的比赛控制器和全局比赛管理器脚本的格式完全相同。

## 13.1 主游戏场景

坦克战有两个场景：菜单场景和主游戏战斗场场景。

主菜单由单个 gameObject 组成，主菜单脚本在第 10 章中显示。

主游戏场景的层级结构（Hierarchy）包含以下内容：

- ARENA
  - (构成环境的模型，包括一个用于提亮的光方向光)
- GameController
- Main Camera
- MusicController
- Player_Startpoints
  - StartPoint_1 (1–10)
- Players
- SoundController
- UI
- Game Over Graphic
- Get Ready Graphic

注意，游戏控制器在游戏开始时动态创建玩家和敌人。Unity Inspector 窗口中设置了多个 prefabs 和 gameObjects：

- 游戏控制器引用了这些 prefabs 和对象：
  - 爆炸 prefab（用于爆炸的粒子效果）
  - StartPoints 数组，包含对场景中 Startpoint_X gameObjects 的引用
  - Player Prefab List 数组，包含对 Top_Down_Player prefab 的引用
  - 附载在 Sound Controller gameObject 上的 `BaseSoundController.cs` 脚本有一个名为 `Game Sounds` 的数组，包含了：
    - shoot1
    - explode2
    - player_explode
    - spawner 1
  - Spawn Controller gameObject 附载了一个 `WaveSpawner.cs` 实例，其 Spawn Object Prefabs 数组中包含以下引用：
    - Spawn_Structure1
    - Spawn_Structure2
    - Spawn_Structure3
- UI GameObject 附载了一个名为 `UI_LBS.cs` 的脚本。它引用了：
  - GAMEOVER_GRAPHIC gameObject
  - GETREADY_GRAPHIC gameObject

## 13.2 Prefabs

构成游戏的 prefabs 如下：

- PLAYERS
  - Tank
  - AI_Tank
- PROJECTILES
  - Tank_StandardFire
- WEAPONS
  - TankProjectileBlaster_Player
  - TankProjectileBlaster_Enemy

## 13.3 组件

游戏使用了这些组件：

1. Game Controller——此游戏的控制器脚本派自 `BaseGameController.cs`。
2. Battle Controller——每个玩家都附载了一个战斗控制器脚本，存储与其战斗统计相关的信息（击杀数/击杀次数等）。明确来说，一次 frag 指一次命中。当玩家被毁时，计一次 frag。
3. Global Battle Manager——全局战斗管理器与所有玩家战斗控制器通信，并跟踪战斗状态的全局信息，例如玩家位置以及战斗是否仍在。
4. Vehicles（坦克）：
   a. 主玩家
   b. AI 对手
5. Scene Manager
6. User Interface——游戏内界面派自第 4 章的 `BaseUIDataManager` 脚本，该脚本增加了数据管理功能。主菜单使用了第 10 章概述的菜单系统。
7. Sound Controller——第 8 章的音频控制器脚本。
8. Music Controller

## 13.4 Game Controller

控制器脚本 `GameController_TB.cs` 如下所示：

```c
using UnityEngine;
using System.Collections;

public class GameController_TB : BaseController
{
    public string mainMenuSceneName = "menu_TB";
    public int numberOfBattlers = 4;
    public int gameTime = 120;

    public Transform playerParent;
    public Transform [] startPoints;
    public Camera_Third_Person cameraScript;

    [System.Serialized]
    public GameObject playerGO1;

    private CarController_TB thePlayerScript;
    private CarController_TB focusPlayersScript;

    private ArrayList playerList;
    private ArrayList playerTransforms;

    private float speed;
    public GUitext timerText;
    public GUitext postText;

    private bool isAhead;
    private CarController_TB car2;
    private int focusPlayerBattlePosition;

    public GameObject count3;
    public GameObject count2;
    public GameObject count1;

    public GUitext finalPositionText;

    public GameObject [] prefabList;

    [System.Serialized]
    public static GameController_TB Instance;

    public Waypoints_Controller WaypointControllerForAI;

    // 在此处缩放时间
    public float gameSpeed = 1;
    private bool didInit;

    private Timer theTimer;

    public GameController_TB ()
    {
        Instance = this;
    }
    void Start ()
    {
        Init();
    }
    void Init ()
    {
        SpawnController.Instance.Restart();

        // 如果我们需要更改时间缩放，在这里设置
        Time.timeScale = gameSpeed;

        // 告诉战斗
    }
```

