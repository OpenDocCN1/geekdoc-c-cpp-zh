

当摇杆处于静止状态时，摇杆x轴和y轴报告的值为零。但实际上，这些值通常在零附近，但很少精确为零。相反，如果玩家将摇杆完全向右推，摇杆x轴报告的值将接近最大值，但很少精确等于最大值。

这对游戏来说有两个方面的问题。首先，它可能导致**幻象输入**，即玩家没有触碰任何输入轴，但游戏却报告有事情发生。例如，假设玩家将控制器完全放在桌面上。玩家理应期望游戏中的角色不会移动。但是，如果未处理此问题，游戏会检测到轴上的某个输入值并移动角色。

此外，许多游戏会根据模拟摇杆在某个方向移动的距离来控制角色移动——因此轻微移动摇杆可能会导致角色缓慢行走，而将摇杆完全向某个方向移动可能会导致角色冲刺。但是，如果你仅在轴报告最大值时才让玩家冲刺，玩家将永远无法冲刺。

要解决此问题，处理轴输入的代码应**过滤**该值。具体来说，你希望将接近零的值解释为零，将接近最小值或最大值的值解释为最小值或最大值。此外，如果将整数范围转换为归一化的浮点范围，输入系统的用户会觉得更方便。对于同时产生正值和负值的轴，这意味着范围在−1.0到1.0之间。

图8.2展示了单轴上此类过滤器的示例。线上方的数字是过滤前的整数值，线下方的数字是过滤后的浮点值。你将其解释为0.0的零附近区域称为**死区**。

![](img/e9afcec1487716b0ef80d7e7c09869c8_579_0.png)

**图8.2** 轴的示例过滤器，输入值在上方，输出值在下方

清单8.7展示了`InputSystem::Filter1D`函数的实现，输入系统使用该函数来过滤一维轴（例如扳机）。首先，你为死区和最大值声明两个常量。请注意，此处的`deadZone`为`250`——这小于**图8.2**中的值，因为该值对扳机效果更好（但如果需要，你可以将常量设为参数或用户可配置项）。

接下来，代码使用三元运算符获取输入的绝对值。如果该值小于死区常量，则直接返回`0.0f`。否则，你将输入转换为一个比例值，表示其在死区和最大值之间的位置。例如，介于deadZone和maxValue中间的输入为0.5f。

然后，你确保该比例值的符号与原始输入的符号匹配。最后，你将值限制在-1.0到1.0的范围内，以处理输入大于最大值常量的情况。`Math::Clamp`的实现位于自定义的`Math.h`头文件中。

### 清单8.7 Filter1D实现

单击此处查看代码图像

```
float InputSystem::Filter1D(int input)
{
    // A value < dead zone is interpreted as 0%
    const int deadZone = 250;
    // A value > max value is interpreted as 100%
    const int maxValue = 30000;
    float retVal = 0.0f;
    // Take absolute value of input
    int absValue = input > 0 ? input : -input;
    // Ignore input within dead zone
    if (absValue > deadZone)
    {
        // Compute fractional value between dead zone and max
        retVal = static_cast<float>(absValue - deadZone) / (maxValue - deadZone);

        // Make sure sign matches original value
        retVal = input > 0 ? retVal : -1.0f * retVal;

        // Clamp between -1.0f and 1.0f
        retVal = Math::Clamp(retVal, -1.0f, 1.0f);
    }

    return retVal;
}
```

使用`Filter1D`函数，输入值5000返回0.0f，值-19000返回-0.5f。

`Filter1D`函数在只需要单个轴（例如其中一个扳机）时效果良好。但是，由于模拟摇杆实际上是两个协同工作的不同轴，通常更倾向于将其以二维方式过滤，如下一节所述。

目前，你可以向`ControllerState`添加两个浮点数，分别用于左扳机和右扳机：

```
float mLeftTrigger;
float mRightTrigger;
```

接下来，在`InputSystem::Update`中使用`SDL_GameControllerGetAxis`函数读取两个扳机的值，并对该值调用`Filter1D`函数将其转换为0.0到1.0的范围（因为扳机不能为负值）。例如，以下代码设置`mLeftTrigger`成员：

单击此处查看代码图像

```
mState.Controller.mLeftTrigger =
    Filter1D(SDL_GameControllerGetAxis(mController,
        SDL_CONTROLLER_AXIS_TRIGGERLEFT));
```

然后，你添加`GetLeftTrigger()`和`GetRightTrigger()`函数来访问这些值。例如，以下代码获取左扳机的值：

单击此处查看代码图像

```
float left = state.Controller.GetLeftTrigger();
```

## 以二维方式过滤模拟摇杆

模拟摇杆的常见控制方案是：摇杆的方向对应于玩家角色移动的方向。例如，将摇杆向上并向左按下会导致屏幕上的角色也向该方向移动。要实现此功能，你应该共同解释x轴和y轴。

虽然将Filter1D函数独立应用于x轴和y轴很诱人，但这样做可能会引发一个有趣的问题。如果玩家将摇杆完全向上移动，将其解释为归一化向量会得到<0.0, 1.0>。另一方面，如果玩家将摇杆完全向上并向右移动，归一化向量为<1.0, 1.0>。这两个向量的长度不同，如果你使用长度来决定角色移动速度，这就成了一个问题：角色沿对角线移动可能比沿单一方向直线移动更快！

虽然你可以简单地将长度大于一的向量归一化，但独立解释每个轴最终仍意味着你将死区和最大值解释为一个正方形。更好的方法是将其解释为同心圆，如图8.3所示。正方形边框表示原始输入值，内圆表示死区，外圆表示最大值。

![](img/e9afcec1487716b0ef80d7e7c09869c8_584_0.png)

图8.3 二维过滤

清单8.8给出了Filter2D的代码，它接收模拟摇杆的x轴和y轴，并以二维方式进行过滤。你首先创建一个2D向量，然后确定该向量的长度。长度小于死区会导致Vector2::Zero。对于大于死区的长度，你确定死区和最大值之间的比例值，并将向量的长度设置为该比例值。

### 清单8.8 InputSystem::Filter2D实现

单击此处查看代码图像

```
Vector2 InputSystem::Filter2D(int inputX, int inputY)
{
    const float deadZone = 8000.0f;
    const float maxValue = 30000.0f;

    // Make into 2D vector
    Vector2 dir;

    dir.x = static_cast<float>(inputX);
    dir.y = static_cast<float>(inputY);

    float length = dir.Length();

    // If length < deadZone, should be no input
    if (length < deadZone)
    {
        dir = Vector2::Zero;
    }

    else
    {
        // Calculate fractional value between
        // dead zone and max value circles

        float f = (length - deadZone) / (maxValue - deadZone);

        // Clamp f between 0.0f and 1.0f
        f = Math::Clamp(f, 0.0f, 1.0f);
        // Normalize the vector, and then scale it to the
        // fractional value
        dir *= f / length;
    }
    return dir;
}
```

接下来，分别向ControllerState添加两个Vector2，分别用于左摇杆和右摇杆。然后，你可以在InputSystem::Update中添加代码来获取每个摇杆的两个轴值，然后运行Filter2D以获得最终的模拟摇杆值。例如，以下代码过滤左摇杆并将结果保存在控制器状态中：

单击此处查看代码图像

```
x = SDL_GameControllerGetAxis(mController,
SDL_CONTROLLER_AXIS_LEFTX);
y = -SDL_GameControllerGetAxis(mController,
SDL_CONTROLLER_AXIS_LEFTY);
```

