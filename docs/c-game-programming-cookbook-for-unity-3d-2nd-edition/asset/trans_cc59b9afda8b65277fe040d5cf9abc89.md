
{
    if (!didInit)
        Init();
    global_userDatas[id].isFinished = aVal;
}
}

## 4.4 BasePlayerStatsController 类

你可以在文件夹 GPC_Framework/Scripts/BASE/PLAYER 中找到此类。

我的玩家控制器派生自多个其他类，其中之一是 BasePlayerStatsController，该类为玩家控制器提供了一系列处理用户数据的函数。好吧，这并不是 BasePlayerStatsController 的唯一功能。它也只是用来保存与游戏中处理玩家相关的任何变量，但 BasePlayerStatsController 主要充当我的玩家脚本与用户数据之间的友好接口。例如，我可以在玩家控制器中调用 SetHealth(an amount) 而无需担心用正确的 ID 标识我的玩家或类似的事情。BasePlayerStatsController 中用于设置 UserData 的函数已经处理了 ID 以及 UserDataManager 需要如何调用的问题。

BasePlayerStatsController.cs 脚本完整内容如下：

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

namespace GPC
{
    [RequireComponent(typeof(BaseUserManager))]
    public class BasePlayerStatsController : ExtendedCustomMonoBehaviour
    {
        public BaseUserManager _myDataManager;
        public int myID;

        public BaseInputController _inputController;
        public bool disableAutoPlayerListAdd;

        public virtual void Init()
        {
            // cache the usual suspects
            _RB = GetComponent<Rigidbody>();
            _GO = GetComponent<GameObject>();
            _TR = GetComponent<Transform>();
            _inputController = GetComponent<BaseInputController>();
            SetupDataManager();
        }

        public virtual void SetPlayerDetails(int anID)
        {
            // this function can be used by a game manager to pass in details from the player list, such as
            // this players ID or perhaps you could override this in the future to add avatar support, loadouts or
            // special abilities etc.?
            myID = anID;
        }

        public virtual void SetupDataManager()
        {
            // if a player manager is not set in the editor, let's try to find one
            if (_myDataManager == null)
                _myDataManager = GetComponent<BaseUserManager>();
            if (_myDataManager == null)
                _myDataManager = gameObject.AddComponent<BaseUserManager>();
            if (_myDataManager == null)
                _myDataManager = GetComponent<BaseUserManager>();
            if (!disableAutoPlayerListAdd)
            {
                // add the player (set up data) to the ScriptableObject we use to store player info
                myID = _myDataManager.AddNewPlayer();
                _myDataManager.SetName(myID, "Player");
                _myDataManager.SetHealth(myID, 3);
            }
        }
        public virtual void AddScore(int anAmount)
        {
            if (!didInit)
                Init();
            _myDataManager.AddScore(myID, anAmount);
        }
        public virtual void AddHealth(int anAmount)
        {
            if (!didInit)
                Init();
            _myDataManager.AddHealth(myID, anAmount);
        }
        public virtual void ReduceScore(int anAmount)
        {
            if (!didInit)
                Init();
            _myDataManager.ReduceScore(myID, anAmount);
        }
        public virtual void ReduceHealth(int anAmount)
        {
            if (!didInit)
                Init();
            _myDataManager.ReduceHealth(myID, anAmount);
        }
        public virtual void SetLives(int anAmount)
        {
            if (!didInit)
                Init();
            _myDataManager.SetLives(myID, anAmount);
        }
```

```
public virtual void AddLives(int anAmount)
{
    if (!didInit)
        Init();
    _myDataManager.AddLives(myID, -anAmount);
}

public virtual void ReduceLives(int anAmount)
{
    if (!didInit)
        Init();
    _myDataManager.ReduceLives(myID, anAmount);
}

public virtual void SetScore(int anAmount)
{
    if (!didInit)
        Init();
    _myDataManager.SetScore(myID, anAmount);
}

public virtual void SetHealth(int anAmount)
{
    if (!didInit)
        Init();
    _myDataManager.SetHealth(myID, anAmount);
}

public virtual void SetName(string aName)
{
    if (!didInit)
        Init();
    _myDataManager.SetName(myID, aName);
}

public int GetLives()
{
    if (!didInit)
        Init();
    return _myDataManager.GetLives(myID);
}

public int GetHealth()
{
    if (!didInit)
        Init();
    return _myDataManager.GetHealth(myID);
}

public int GetScore()
{
    if (!didInit)
        Init();
    return _myDataManager.GetScore(myID);
}
}
}
```

立刻就能注意到，上面的代码与 BaseUserManager 类有很多相似之处。上面的脚本很大一部分都是对 BaseUserManager 中对应函数的调用——通过在这里复制这些函数并调用它们，我们将 BaseUserManager 的所有功能都添加到玩家脚本中，并简化了调用方式。例如，我每次调用为玩家分数总额添加分数时，都不必检查一切是否已设置并可用。我也不想每次都传入 ID，因此上面的代码中的函数如 GetHealth() 和 AddScore() 进一步简化了与 BaseUserManager 的交互。如果你向 UserData 添加了更多变量，你需要在 BaseUserManager 和 BasePlayerStatsController 两者中都添加更改它们的方式。

## 4.5 管理玩家

要管理玩家，请向菜单（或你想最初设置玩家的任何位置）添加一个 BaseUserManager 组件，然后在自己的脚本中设置对其的引用并调用 ResetUsers() 以清除现有用户，然后调用 AddNewPlayer 添加新玩家。

有关工作示例，请参阅第 14 章赛车游戏示例的主菜单部分。

![](img/e4b578cd512539e7261e070d87b6550a_92_0.png)

Taylor & Francis
Taylor & Francis Group
http://taylorandfrancis.com

## 5 Recipes

### Common Components

### 5.1 Introduction

本章中的实用脚本和常用系统可能对各种类型的游戏项目都有帮助。在 Assets/GPC_Framework/Scripts/COMMON 文件夹中，你会找到一套多样化的可重用脚本，如计时器和摄像机控制器。本章重点介绍这些独立脚本。你可以轻松地将它们取出来用于任何项目，无论是否使用本书中的 GPC 框架。

在 COMMON 文件夹内，有几个子文件夹。它们是；

### AI

这里包含与玩家或自动控制相关的脚本，例如一个与 BaseAIController.cs 脚本对话并充当简单功能性机器人在游戏环境中移动的脚本。

### CAMERA

与摄像机相关的脚本应放在这里，例如第三人称或俯视摄像机代码。

### GAME CONTROL

此文件夹中的脚本涉及整体游戏状态控制。在示例文件中，你会找到：

BattleController 和 GlobalBattleManager – 用于死亡竞赛风格的计分和游戏状态逻辑）

### 5.3.1 第三人称摄像机

第三人称摄像机位于玩家身后。它与跟随摄像机并不完全相同；第三人称摄像机通常围绕玩家轨道移动，而不是简单地跟随其移动。为了形象化这一点，可以想象摄像机被系在一根连接到目标玩家的杆子上。随着玩家的移动，摄像机保持在与之杆长距离的位置，但摄像机可以自由地在玩家周围做圆周运动。摄像机的位置通常在玩家身后，并对其水平移动施加一点阻尼，以便在玩家转弯时获得良好的运动感。在某些第三人称摄像机设置中，摄像机可能被允许相对于目标玩家进出移动。

```
using UnityEngine;
using System.Collections;

namespace GPC
{
    [AddComponentMenu("CSharpBookCode/Common/Cameras/Third Person Cam Controller")]

    public class CameraThirdPerson : BaseCameraController
    {
        public float distance = 20.0f;
        public float height = 5.0f;
        public float heightDamping = 2.0f;

        public float lookAtHeight = 0.0f;

        public float rotationSnapTime = 0.3F;

        public float distanceSnapTime;

        public Vector3 lookAtAdjustVector;

        private float usedDistance;

        float wantedRotationAngle;
        float wantedHeight;

        float currentRotationAngle;
        float currentHeight;

        Quaternion currentRotation;
        Vector3 wantedPosition;

        private float yVelocity = 0.0F;
        private float zVelocity = 0.0F;

        void Update()
        {
```

摄像机的主要更新发生在 Update() 中，而不是 FixedUpdate()。原因是我们希望所有物理相关的更新在移动摄像机之前完成——这应该在 Update() 时已经发生——并且在此过程中，我们的目标对象在摄像机更新结束和下一帧绘制之间不应存在位置差异。绘制时间错误会导致抖动效果，因为我们跟随的对象在摄像机定位之后才更新。
在 Update() 开始时有一个空值检查，以确保我们有目标：

```
if ( _cameraTarget == null)
    return;
```
