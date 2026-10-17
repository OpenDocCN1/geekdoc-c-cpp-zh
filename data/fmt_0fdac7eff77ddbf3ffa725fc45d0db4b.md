
### 3. 此脚本的 `WeaponControl` 是一个 `BaseWeapon` 类类型，而不是槽位武器系统。做出这一决定是为了让《Metal Vehicle Doom》能够留出通过槽位系统接收可切换武器，而本游戏只需要一个不需要切换的单炮塔。

### 4. 没有进行路点检查或反向方向检查。

### 5. 当玩家重生时，它将使用原始起始点的位置和旋转角度。

### 6. 当处于无敌状态时，会显示护盾网格（一个包裹在玩家周围的球体）。

除了本节开头强调的差异外，它与第 12 章中的汽车控制脚本非常相似。

请注意，本游戏的转向由 `BaseAIController` 的 `TurnTowardTarget()` 函数处理，用于寻找并朝目标。它没有使用任何水平输入。由于它使用 `TurnTowardTarget()` 函数进行转向，坦克的转弯速度由 `AIController` 上的变量 `modelRotateSpeed` 的值决定。

## 13.8 基于标签设置 AI 追逐

该系统被设计为锁定并追逐特定的目标。本游戏中的坦克需要这种更动态的行为，即某种能够自行筛选目标的寻找系统。`SetAIChaseTargetBasedOnTag` 脚本充当添加到 AI 对象上的一个组件，它将利用 Unity 系统找到所有带有特定标签的对象，检查它们的距离，并选择最近的一个作为 `AIController` 组件的使用目标。

脚本内容：

```csharp
using UnityEngine;
using System.Collections;
using AIStates;
public class SetAIChaseTargetBasedOnTag : MonoBehaviour
{
    public BaseAIController AIComponent;
    public string defaultTagFilter= "enemy";
    public bool checkForWalls;
    public LayerMask raycastWallMask;
    public float chaseDistance;
    private GameObject myGO;
    private Transform myTransform;
    private GameObject tempGO;
    private RaycastHit hit;
    private Vector3 tempDirVec;
    private bool foundTarget;
    public float visionHeightOffset= 1f;
    void Start ()
    {
        // first, let's try to get the AI control script
        // automatically
        AIControlComponent = GetComponent<BaseAIController>();
        myGO = gameObject;
        myTransform = transform;
        // quick check, to warn us if something goes wrong
        if ( AIControlComponent == null )
        {
            Debug.LogWarning("SetAIChaseTargetBasedOnTag cannot
            find BaseAIController");
        }
        InvokeRepeating("LookForChaseTarget", 1.5f, 1.5f);
    }
    void LookForChaseTarget ()
    {
        // null check
        if (AIControlComponent == null)
            return;
        GameObject[] gos = GameObject.FindObjectsWithTag
        ( defaultTagFilter );
        // Iterate through them
        foreach ( GameObject go in gos )
        {
            if (go!= myGO ) // make sure we're not comparing
            // ourselves to ourselves
            {
                float aDist = = Vector3.Distance(myGO.transform.position,
                go.transform.position,)
                if(checkForWalls )
                {
                    // wall check required
                    if(CanSee(go.transform)==true)
                        AIControlComponent.SetChaseTarget(go.transform);
                        foundTarget=true;
                } else {
                    // no wall check required! go ahead
                    // and find something to chase!
                    if(aDist<distance )
                    {
                        // tell our AI controller to
                        // chase this target
                        AIControlComponent.SetChaseTarget(go.transform);
                        foundTarget=true;
                    }
                }
            }
            if( foundTarget==false )
            {
              // clear target
              AIControl.SetChaseTarget( null );
              // change AI state
              AIControl.SetAIState(AIState.moving_looking_
              for (_target) );
            }
        }
    }
    public bool CanSee( Transform aTarget ) {
      // first, let's get a vector to use for raycasting by
      // subtracting the target position from our AI position
      tempDirVec:Vector3.Normalize(aTarget.position -
      myTransform.position);
      // let's have a debug line to check the distance between the
      // two manually, in case you run into trouble!
      Debug.DrawLine(myTransform.position, aTarget.position);
      // cast a ray from our AI, out toward the target passed in
      // (use the tempDirVec magnitude as the distance to cast)
      if (Physics.Raycast(myTransform.position +
      ( visionHeightOffset * myTransform.up), tempDirVec, out hit,
      chaseDistance) {
        // check to see if we hit the target
        if (hit.transform.gameObject == aTarget.gameObject) {
          return true;
        }
      }
      // nothing found, so return false
      return false;
    }
}
```

### 13.8.1 脚本解析

此脚本将利用 `MonoBehavior` 提供的一些功能，这也是它源自那里：

```csharp
using UnityEngine;
using System.Collections;
```

`AIStates` 命名空间被此脚本用于方便更容易访问 `AIStates` 枚举：

```csharp
using AIStates;
```

```csharp
public class SetAIChaseTargetBasedOnTag : MonoBehavior {
}
```

`Start()` 从获取 AI 控制器的引用开始。接下来，缓存了 `gameObject` 和 `transform` 的引用，并进行了快速检查以确保我们拥有 AI 控制器。脚本的主要部分位于 `LookForChaseTarget()` 内部，但这不是我们每帧都需要执行的操作。相反，`InvokeRepeating` 调用每 1.5 秒执行一次。为了寻找另一个目标，需要获取所有带标签对象的引用并放入数组。`defaultTagFilter` 变量实际上只是包含 `"enemy"` 单词的字符串。`foreach` 循环遍历数组 `gos` 中的每个 `gameObject`，该数组持有 `FindObjectsWithTag()` 返回的所有带标签的对象：当然，让这个 `gameObject` 追逐自己是没有意义的，为了避免这种情况，快速检查 `go!=myGO`。要检查这是否是一个可行的目标，过程是使用 `Vector3.Distance(myGO` 的 `transform` 位置（此玩家）和 `go` 的 `transform` 位置（循环中拾取的最近 `GameObject`）` 进行简单的距离检查。当不需要墙检查时，将 `aDist` 与 `chaseDistance` 比较，以查看循环设置的目标是否足够近可以追逐。AI 控制器现在需要目标循环中的当前 `gameObject`，通过 `BaseAuthController.SetChaseTarget` 传递给它。我们需要跟踪是否已找到目标，以便在没有合适目标出现时，调整 AI 行为：

在这里，如果变量 `foundTarget` 为 `false`，我们知道通过之前的距离检查没有找到目标。如果没有找到目标，则需要清除当前的追逐目标，并将 AI 控制器状态切换回 `moving_looking_for_target` 阶段：

```cs
if( foundTarget==false )
// clear target
AIControlComponent.SetChaseTarget( null );
```

在将追逐目标设置为 `null` 后，我们将 `AIState` 设置为 `AIState.moving_looking_for_target`，以确保即使目标被设置为 `null`，AI 也会移动：

```cs
// change AI state
AIControlComponent.SetAIState( AIState.moving_looking_for_target );
```

`CanSee()` 的代码与 `BaseAIController.cs` 中内置的 `CanSee()` 函数几乎完全相同。请查看第 9 章中的分解以获取关于该函数工作原理的描述：

```cs
public bool CanSee( Transform aTarget )
{
    // 首先，我们通过从 AI 位置中减去目标位置，
    // 来获取一个用于射线检测的向量
tempDirVec= Vector3.Normalize(aTarget.position - myTransform.position);
    // 让我们画一条调试线来手动检查
    // 两个之间的距离，以防你遇到麻烦！
    Debug.Drawline(myTransform.position, aTarget.position);
    // 从我们的 AI 向传入的目标方向投射出一条射线
    //（使用 tempDirVec 的幅度作为投射的距离）
    if( Physics.Raycast(myTransform.position + visionHeight * myTransform.up ), tempDirVec, out hit, chaseDistance )
    {
        // 检查是否击中了目标
        if( hit.transform.gameObject == aTarget.gameObject )
        {
            return true;
        }
    }
    // 什么都没有找到，所以返回 false
    return false;
}
```
