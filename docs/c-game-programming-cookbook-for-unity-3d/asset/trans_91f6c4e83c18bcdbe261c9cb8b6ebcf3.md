

```cs
// 保存 accelMax 值以备后用，以防我们需要
// 将其更改以便 AI 捕捉
originalAccelMax=accelMax;

// 如果没有默认输入，则添加一个
onendefault_input=myGO.GetComponent<KeyboardInput>();

if (default_input==null)
    default_input=myGO.AddComponent<Keyboard_Input>();

// 缓存玩家控制器的引用
myPlayerController=myGO.GetComponent<BasePlayerManager>();

// 调用基类初始化
myPlayerController.Init();

// 通过这段简单的车辆代码，我们将重心设置得
// 低以防止汽车翻倒
myBody.centerOfMass=new Vector3(0,-6.5f,0);

// 检查是否能找到引擎声源，如果需要的话
if (engineSoundSource==null)
    engineSoundSource=myGO.GetComponent<AudioSource>();

AddBattleController();

// 获取武器控制器的引用
weaponControl=myGO.GetComponent<BaseWeaponController>();

// 如果在编辑器中没有设置玩家管理器，让我们尝试
// 寻找一个
if (myPlayerManager==null)
    myPlayerManager=
    myGO.GetComponent<BasePlayerManager>();

// 缓存数据管理器引用
DataManager=myPlayerManager.DataManager;

// 设置默认数据
DataManager.SetName("Player");
DataManager.SetHealth(startHealthAmount);

if (isAIControlled)
{
    // 将我们的名称设置为 AI 玩家
    DataManager.SetName("AIPlayer");

    // 设置 AI
    InitAI();
}

isGameRunning=true;

// 存储重生点
respawnPoint=myTransform.position;
respawnRotation=myTransform.eulerAngles;

// 13.7 玩家

Makeulnerable();

// 从音效控制器获取我们的引擎音量
audio.volume=BaseSoundController.Instance.volume;

void InitAI()
{
// 缓存 AI 控制器的引用
AIController=myGO.GetComponent<BaseAIController>();

// 检查是否找到了 AI 组件，如果没有
// 则在此处添加一个
if(AIController==null)
    AIController=myGO.AddComponent<BaseAIController>();

// 初始化 AI 控制器
AIController.Init();

// 告诉 AI 控制器进入路点模式
AIController.SetAIState(AIStates.steer_to_waypoint);

// 禁用我们的默认输入
default_input.enabled=false;

// 添加一个 AI 武器控制器
gunControl=myGO.GetComponent<BaseEnemy>();

// 如果我们还没有武器控制器，让我们添加一个
// 以停止报错，但要警告这可能需要修复
if(gunControl==null)
{
gunControl=myGO.AddComponent<BaseEnemy>();
// 告诉武器控制器执行“查看并销毁”状态
gunControl.currentState=AttackStates.look_and_destroy;
}

void AddBattleController()
{
if(myGO==null)
myGO=gameObject;
// 为我们的对象添加战斗控制器脚本
battleControl=myGO.AddComponent<BattleController>();

// 从战斗控制器脚本中获取 ID，这样我们就不需要
// 每次与全局战斗控制器通信时都去查找它
id=battleControl.GetID();

// 我们将为这个玩家及其// 武器使用相同的 id
weaponControl.SetOwner(id);

// 使用重复调用来更新我们的位置，而不是
// 在单帧或 update 中调用它
InvokeRepeating("UpdatePosition",0, 0.5f);

public void UpdateBattlePosition()
{
// 从全局战斗管理器获取我们的得分板位置
GlobalBattleManager.Instance.GetPosition(id);
}

public override void UpdatePhysics()
{
if(canControl)
base.UpdatePhysics();

if(isFinished)
myBody.velocity *=0.99f;

// 如果我们移动较慢，我们对身体施加额外的力
// 以便我们可以做绕圈动作 - 注意由于没有
//“地面”，它也会在空中施加（这糟糕！）
if(mySpeed < TorqueHelperMaxSpeed)
{
myBody.AddTorque(new Vector3(0, steer * myBody.mass * TorqueHelper, 0));
}

private float timide;
public override void LateUpdate()
{
// 从战斗控制器获取战斗状态
isGameRunning=battleControl.battleRunning;

if(isGameRunning)
{
// 检查我们是否撞了车并且处于倒朝状态
Check_Car_Is_Flipped();
}

// 确保 gunControl 已告知它可以射击
if(isAIControlled)
gunControl.canControl=true;

// 我们在 LateUpdate 中检查输入，因为 Unity 推荐这么做
if(temp.layer==17 || temp.layer==9)
{
// 获取弹体的引用
aProj=tempGO.GetComponent<ProjectileController>();
    
// 快速检查此弹体是否不是由此玩家发射
if (aProj.ownerTypeId != id ) 
{
// 告诉 hit 函数这次碰撞，传入 gameObject
// 以便我们可以获取其弹体控制器脚本
// 并发现更多关于它的来源
Hit();
// 告诉我们的战斗控制器我们被击中了
battleControl.Fragged();
}
    
// 通知全局战斗控制器是谁击杀了我们
GlobalBattleManager.Instance.RegisterFrag(aProj.ownerTypeId);
}

public void OnTriggerEnter( Collider other )
{
// 检查触发器是否使用了任何我们希望
// 在碰撞时自动让玩家重生的层
int objLayerMask = (1 << other.gameObject.layer);
    
if ((respawnLayerMask.value & objLayerMask) > 0)
{
    Respawn();
}
}

void Hit()
{
// 减少一个生命值
myDataManager.ReduceHealth(1);
    
    if (myDataManager.GetHealth()<1) // 被销毁
    {
        isRespawning=true;
        
        // 爆炸！（施加一个力来影响周围的一切
// 并让模型也旋转起来 - 带有角速度）
        myBody.AddExplosionForce(myBody.mass * 2000f,
myBody.position, 100);
myBody.angularVelocity=new Vector3( Random.Range(-100,100), Random.Range (-100,100), Random.Range(-100,100) );
    }
// 告诉游戏控制器执行一次大大的爆炸
GameController_TB.Instance.PlayerBigHit( myTransform );

// 重生
Invoke("Respawn",4f);

// 重置生命值为满值
myDataManager.SetHealth(startHealthAmount);
}

void Respawn()
{
// 重置“正在重生”变量
isRespawning=false;

// 重置我们的速度以停止旋转
myBody.velocity=Vector3.zero;
myBody.angularVelocity=Vector3.zero;

// 将玩家重新定位到 tempVEC（路点位置）
// 同时设置玩家为路点的旋转，
// 以便我们在重生后面向正确的方向
myTransform.eulerAngles=respawnRotation;
myTransform.position=tempVEC;
}
```
