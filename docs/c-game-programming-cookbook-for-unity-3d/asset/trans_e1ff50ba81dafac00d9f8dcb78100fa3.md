
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

    private Vector3 diff;
    private float floatDistance;
    private Transform closest;

    private Vector3 currentPos;
    private Vector3 lastPos;
    private Transform pointT;

    public bool closed=true;
    public bool shouldReverse;

    void Start()
    {
        // 确保当此脚本启动时
        // 我们已经获取了每个路点的 transforms
        GetTransforms();
    }

    void OnDrawGizmos()
    {
        // 我们只在编辑时绘制路点，
        // 不在玩游戏时绘制
        if (Application.isPlaying)
            return;

        GetTransforms();
        // 确保列表中多于一个 transform
        // 否则我们无法在它们之间画线
        if (totalTransforms < 2)
            return;

        // 绘制我们的路径，我们获取第一个
        // 路点的位置，以便我们的线有一个起点
        Transform TMPtrans = (Transform)transforms[0];
        lastPos = TMPtrans.position;

        // 我们让每个路点指向下一个，这样
        // 就能旋转就可以出玩家
        // 是面朝哪个方向
        for (int i = 0; i < totalTransforms; i++)
        {
            Transform TempTrans = (Transform)transforms[i];
            if (TempTrans == null)
            {
                GetTransforms();
                return;
            }

            // 更新“上一个”路点变为
            // 当前这，因为我们需要
            lastPos = TempTrans.position;

            // 更新当前的“胜利者”
            //（最近的 transform）为
            // 我们刚刚找到的 transform
            // ... 逻辑继续
        }

        Gizmos.color = Color.green;
        Gizmos.DrawSphere(currentPos,2);

        if (closed)
        {
            Gizmos.color = Color.red;
            Gizmos.DrawLine(lastPos, firstPos);
        }
    }

    public void SetReverseMode(bool rev)
    {
        shouldReverse=rev;
    }

    public void GetTransforms()
    {
        // 将所有路点存储在 ArrayList 中
        // 它在在这里初始化（在我们可以使用 ArrayLists
        // 之前总是需要这样做）
        transforms=new ArrayList();

        // 现在我们遍历此 transform “下方”的 transforms
        // 所以所有的子对象都作为路点
        foreach(Transform t in transform)
        {
            // 将此 transform 添加到列表
            transforms.Add(t);
        }
        totalTransforms=(int)transforms.Count;
    }

    public int FindNearestWaypoint (Vector3 fromPos, float maxRange)
    {
        // 确保我们已经填充了 transforms
        // 列表，如果没有，则填充
        if(transforms==null)
            GetTransforms();

        // distance 变量仅用于在比较时持有
        // “当前”距离，这样我们就能
        // 找到最近的 distance = Math.Infinity;

        // 遍历它们并找到最近的一个
        for (int i = 0; i < transforms.Count; i++)
        {
            // 获取 transform 的引用
            Transform TempTrans = (Transform)transforms[i];

            // 计算当前 transform 
            // 和传入的 transform 之间的距离
            diff = (TempTrans.position - fromPos);
            float curDistance = diff.sqrMagnitude;
            // 现在比较距离——确保
            // 我们不比最近的物体更近
            //（其距离由变量
            // (distance）持有）
            if (curDistance < distance)
            {
                if (Math.Abs(TempTrans.position.y - fromPos.y) < maxRange)
                {
                    // 设置当前的“胜利者”
                    //（最近的 transform）为
                    // 我们刚刚找到的 transform
                    closest = TempTrans;

                    // 存储此路点的
                    // 索引
                    TempIndex=i;

                    // 设置我们的“胜利”距离
                    // 为刚刚找到的距离
                    // 
                    distance = curDistance;
                }
            }
        }
        return TempIndex;
    }
    
    private int TempIndex;
}
```
