
`TEMPWeapon = (BaseWeaponScript) weaponScripts[selectedWeaponSlot];`

默认情况下，发射方向沿变换的正向向量：

```
theDir = myTransform.forward;
```

当 `useForceVectorDirection` 被设置为 `true` 时，`theDir` 被设置为来自变量 `forceVector` 的向量，该向量应该在 Unity 编辑器的 Inspector 面板上在 gameObject 上设置：

```
if (useForceVectorDirection )
    theDir = forceVector;
```

`ownerNum` 变量在本节的之前提到过，它通过 `SetOwner` 函数设置。当调用当前选定武器的 `Fire()` 函数时，它会接收一个 `Vector3` 和所有者 ID：

```
// 发射射体
TEMPWeapon.Fire(theDir, ownerNum);
```

```
}
```

### 6.1.2 BaseWeaponScript.cs

这里是 `BaseWeaponController.cs` 的完整形式：

```cs
using UnityEngine;
using System.Collections;
public class BaseWeaponScript : MonoBehaviour
{
    [Serialized]
    public bool canFire;
    public int ammo = 100;
    public int maxAmmo = 100;
    public bool InfiniteAmmo;
    public GameObject projectileGO;
    public Collider parentCollider;
    public Vector3 fireVector;
    public Transform myTransform;
    public int myLayer;
    public Vector3 spawnPos;
    public float forwardOffset = 1.5f;
    public float reloadTime = 0.2f;
    public float projectileSpeed = 10f;
    public bool inheritVelocity;
    public Transform theProjectile;
    private GameObject theGO;
    private bool isLoaded;
    private ProjectileController theController;
    public virtual void Start()
    {
        Init();
    }
    public virtual void Init()
    {
        // 缓存变换
        myTransform= transform;
        // 缓存层（我们将设置所有射体的层
        // 以免它们击中自己！）
        myLayer=gameObject.layer;
        // 加载武器
        Reloaded();
    }
    public virtual void Enable()
    {
        // 如果已经是启用状态，则跳出
        if(canFire==true)
            return;
        // 启用武器（如显示武器网格等）
        canFire=true;
    }
    public virtual void Disable()
    {
        // 如果已经是禁用状态，则跳出
        if(canFire==false )
            return;
        // 隐藏武器（如隐藏武器网格等）
        canFire=false;
    }
    public virtual void Reloaded()
    {
        // 'isLoaded' 变量告诉我们武器是否已加载
        // 准备好发射
        isLoaded= true;
    }
    public virtual void SetCollider( Collider aCollider)
    {
        parentCollider= aCollider;
    }
    public virtual void Fire( Vector3 aDirection, int ownerID )
    {
        // 确保检查 canFire，以便根据需要
        // 启用或禁用！
        if (!canFire)
            return;
        // 如果武器未加载，则跳出
        if(!isLoaded)
            return;
        // 如果弹药耗尽且没有无限弹药，
        // 跳出……
        if(ammo<=0 && !isInfiniteAmmo)
            return;
        // 减少弹药
        ammo--;
        // 生成实际射体
        FireProjectile( aDirection, ownerID);
        // 在再次发射之前我们需要加载
        isLoaded= false;
        // 在 <reloadTime> 秒后调度重新加载
        // 方法："Reloaded"
        Invoke("Reloaded", reloadTime);
    }
    public virtual void FireProjectile( Vector3 fireDirection, int ownerID )
    {
        // 制作我们的第一个射体
        theProjectile= MakeProjectile( ownerID);
        // 将射体导向发射方向
    }
    protected abstract GameObject MakeProjectile(int ownerID); 
}
```

```cs
theProjectile.LookAt(theProjectile.position + 
fireDirection);
```

```cs
// 使用力来移动我们的射物体
theProjectile.rigidbody.velocity= fireDirection *
projectileSpeed;
}
```

```cs
public virtual Transform MakeProjectile( int ownerID ) 
{
    // 创建一个射物体
    theProjectile= SpawnController.Instance.Spawn( projectileGO,
    myTransform.position=spawnPosOffset + (myTransform.forward
    * forwardOffset), myTransform.rotation);
    theGO=theProjectile.gameObject;
    theProjectile.layer=myLayer;
// 获取射物体控制器的引用，以便我们传递
// 关于它的信息
theProjectileController=theGO.GetComponent<Proj
tileController>();
// 设置所有者 ID，以便我们知道是谁发送的
theProjectileController.SetOwnerType(ownerID);
```

```cs
// 注意：确保 parentCollider 是一个代表发射对象的
// 碰撞网格，或者是在从车辆上发射时
// 可能被射物体击中的碰撞网格
// 该系统的一个局限性是它只能可靠地支持
// 单个碰撞网格
if(parentCollider!=null) 
{
    // 禁用我们与我们的射物体之间的碰撞
    // 以免被自己击中！
    Physics.IgnoreCollision(theProjectile.collider,
    parentCollider);
}
// 返回此射物体，以防我们想对它进行
// 其他操作
return theProjectile;
}
```

### 6.1.2.1 脚本解析

`BaseWeaponScript` 类继承自 `MonoBehavior`:

```cs
using UnityEngine;
using System.Collections;
public class BaseWeaponScript : MonoBehaviour
{
    public virtual void Start()
    {
        Init();
    }
}
```

`Init()` 开始获取挂载此脚本的 gameObject 的 `transform` 和 `layer`（层级）。这将用于禁用武器层与实际射物体之间的碰撞，以便射物体在实例化后不会立即爆炸：`Init()`

```cs
public virtual void Init()
{
    // 缓存 transform
    myTransform= transform;
    // 缓存层（我们将设置所有射物体以避免
    // 层级碰撞，以免物体之间相互碰撞！）
    myLayer= gameObject.layer;
    // 加载武器
    Reloaded();
}
```

`Enable()` 和 `Disable()` 函数分别将布尔变量 `canFire` 设置为 `true` 和 `false`。这将在代码的其他地方在允许任何射物体发射之前进行检查。请注意，武器的视觉表示在这里并不被隐藏；该任务留给槽位控制脚本来处理，而不是武器本身：

```cs
public virtual void Enable()
{
    canFire=true;
}
public virtual void Disable()
{
    canFire=false;
}
```

当武器发射时，假设它在一段时间内不会被重新加载（否则，理论上，你每秒可以发射数千上个射物体）。为了跟踪武器何时处于加载状态，此脚本使用了布尔变量 `isLoaded`。发射后对 `Reloaded()` 函数的定时调用将再次重置武器状态：

```cs
public virtual void Reloaded()
{
    // 'isLoaded' 变量告诉我们武器是否已加载
    // 并已准备好发射
    isLoaded=true;
}
```

`Collider()` 用于设置让射物体忽略的碰撞器。例如，当脚本应用到玩家时，它应该忽略玩家的碰撞器，以防止新创建的射物体立即爆炸。它应该使用 Unity 编辑器的 Inspector 窗口设置为一个在射物体生成时可能销毁射体的碰撞器。如果没有 `parentCollider`，脚本仍可以工作，但射物体将不会忽略任何碰撞器：

```cs
public virtual void SetCollider( Collider aDecoder)
{
    parentCollider=aCollider;
}
```

`Fire()` 函数接收两个参数：代表发射方向的 `Vector3` 和一个提供其所有者 ID 编号的 `integer`（该 ID 主要用于碰撞代码，以确定如何反应）：

```cs
public virtual void Fire( Vector3 aDirection, int ownerID)
```

布尔变量 `canFire` 需要为 `true`（允许武器发射），且 `isLoaded` 需要为 `true`（武器已准备好发射）。这里的逻辑在 OCR 文本中似乎是碎片的，但根据提供的代码片段的逻辑流）：

```cs
if(canFire)
{
    // ... 发射逻辑 ...
}
if(!isLoaded)
{
    // ... 重新加载逻辑 ...
}
```

为了防止投射物与父物体或其他紧密生成的投射物发生碰撞，使用了 `Physics.IgnoreLayerCollision()`。`Physics.IgnoreLayerCollision()` 需要两个数字（均为整数），表示哪些层之间应该忽略相互碰撞。层号可以通过菜单 `Edit -> Project Settings -> Unity Editor Inspector` 访问，通过点击层下拉菜单并点击 `Add layer` 按钮从 `Tags and Layers` 管理器中获取。这是全局生效的，这意味着一旦两个层进入 Unity 的列表，放置在这些层上的所有物体都将不再检测碰撞。

在这种情况下，第一层层是通过 `myTransform.gameObject.layer` 获取的武器层，第二个层则取自变量 `myLayer`，该变量在脚本的 `Init()` 函数中设置：

```
Physics.IgnoreLayerCollision(myTransform.gameObject.layer, myLayer);
```

在 Unity 编辑器 Inspector 窗口中避免投射物与任何父级碰撞器引用之间碰撞的更好解决方案。代码的这部分检查 `parentCollider` 是否为空；如果它包含内容，则使用 `Physics`。当脚本可以通过 `parentCollider` 访问到碰撞器时（如在 Unity Inspector 窗口中设置），将使用 `Physics.IgnoreCollision` 来告诉引擎忽略这两个特定碰撞器之间的碰撞。

虽然 `Physics.IgnoreLayerCollision()` 用于禁用两个层上物体之间的碰撞，但 `Physics.IgnoreCollision` 函数会停止指定碰撞器上的碰撞事件：

```
if (parentCollider==null)
{
    // 禁用“我们”和投射物之间的碰撞
    // 以免被自己击中！
    Physics.IgnoreCollision(theProjectile.collider, parentCollider);
}
```

当从本节之前显示的 `Fire()` 函数中调用此处时，新创建的投射物需要返回给调用它的函数，而此脚本的最后部分代码正是此操作：

```
// 返回此投射物，以防我们想对它
// 做些什么
return theProjectile;
```

在书的后续内容中，将检查示例游戏，这些基础脚本将再次出现，我们将看到如何将它们应用于真实的游戏场景中。在第 9 章中，我们将研究为游戏添加人工智能（AI），以及武器控制器如何轻松地接入其中并由游戏中的 AI 玩家控制。

## 第 7 个配方：路点管理器 (Waypoints Manager)

### 7.1 路点系统 (Waypoint System)

赛车游戏 *Motor Vehicle Doom* 和射击游戏 *Interstellar Paranoids* 都为 AI 玩家需要路点。在 *Motor Vehicle Doom* 中，我们为 AI 以及主玩家使用路点，原因如下：

- 1. 检查主玩家是否正朝着正确的方向行驶。汽车控制器代码将跟踪玩家在赛道上的位置（基于通过了哪个路点），并检查其前进向量，以确保它面向赛道上的下一个路点。如果玩家的前进向量不在特定的容差角内，游戏将显示错误方向消息并最终以正确的方式重新生成车辆。
- 2. 允许复活系统在赛道上找到一个“安全”地点来复活玩家，并利用其旋转将复活车辆朝向赛道的正确方向。
- 3. 找出车辆绕赛道行驶的距离，这用于与其他玩家的进度量进行比较，以计算比赛排名。

*Interstellar Paranoids* 使用路点来移动所有的敌人。敌人是简单的路径跟随者，沿着路径移动并射击，直到到达终点并在那里被销毁。

`Waypoints_Controller cs` 脚本与我上一本书 *Game Development for iOS*（同样由 CRC Press 出版）中的非常相似。路点控制器已从原始的 JavaScript 格式转换为 C#：

```csharp
public class Waypoints_Controller : MonoBehaviour
{
    [ExecuteInEditMode]
    // 此脚本只是为我们提供了一个视觉路径，以便更容易编辑
    // 我们的点
    private ArrayList transforms; // 用于方便访问的 arraylist
    // transforms
    private Vector3 firstPoint; // 存储第一个路点，以便我们可以
    // 循环路径
    private float distance; // 用于计算点之间的
    // 距离
    private Transform TMPrans; // transform 的临时存储容器
    private int TMPPIndex; // 索引数的临时存储容器
    private int totalTransforms;
