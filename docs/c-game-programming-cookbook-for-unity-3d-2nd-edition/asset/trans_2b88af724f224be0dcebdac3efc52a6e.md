
moveSpeed 在函数中更早时就被使用，但它只在这里计算，因为它依赖于 targetSpeed 和 curSmooth 已被计算出来。moveSpeed 是使用 Mathf.Lerp 在其当前值和变量 targetSpeed 之间进行插值的结果，插值量由 curSmooth 设置。

当 moveSpeed 降至 walkSpeed 设定的阈值以下（即当玩家释放移动输入以减慢移动时）walkTimeStart 会重置为 Time.time，以便在玩家下次移动时允许再次开始行走。

UpdateDirectionalMovement() 函数的最后一部分处理移动方向：

```csharp
// Calculate actual motion
Vector3 movement = moveDirection * moveSpeed;
movement *= Time.deltaTime;

// Move the controller
collisionFlags = _charController.Move(movement);
```

变量 movement 取 moveDirection 并乘以 moveSpeed，然后在下一行结果乘以 Time.deltaTime，以提供一个基于时间的移动向量，其大小适合传入角色控制器。当控制器被告知 Move（将移动向量作为参数传入）时，它会返回一个名为 CollisionFlags 的位掩码。当与角色控制器发生碰撞时，collisionFlags 变量可用于判断碰撞发生的位置；collisionFlags 掩码表示 None、Sides、Above 或 Below。虽然在 BaseTopDown.cs 的此版本中未使用碰撞数据，但它已为未来功能实现。

```csharp
// Set rotation to the move direction
_TR.rotation = Quaternion.LookRotation(moveDirection);
}
```

在上面的函数最后一行，Quaternion.LookRotation 创建一个朝向 moveDirection 的旋转并将其设置为 _TR.rotation——使玩家面向移动的正确方向。

```csharp
void UpdateRotationMovement()
{
    _TR.Rotate(0, horz * rotateSpeed * Time.deltaTime, 0);
}
```

此类第二种移动类型是旋转。UpdateRotationMovement() 使用 Transform.Rotate 和角色控制器的 SimpleMove 函数的组合，提供一个控制系统，使玩家绕其 y 轴旋转并沿其 z 轴移动（对于人形角色，这就是前后行走或奔跑）。

对于水平输入，变量 horz 乘以变量 rotateSpeed 并乘以 Time.deltaTime，用作玩家绕其 y 轴旋转的旋转。垂直输入（存储在 vert 中）接下来处理，因为 vert 乘以 moveSpeed 构成了在玩家 z 轴上移动的速度。

请注意 moveSpeed 在函数中更下方计算，因此暂时不必担心——只需记住 moveSpeed 是期望的移动速度：

```csharp
curSpeed = moveSpeed * vert;
```

CharacterController.SimpleMove 移动角色控制器；考虑传入向量的速度。在此行中，提供给 SimpleMove 的向量是玩家的前向向量乘以 curSpeed：

```csharp
_charController.SimpleMove( _TR.forward * curSpeed );
```

targetDirection 是一个 Vector3 类型变量，根据 vert 输入变量确定我们希望移动多少；即使其向量仅在函数后面的计算其大小时使用：

```csharp
// Target direction (the max we want to move, used for calculating target speed)
targetDirection = vert * _TR.forward;
```

当速度变化时，而不是瞬间将动画从慢变快，变量 curSmooth 用于平滑过渡速度。变量 speedSmoothing 旨在在 Unity 检查器窗口中设置，然后乘以 Time.deltaTime 使速度过渡基于时间：

```csharp
// Smooth the speed based on the current target direction
float curSmooth = speedSmoothing * Time.deltaTime;
```

脚本的下一行将 targetSpeed 限制为 1。取之前的 targetDirection 向量，targetSpeed 的最大值是 1，或者如果小于 1，则为 targetDirection.magnitude 持有值：

```csharp
// Choose target speed
// We want to support analog input but make sure you can't walk faster diagonally than just forward or sideways
targetSpeed = Mathf.Min(targetDirection.magnitude, 1.0f);
```

函数的其余部分以与本节前面 UpdateDirectionalMovement() 函数相同的方式在行走和奔跑之间过渡：

```csharp
// adjust move speed
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

上面，我们再次将 targetSpeed 改为 runSpeed 或 walkSpeed。moveSpeed 在当前速度和 targetSpeed 之间插值，并且有一个检查以查看 moveSpeed 变量是否降至 walkSpeed 的三分之一以下，以告知我们玩家移动得如此缓慢以至于我们可以重置 walkTimeStart。

接下来是 Update() 函数：

```csharp
public void Update()
{
    ApplyGravity();

    if (!canControl)
    {
        // kill all inputs if not controllable.
        Input.ResetInputAxes();
    }
    UpdateSmoothedMovementDirection();
}
```

上面，Update() 以调用停止输入开始，当 canControl 设置为 false 时。更重要的是，这旨在在游戏结束时将 canControl 设置为使玩家停止。当游戏结束时，而不是输入继续并让玩家在游戏结束消息后面到处跑，输入被设置为零。

UpdateSmoothedMovementDirection() 根据布尔变量 moveDirectionally 的值调用两个移动更新脚本之一。

```csharp
void ApplyGravity()
{
    // apply some gravity to the character
    float gravity = -9.8f * Time.deltaTime;
    _charController.Move(new Vector3(0, gravity, 0));
}
```

上面，我们将重力应用于角色控制器——默认情况下，Unity 不会向此类对象添加重力。我们只需调用 Move() 并传入重力方向的 Vector3 即可实现。

在类的末尾，GetSpeed()、GetDirection() 和 IsMoving() 是为其他脚本提供的实用函数，以便访问角色的一些属性：

```csharp
public float GetSpeed ()
{
    return moveSpeed;
}
public Vector3 GetDirection ()
{
    return moveDirection;
}
public bool IsMoving ()
{
    return (Mathf.Abs(vert) + Mathf.Abs(horz) > 0.5f);
}
```

GetSpeed() 和 GetDirection() 返回其关联变量。IsMoving() 取 vert 和 horz 的绝对值，以判断玩家是否移动速度超过 0.5f。

## 6.2 轮式车辆

BaseWheeledVehicle.cs 脚本依赖于 Unity 内置的 WheelCollider 系统之一。WheelCollider 组件被添加到位于支撑汽车车身的车轮位置的 GameObjects 中。WheelCollider 组件本身没有任何视觉形式，并且表示车轮的网格不会自动对齐。WheelColliders 是物理模拟；它们负责物理动作，例如悬挂和车轮摩擦。

摩擦系统背后的数学超出了本书的范围，尽管 Unity 文档在在线帮助的 WheelCollider 页面上涵盖了该主题。

BaseWheeledVehicle 使用四个 WheelColliders 进行驱动，车轮网格的朝向由本章后面解释的名为 BaseWheelAlignment.cs 的脚本处理。

该类派生自 ExtendedCustomMonoBehaviour（本书第 4 章讨论过），它添加了一些常用变量。

BaseWheeledVehicle.cs 开始如下：

```csharp
using UnityEngine;
namespace GPC
{
    [AddComponentMenu("CSharpBookCode/Base/Vehicles/Wheeled Vehicle Controller")]
    [RequireComponent(typeof(Rigidbody))]
}
```

上面，我们以通常的 UnityEngine 引用开始类，然后为此组件添加菜单项。在附加此脚本的同一 GameObject 上拥有 Rigidbody 组件很重要。下一个标签（用方括号括起来的行是 Unity 所称的标签）是 RequireComponent。这将检查 Rigidbody 是否附加到我们的 GameObject，如果需要则添加一个。然后我们设置所有框架所在的命名空间，我们的 GPC 命名空间。

现在进入类：

```csharp
public class BaseWheeledVehicle : ExtendedCustomMonoBehaviour
{
    public bool isLocked;
    [Header("Wheel Colliders")]
    public WheelCollider _frontWheelLeft;
    public WheelCollider _frontWheelRight;
    public WheelCollider _rearWheelLeft;
    public WheelCollider _rearWheelRight;
}
```

我们使用名为 isLocked 的布尔变量来固定车辆。在示例游戏中，这用于在游戏开始时 3、2、1 倒计时完成之前阻止玩家开车离开。

每个 WheelCollider 变量都根据其预期位置命名；frontWheelLeft、frontWheelRight、rearWheelLeft 和 rearWheelRight。为了脚本正常运行，WheelColliders 需要在车辆脚本的 Unity 检查器窗口中被引用（拖放）到正确的变量中。

```csharp
public BaseInputController _inputController;
```

默认输入系统设置为使用本书框架中的 BaseInputController 类。当然，你可以随意更换输入。我们使用 _inputController 变量与 BaseInputController 通信，并在每次更新时了解输入的情况，这发生在该类的更下方，在 GetInputs() 函数中。

```csharp
[Header("Steer settings")]
public float steerMax = 30f;
public float accelMax = 5000f;
public float brakeMax = 5000f;
```
