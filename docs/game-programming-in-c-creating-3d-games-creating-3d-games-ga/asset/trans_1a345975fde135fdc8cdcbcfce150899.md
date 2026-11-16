

## 练习 8.2

为动作添加基本输入映射支持。为此，创建一种文本文件格式，将动作映射到设备及其上的按钮/键。例如，该文本文件中用于指定“Fire”动作对应控制器 A 按钮的条目可能如下所示：

```
Fire,Controller,A
```

然后在 `InputSystem` 中解析此数据并将其保存到映射中。接着，向 `InputState` 添加一个名为 `GetMappedButtonState` 的通用函数，该函数接受动作名称并从正确的设备返回 `ButtonState`。该函数的签名大致如下：

**单击此处查看代码图像**

```
ButtonState GetMappedButtonState(const std::string& a
```

## 第 9 章

## 摄像机

摄像机决定了玩家在 3D 游戏世界中的视角，并且有多种不同类型的摄像机。本章介绍四种摄像机的实现：第一人称摄像机、跟随摄像机、环绕摄像机以及沿路径移动的样条摄像机。由于摄像机通常决定玩家角色的移动，本章还介绍如何为不同类型的摄像机更新移动代码。

### 第一人称摄像机

**第一人称摄像机**从角色在世界中移动的视角展示游戏世界。这种摄像机在第一人称射击游戏（如 *Overwatch*）中很受欢迎，也用于一些角色扮演游戏（如 *Skyrim*）或叙事驱动型游戏（如 *Gone Home*）。一些设计师认为，第一人称摄像机是视频游戏中最具沉浸感的摄像机类型。

尽管很容易将摄像机视为单纯的视图，但摄像机也会告知玩家角色如何在世界中移动。这意味着摄像机和移动系统的实现相互依赖。PC 上第一人称射击游戏的典型控制方式同时使用键盘和鼠标。W/S 键用于前后移动，而 A/D 键 **侧移** 角色（即向左和向右移动）。左右移动鼠标会围绕上轴旋转角色，而上下移动鼠标只会俯仰视图，*不会*俯仰角色。

### 基本第一人称移动

实现移动比处理视图更容易，因此这是一个很好的起点。你创建一个名为 `FPSActor` 的新角色，用于实现第一人称移动。MoveComponent 中的前后移动基于第 6 章“3D 图形”中所做的更改，已在 3D 世界中正常工作。实现侧移只需进行少量更新。首先，在 Actor 中创建一个名为 GetRight 的函数，它类似于 GetForward（只是使用 y 轴而不是其他轴）：

**单击此处查看代码图像**

```
Vector3 Actor::GetRight() const
{
    // Rotate right axis using quaternion rotation
    return Vector3::Transform(Vector3::UnitY, mRotation
}
```

接下来，在 MoveComponent 中添加一个名为 mStrafeSpeed 的新变量，它影响角色侧移的速度。在 Update 中，你只需使用角色的右向量根据侧移速度调整位置：

**单击此处查看代码图像**

```
if (!Math::NearZero(mForwardSpeed) || !Math::NearZero
{
    Vector3 pos = mOwner->GetPosition();
    pos += mOwner->GetForward() * mForwardSpeed * delt
// Update position based on strafe
pos += mOwner->GetRight() * mStrafeSpeed * deltaTime
mOwner->SetPosition(pos);
}
```

然后在 `FPSActor::ActorInput` 中，你可以检测 A/D 键并根据需要调整侧移速度。现在角色可以使用标准的第一人称 WASD 控件进行移动。

左右旋转已通过角速度在 `MoveComponent` 中存在。因此，下一项任务是将鼠标左右移动转换为角速度。首先，游戏需要通过 `SDL_RelativeMouseMode` 启用相对鼠标模式。回顾第 8 章“输入系统”，相对鼠标模式报告每帧 (x, y) 值的变化，而不是绝对 (x, y) 坐标。（注意，在本章中，你将直接使用 SDL 输入函数，而不是第 8 章中创建的输入系统。）

将相对 x 移动转换为角速度只需进行少量计算，如清单 9.1 所示。首先，`SDL_GetRelativeMouseState` 检索 (x, y) 运动。`maxMouseSpeed` 常量是每帧可能的最大相对运动量，尽管这可能是一个游戏内设置。同样，`maxAngularSpeed` 将运动转换为每秒旋转量。然后，你取报告的 x 值，除以 maxMouseSpeed，再乘以 maxAngularSpeed。这将产生一个发送到 MoveComponent 的角速度。

### 清单 9.1 来自鼠标的 FPS 角速度计算

**单击此处查看代码图像**

```
// Get relative movement from SDL

int x, y;

Uint32 buttons = SDL_GetRelativeMouseState(&x, &y);

// Assume mouse movement is usually between -500 and
const int maxMouseSpeed = 500;

// Rotation/sec at maximum speed
const float maxAngularSpeed = Math::Pi * 8;

float angularSpeed = 0.0f;

if (x != 0)
{
    // Convert to approximately [-1.0, 1.0]

    angularSpeed = static_cast<float>(x) / maxMouseSpe
    // Multiply by rotation/sec

    angularSpeed *= maxAngularSpeed;
}
mMoveComp->SetAngularSpeed(angularSpeed);
```

### 摄像机（无俯仰）

实现摄像机的第一步是创建一个名为 CameraComponent 的 Component 子类。本章中所有不同类型的摄像机都将从 CameraComponent 继承，因此任何通用摄像机功能都可以放入这个新组件中。CameraComponent 的声明与任何其他组件子类类似。目前，唯一的新函数是一个名为 SetViewMatrix 的受保护函数，它只是将视图矩阵转发给渲染器和音频系统：

**单击此处查看代码图像**

```
void CameraComponent::SetViewMatrix(const Matrix4& view
{
 // Pass view matrix to renderer and audio system
 Game* game = mOwner->GetGame();
 game->GetRenderer()->SetViewMatrix(view);
 game->GetAudioSystem()->SetListener(view);
}
```

具体到 FPS 摄像机，你创建一个名为 FPSCamera 的 CameraComponent 子类，其中包含一个重写的 Update 函数。清单 9.2 显示了 Update 的代码。目前，Update 使用与第 6 章中介绍的基本摄像机角色相同的逻辑。摄像机位置是拥有者角色的位置，目标点是拥有者角色前向方向上的一个任意点，上向量是 z 轴。最后，Matrix4::CreateLookAt 创建视图矩阵。

### 清单 9.2 FPSCamera::Update 实现（无俯仰）

**单击此处查看代码图像**

```
void FPSCamera::Update(float deltaTime)
{

 // Camera position is owner position
 Vector3 cameraPos = mOwner->GetPosition();

 // Target position 100 units in front of owner
 Vector3 target = cameraPos + mOwner->GetForward()

 // Up is just unit z
 Vector3 up = Vector3::UnitZ;

 // Create look at matrix, set as view
 Matrix4 view = Matrix4::CreateLookAt(cameraPos, ta

 SetViewMatrix(view);

}
```

### 添加俯仰

回顾第 6 章，偏航是围绕上轴的旋转，俯仰是围绕侧轴的旋转（在此例中为右轴）。将俯仰纳入 FPS 摄像机需要进行一些更改。摄像机仍然从拥有者角色的前向量开始，但你应用额外的旋转以考虑俯仰。然后，你从这个视图前向量推导出目标。要实现这一点，你向 FPSCamera 添加三个新的成员变量：

**单击此处查看代码图像**

```
// Rotation/sec speed of pitch

float mPitchSpeed;

// Maximum pitch deviation from forward

float mMaxPitch;

// Current pitch

float mPitch;
```

mPitch 变量表示摄像机当前的（绝对）俯仰，而 mPitchSpeed 是俯仰方向当前的每秒旋转量。最后，mMaxPitch 变量是俯仰相对于前向量在任一方向上可偏差的最大值。大多数

