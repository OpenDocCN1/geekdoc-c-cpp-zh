

## 11.6 玩家控制器 (Player Controller)

Lazer Blast 使用了 Unity 自带的 Angry Bots 教程中的动画人物模型。它使用继承自第 5 章所示俯视角控制器脚本的类，并为其添加了自定义的游戏特定脚本，以及一个独立的类来处理角色模型的动画。

玩家类 _LBS 继承自控制器脚本 BaseTopDown.cs*，后者是 Unity 自带的第三称控制器脚本的修改版本，该脚本使用 Unity 内置的字符控制器来处理物理效果。BaseTopDown.cs 在第 5 章（构建玩家移动控制器）中有详细的介绍。

Player_LBS.cs 看起来如下：

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

    // 让玩家一段时间内无敌
    MakeInvulnerable();

    // 显示船体
    theMeshGO.SetActive(true);

    // 显示武器
    weaponControl.EnableCurrentWeapon();
}

void OnEnter(Collision collision)
{
    // 如果玩家处于无敌状态，则忽略碰撞
    if (isInvulnerable) return;

    // 检查是否撞到了弹药
    if (collision.gameObject.CompareTag("Projectile"))
    {
        LostLife();
    }
}

void MakeVulnerable() 
{
    isInvulnerable = true;
}

void MakeInvulnerable() 
{
    isInvulnerable = false;
}
```

