
GetTime() 只是返回变量 currentTime 的值，这样你就可以在另一个脚本中处理格式化或后续处理。

### 5.10.7.1 修改计时器以自动更新

如果你希望使用它并让计时器自动更新，可以修改类声明：

```csharp
public class TimerClass
```

让该类继承自 MonoBehaviour：

```csharp
public class TimerClass : MonoBehaviour
```

然后，将 UpdateTimer() 函数的名称改为 Update()，引擎会在每一帧自动调用它。

### 5.10.8 WaypointsController

这个脚本非常庞大且重要，因此单独用一章来介绍！请查看第 8 章，了解这个脚本如何组合在一起，以及如何在你自己的游戏中使用它。

## 5.11 武器

Weapons 文件夹中有四个脚本：AutoShooter.cs、ProjectileController.cs、StandardSlotWeaponController.cs 和 ThreeWayShooter.cs。这些脚本以及武器系统的使用方法将在本书第 7 章中完整介绍。

```csharp
charController = GetComponent<CharacterController>();
GetComponents();

_RB = GetComponent<Rigidbody>();
_inputController = GetComponent<BaseInputController>();
}
```

在上面的代码中，moveDirection 是一个 Vector3，脚本后面会用它来告诉角色控制器向哪个方向移动。在 Init() 函数中，它被赋予世界坐标的前向向量作为默认值。

随后，Init() 调用 GetComponents()，这是 ExtendedCustomMonoBehaviour.cs（本类派生自该类）中的一个函数，它会获取对此脚本所附加到的 Transform 和 GameObject 的引用。我们还获取 Rigidbody（因为此脚本依赖物理系统工作），并将其引用存储在变量 _RB 中。_inputController 会填充一个对 BaseInputController 组件（或派生自 BaseInputController 的组件）的引用，以便我们可以处理来自用户的输入。

BaseInputController 类用于提供来自玩家的输入，以移动角色，并且应作为组件附加到与此脚本相同的 GameObject 上。BaseInputController.cs 作为本书框架的一部分提供。你可以使用此脚本处理输入，也可以将输入系统替换为你需要的任何系统，只要将名为 horz 和 vert 的变量分别传入作为浮点数的水平和垂直输入值即可。

```csharp
public void SetUserInput( bool setInput )
{
    canControl = setInput;
}
```

在上面的代码中，SetUserInput() 函数用于设置变量 canControl，该变量用于检查是否应禁用用户输入。这只是一种更优雅的方式，允许其他脚本启用或禁用用户输入。

将输入分离到单个 GetInput() 函数中，应该可以在需要时轻松自定义输入。接下来，我们处理在 GetInput() 函数中调用以更新输入：

```csharp
public virtual void GetInput()
{
    if (isFinished || isRespawning || !canControl)
    {
        horz = 0;
        vert = 0;
        return;
    }
```

在上面的代码中，GetInput() 的开头会检查我们是否应该控制玩家。如果不是，则角色控制器的水平和垂直输入会被锁定为零，并退出此函数。否则，我们需要从 BaseInputController 组件获取输入：

```csharp
    if (!canControl)
        return;

    horz = _inputController.GetHorizontal();
    vert = _inputController.GetVertical();
}
```

在上面的代码中，在获取用户输入之前，我们要确保 canControl 为 true——这意味着用户可以控制它——如果不是这种情况就退出。本书中的输入脚本会返回正确范围内的值，因此我们只需调用函数，将输入值返回到 horz 和 vert 中。

```csharp
public virtual void LateUpdate()
{
    if (canControl)
        GetInput();
}
```

LateUpdate() 用于通过 GetInput() 脚本请求更新输入布尔变量。Unity 建议将 LateUpdate 作为检查键盘输入的最佳位置，因为此时引擎已经完成了自身的输入更新。

```csharp
void UpdateSmoothedMovementDirection()
{
    if (moveDirectionally)
        UpdateDirectionalMovement();
    else
        UpdateRotationMovement();
}
```

通过将 moveDirectionally 设置为 true 或 false，此脚本既可以进行方向移动，也可以进行旋转移动。每当 moveDirectionally 设置为 false 时，按下左键或右键会使玩家绕其 y 轴向左或向右旋转。按下上键会沿玩家的 z 轴向前行走，按下下键会向后移动。

在 UpdateSmoothedMovementDirection() 脚本中，会检查 moveDirectionally 变量，以确定调用哪种类型的移动函数来更新玩家移动：

移动类型分为两个独立的函数，上面的代码会根据 moveDirectionally 的状态调用它们。

```csharp
void UpdateDirectionalMovement()
{
    // find target direction
    targetDirection = horz * Vector3.right;
    targetDirection += vert * Vector3.forward;
}
```

方向移动使用世界坐标的 x 轴和 z 轴来决定移动方向；也就是说，玩家会根据所按的按钮沿世界坐标的 x 轴或 z 轴移动。在上面的代码中，UpdateDirectionalMovement() 函数首先获取用户的水平和垂直输入（来自变量 horz 和 vert），并将它们分别乘以一个向量，该向量指向我们希望 horz 或 vert 影响的轴。targetDirection 变量是一个 Vector3，它将垂直和水平移动合并为一个表示玩家移动方向的向量。

当没有用户输入时，targetDirection 变量将为零，因此在计算任何移动量之前，我们先检查是否打算移动：

```csharp
if (targetDirection != Vector3.zero)
{
    moveDirection = Vector3.RotateTowards(moveDirection, targetDirection, rotateSpeed * Mathf.Deg2Rad * Time.deltaTime, 1000);
    moveDirection = moveDirection.normalized;
}
```

在上面的代码中，moveDirection 将用于移动玩家。它的值来自当前 moveDirection 值与先前根据用户输入计算出的 targetDirection 之间的插值。然后将该向量乘以 rotateSpeed，再转换为弧度，并再次乘以 Time.deltaTime，使旋转基于时间。Vector3.RotateTowards 用于完成转向，可确保旋转最终停在指定的精确位置。

然后对 moveDirection 向量进行归一化，以消除向量长度的影响。

BasePlayerCharacterController 类的下一部分处理速度：

```csharp
// Smooth the speed based on the current target direction
curSmooth = speedSmoothing * Time.deltaTime;
```

变量 curSmooth 将在脚本后面使用，用于决定玩家的移动速度从零增加到最大速度需要多长时间。

```csharp
// Choose target speed
// We want to support analog input but make sure you can't walk faster diagonally than just forward or sideways
targetSpeed = Mathf.Min(targetDirection.magnitude, 1.0f);
```

变量 targetSpeed 的上限为 1。为此，将 targetDirection 的大小和 1 传给 Mathf.Min。其中较小的值将赋给 targetSpeed。

此脚本允许两种移动状态：奔跑和行走。奔跑与行走之间的切换是计时的——角色会开始行走并继续行走，直到垂直输入持续的时间（以秒为单位）超过 runAfterSeconds 的值。

```csharp
if (Time.time - runAfterSeconds > walkTimeStart)
{
    targetSpeed *= runSpeed;
}
else
{
    targetSpeed *= walkSpeed;
}
moveSpeed = Mathf.Lerp(moveSpeed, targetSpeed, curSmooth);
// Reset walk time start when we slow down
if (moveSpeed < walkSpeed * 0.3f)
    walkTimeStart = Time.time;
```

上面的代码使用 Time.time 来跟踪玩家已经行走了多长时间，这意味着 Time.timeScale 会影响它（如果游戏暂停或时间被缩放，此计时仍将相对于时间缩放）。

当玩家处于行走状态时，walkSpeed 是 targetSpeed 的乘数：
