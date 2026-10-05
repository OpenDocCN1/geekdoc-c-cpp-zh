
此游戏的游戏控制器是通过附加在名为 `LevelSetup` 的空游戏对象上的 `LevelSetup` 脚本组件动态创建的。本章稍后会详细介绍脚本，但该脚本的基本功能是检查场景中是否存在游戏控制器，如果不存在，则实例化一个。它引用了两个名为 `GameController` 的偏好设置和一个 `SceneManager`。

通过动态创建游戏控制器和场景管理器对象，这些对象可以跨不同的游戏关卡存在。关卡设置脚本首先检查它们是否存在，如果游戏场景不是第一个关卡，则这些对象将不会被意外复制。

当游戏控制器制体被实例化时，其游戏对象在 Unity 编辑器的层级（Hierarchy）窗口中显示如下：

- GameController
  - GameCamera
    - BulletDestroyer
    - BulletDestroyer
    - Player_Parent_Object
    - StarsLayer1
      - StarsLayer1
- UI
  - GAMEO_GRAPHIC
  - GET_READY_GRAPHIC

可以看出，`GameController` 制体包含了游戏控制器运行、创建玩家以及在游戏期间可以使用相机和 UI 所需的所有内容。制体包含了运行游戏所需的最小元素，即最重要的元素。除了每个游戏场景中的 `LevelSetup` 游戏对象外，关卡场景中的其他所有内容都是关卡特定的。

## 14.3 制体 (Prefabs)

此游戏使用的制体有：

- ENEMIES（敌人）
  - EnemyShip_1
  - EnemyShip_2
  - EnemyShip_3
  - Gameboss

- LEVEL CONTROL（关卡控制）
  - GameController

- PLAYERS（玩家）
  - PlayerShip_1
  - PlayerShip_2

- POWERUPS（强化道具）
  - Powerup

- PROJECTILES（射物）
  - Double_Projectile
  - Projectile_1

- SPWNERS（生成器）
  - AttackPattern_1
  - AttackPattern_2
  - AttackPattern_3
  - AttackPattern_4
  - AttackPattern_5

- WEAPONS（武器）
  - 3WayBlaster_Boss

## 14.3.1 材质

游戏使用了这些材料：

- 1. 游戏控制器——此游戏的游戏控制器脚本派自 `BaseGameController.cs`

- 2. 玩家：
  - PlayerSpaceShip_IP
  - 标准槽位武器控制器
  - 基础玩家管理器
  - 键盘输入和鼠标输入

- 3. 敌人：
  - a. 基础点跟随者
  - b. 基础AI控制器

- 4. 场景管理器

- 5. 用户界面——游戏内用户界面派自第 4 章的 `BaseUIDataManager` 脚本，该脚本增加了数据管理功能。主菜单使用了第 10 章概述的主菜单系统。

- 6. 音频控制器——第 8 章的音频控制器脚本。

- 7. 音乐控制器

## 14.3.2 GameController_IP

`GameController_IP` 脚本：

```cs
using UnityEngine;
using System.Collections;
public class GameController_IP : BaseGameController
{
    public string mainSceneName = "menu_IP";
    public bool didinit;
    public Transform playerParent;
    public GameObject[] playerPrefabList;

    public GameObject powerPrefab;

    public float levelForwardSpeed = 1f;
    public Transform CameraTransform;

    [System.NonSerialized]
    public GameObject playerGO1;
    public GameObject playerGO2;

    private Player_SpaceShip_IP playerScript1;
    private Player_SpaceShip_IP playerScript2;

    public BaseUserManager mainPlayerDataManager1;
    public BaseUserManager mainPlayerDataManager2;

    private int powerupExplosionCount = 0;
    public int numberOfExplosionsToMakePowerup = 10;

    public UI_IP UIControl;
    public UI_Gameover gameUIScript;

    public BaseCameraController cameraControl;

    private int tempINT;
    private Vector3 tempVec3;
    private Quaternion tempQuat;

    private bool isStopped;

    [System.Serialized]
    public static GameController_IP Instance;

    public float gameSpeed = 8;

    public bool BossWinToNextLevel = true;

    // 应该始终有一个玩家
    public int totalPlayers = 1;

    public SceneManager sm;

    public float CameraStartPositionZ = -11;

    public GameController_IP()
    {
        Instance = this;
    }

    public void Start()
    {
        // 我们希望让游戏控制器贯穿整个
        // 游戏，所以使用 DontDestroyOnLoad 来保持它的存
        DontDestroyOnLoad(this.gameObject);
    }

    public void LevelLoadingComplete()
    {
        Init();
        UIControl.Init();
    }

    public void Init()
    {
        // 告诉玩家 4 秒后可以移动
        Invoke("StartPlayer", 4);

        // 以防我们需要更改时间缩放，在这里进行设置
        Time.timeScale = gameSpeed;

        // 我们将玩家人数存储在偏好设置中
        // 这样可以在其他地方（例如主菜单）设置
        // 并带到游戏的每个关卡中
        if (PlayerPrefs.HasKey("totalPlayers")) // 该偏好设置是否存在？
        {
            totalPlayers = PlayerPrefs.GetInt("totalPlayers");
            // 使用存储的值
        } else
        {
            totalPlayers = 1; // 默认单人玩家
        }

        // 找到玩家父物体
        playerParent = GameObject.Find("Player_Parent_Object").transform;
        Vector3[] playerStarts = new Vector3[totalPlayers];
        Quaternion[] playerRotations = new Quaternion[totalPlayers];

        // 这可能有点过头，但硬编码
        // 将不符合整体的重用主题
        for (int i = 0; i < totalPlayers; i++)
        {
            tempQuat = Quaternion.identity;

            if (i == 0)
            {
                // 将玩家 1 放在默认起始
                // 位置 -5,0,0
                tempVec3 = new Vector3(-5, 0, 0);
            }
            else
            {
                // 我们将玩家 2 设置在玩家 1
                // 起始位置右侧 5 个单位
                tempVec3 = new Vector3(-5 + (i * 5), 0, 0);
            }
            playerStarts[i] = tempVec3;
            playerRotations[i] = tempQuat;
        }
    }
}
```

