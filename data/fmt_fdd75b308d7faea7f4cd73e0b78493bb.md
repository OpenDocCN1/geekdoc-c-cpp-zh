
```csharp
public float timeBetweenFireSounds= 0.25f;

public override void Start()
{
    // 我们正在重写 BaseVehicle 的 Start 函数
    // 因为我们不想从这里初始化！游戏
    // 控制器会在准备就绪后调用 Init
    myBody= rigidbody;
    myGO= gameObject;
    myTransform= transform;
}

public override void Init()
{
    Debug.Log("CarController_MVD Init called.");
    // 缓存嫌疑对象
    myBody= rigidbody;
    myGO= gameObject;
    myTransform= transform;
    // 允许从开始时重生
    canRespawn=true;
    // 保存我们的 accelMax 以备后用，以防我们需要
    // 更改它来实现 AI 追赶
    originalAccelMax= accelMax;
    // 如果我们还没有默认键盘输入，则添加一个
    if(default_input==null)
        default_input=myGO.AddComponent<Keyboard_Input>();
    // 缓存玩家控制器的引用
    myPlayerController= myGO.GetComponent<BaseManager>();
    // 基类初始化
    myPlayerController.Init();
    // 通过这段简单的代码，我们将重心设得
    // 较低以防止车辆翻倒
    myBody.centerOfMass= new Vector3(0,-3.5f,0);
}
```

```csharp
if (AIControlled)
{
    // 将我们的名字设为 AI
    myData.SetName("AI");
    // 设置 AI
    InitAI();
}

void InitAI() {
    // 缓存 AI 控制器的引用
    AIController= myGO.GetComponent<BaseAIController>();
    // 检查是否找到了 AI 控制器，
    // 如果没有则添加一个
    if(AIController==null)
        AIController= myGO.AddComponent<BaseAIController>();
    // 初始化 AI 控制
    AIController.Init();
    // 告诉 AI 控制器进入路点模式
    AIController.SetAIState(AIStates.steer_to_point);
    // 禁用默认输入
    def_input.enabled=false;
    // 添加 AI 武器控制器
    gunControl= myGO.GetComponent<BaseArmedEnemy>();
    // 如果没有武器控制器，添加一个
    // 防止崩溃并警告
    if( gunControl==null ) {
        gunControl= myGO.AddComponent<BaseArmedEnemy>();
        Debug.LogWarning("WARNING! 初始化缺少 BaseArmedEnemy。玩家无法射击！");
    }
    // 告诉控制器“寻找并销毁”
    gunControl.currentState=AIAttackStates.look_and_destroy;
}
```

```csharp
public void AddRaceController()
{
    if (myGO==null)
        myGO=gameObject;
    // 将比赛脚本添加到我们的对象
    raceControl=myGO.AddComponent<RaceController>();
    // 从比赛脚本获取我们的 racer ID，
    // 这样我们在与全局比赛控制器通信时就不需要查找
    racerID=raceController.GetID();
    // 设置重复调用来更新我们的排名，
    // 而不是每帧或每次更新
    InvokeRepeating("UpdateRacePosition",0, 0.5f);
}

public void UpdateRacePosition()
{
    // 从全局比赛管理器获取我们的排名
    myRacePosition=GlobalRaceManager.Instance.GetPosition(racerID);
}
```

```csharp
public override void UpdatePhysics ()
{
    if (canControl)
        base.UpdatePhysics();
    // 如果我们移动缓慢，施加额外的力来快速转向
    // 车辆以便我们可以转圈（！）请注意由于
    // 没有“地面检测”，它在空中也会应用
    //（糟糕！）
    if(mySpeed < TurnTorqueHelperMaxSpeed)
        myBody.AddTorque(new Vector3( 0, steer * myBody.mass * turnTorqueHelper * motor, 0 ));
}
```

```csharp
private float timid;

public override void LateUpdate()
{
    // 从比赛控制器获取比赛状态
    isRaceRunning= raceControl.raceRunning;
    if(isRaceRunning)
}
```

```csharp
{
  // 检查车辆是否已经翻车并处于倒置
  // 或错误状态(!)
  Check_If_Car_Is_Flipped();
  // 确保 gunControl 已经被告知它可以
  // 射击
  if(isAIControlled) {
    gunControl.canControl=true;
    // 我们在 LateUpdate 中检查输入，因为 Unity
    // 推荐这样做
    if(isAIControlled) {
      GetAIInput();
    } else {
      GetInput();
    }
  } else {
    if(isAIControlled) {
      // 因为比赛还没有开始，我们会告诉
      // AI gunControl 暂时不要射击
      gunControl.canControl=false;
    }
  }
  // 告诉比赛控制器更新路点
  raceControl.UpdateWaypoints();
  // 检查我们的车辆是否应该被固定在地
  CheckLock();
  // 告诉比赛控制检查我们是否在逆行
  raceControl.CheckWrongWay();
  // 检查我们是否在逆行并对此采取行动
  if(raceControl.goingWrongWay) {
    if(isAIControlled) {
      GameController_MVD.Instance.UpdateWrongWay(true);
    }
    // 如果逆行，比较从开始错误
    // 到现在的时间，以判断我们是否需要重生
    if(raceControl.timeWrongWayStarted!=-1) {
      timedef= Time.time - raceControl.timeWrongWayStarted;
      if(timedef-resetTime) {
        // 在错误方向上行驶了 x resetTime 秒，
        // 让这台车重新生成吧！
        Respawn();
      }
    }
  } else if (!isAIControlled) {
    GameController_MVD.Instance.UpdateWrongWay(false);
  }
}
```

```csharp
accelMax = originalAccel;
```

```csharp
// 如果这辆车在比赛中掉队了就追赶
if (isRaceRunning && isAIControlled)
{
    if (myRacePosition>3)
    {
        // 加速
        accelMax= catchUpAccelMax;
    }
    else {
        accelMax= originalAccel;
    }
    // 第一名，让我们慢下来！
    if(myRacePosition<2)
    {
        accelMax= originalAccel*0.25f;
    }
    // 更新引擎音频
    UpdateEngineAudio();
}
```

```csharp
public override void GetInput()
{
    // 计算转向
    steer= Mathf.Clamp ( default_input.GetHorizontal() , -1, 1 );
    // 需要多少油门（力？
    motor= Mathf.Clamp(default_input.GetVertical() , 0, 1 );
    // 需要多少刹车？
    brake=-1 * Mathf.Clamp ( default_input.GetVertical() , -1, 0 );
    if(default_input.GetRespawn() && !isRespawning)
    {
        isRespawning=true;
        Respawn();
        canRespawn=false;
        Invoke("*resetRespawn",2);
    }
    // 首先，确保一个武器控制器存在
    // (否则不需要射击！)
    if(weaponControl != null)
    {
        // 如果我们需要的话就射击
        if(default_input.GetFire() && canFire)
        {
            // 告诉武器控制器处理射击
            weaponControl.Fire();
        }
    }
}
```

```csharp
void resetRespawn()
{
    canRespawn=true;
}

public void GetAIInput (float amount)
{
    // 计算转向
    steer= Mathf.Clamp( AIController.GetHorizontal(), -1, 1 );
    // 需要多少油门？
    motor= Mathf.Clamp( AIController.GetVertical() , 0, 1 );
}

public void FinishedRace()
{
    // 停止允许对车辆进行控制
    canControl = false;
    brake = 1;
    motor = 0;
    // 设置一个标记，方便判断我们何时
    // 比赛结束
    raceControl.RaceFinished();
}

public void SetAIInput (bool aiFlag)
{
    isAIInput = aiFlag;
}

public bool IsFinished()
{
    return raceControl.GetFinished();
}

public int GetCurrentLap()
{
    return raceControl.GetCurrentLap();
}

public int GetCurrentWaypointNum()
{
    return raceControl.GetCurrentWaypointNum();
}

public float GetCurrentWaypointDist()
{
    return raceControl.GetWaypointDist();
}

public bool IsLapDone()
{
    return raceControl.GetLapDone();
}

public void SetWayController(Waypoints aControl)
{
    raceControl.SetWayController(aControl);
}
```

```csharp
void OnCollisionEnter(Collision collider)
{
    // 确保武器没有碰撞体
    // 如果你使用基础几何体，请仅在带有此脚本的
    // gameObject 上使用单个碰撞体
    // 当物体与我们的飞船碰撞时，我们检查它的层级（layer）
    // 查看它是否是我们的弹药（注意：记得在
    // 添加弹药时正确设置层级！）
    if(isAIControlled)
    {
        if(collider.gameObject.layer==9 && !isRespawning && !Invulnerable)
        {
            Hit();
        }
    }
    else {
        if(collider.gameObject.layer==17 && !isRespawning && !Invulnerable)
        {
            Hit();
        }
    }
}

public void OnTriggerEnter(Collider other)
{
    int objLayerMask = (1 << other.gameObject.layer);
    if (respawnLayerMask & objLayerMask)
    {
        Respawn();
    }
}

void Hit()
{
    // 减少生命值
    DataManager.ReduceHealth(1);
    if(DataManager.GetHealth()<1) // 
    {
        isRespawning=true;
    }
    // 爆炸！
    myBody.AddosionForce(myBody.mass * 2000, myBody.position, myBody.angularVelocity-new Vector3(Random.Range(-100,100), Random.Range(-100,100), Random.Range(-100,100)));
    // 告诉游戏控制器处理爆炸
    CameraController_MVD.Instance.PlayerBigHit(myTransform);
    // 重生
    Invoke("Respawn",4f);
    // 重置生命值为满
    DataManager.SetHealth(startHealthAmount);
}

else {
    // 告诉游戏控制器处理轻微伤害
    GameController_MVD.Instance.PlayerHit(myTransform);
}

void Respawn()
{
    // 重置“正在重生”变量
    isRespawning=false;
    // 重置我们的速度，以便我们重新定位
    myBody.velocity+=Vector3.zero;
    myBody.angularVelocity-=Vector3.zero;
    // 获取用于重生的路点
    tempTR=raceController.GetRespawnWaypoint();
    tempVEC=tempTR.position;
    // 从路点向下发射射线以寻找地面
    RaycastHit hit;
    if(Physics.Raycast(tempVEC + (Vector3.up * 300), -Vector3.up, out hit)) {
        tempVEC.y=hit.point.y+15;
    }
    // 在 tempVEC 重新定位玩家（通过射线检测修正 y 值）
    // 同时也将玩家旋转设置为路点的旋转，
    // 确保重生后面向正确的方向
    myTransform.rotation=tempTR.rotation;
    myTransform.position=tempVEC;
    // 我们需要一段时间的无敌状态
    MakeInvulnerable();
    Invoke("MakeVulnerable",3);
    // 回到第一种武器
    if(weaponControl!=null) {
}
```
