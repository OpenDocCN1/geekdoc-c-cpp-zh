

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

## 11.5.1 脚本详解

Controller_LBS.cs 继承自 BaseGameController，后者又继承自 MonoBehaviour，以便它可以接入 Unity 的某些内置函数调用，如 `Update()`、`Awake()` 和 `Start()`。

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

