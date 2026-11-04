
- 18. 询问玩家是否想再玩一次：记住，良好的游戏循环应始终允许玩家选择再玩一次。
- 19. 结束或重复游戏：在我们的情况下，结束游戏循环意味着结束游戏并返回菜单部分。这允许用户退出程序，或继续进入另一个游戏。

### 示例 3.44. 八个移动方向。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_209_0.png)

## 设置编译器

此时，我们需要让编译器启动并运行起来；重复用于链接类基类及其所有对应部分的步骤。如果你更愿意使用 chapter3\project2，可以直接加载它；但如果你要从头构建，就必须记得将每个文件添加到项目中，并且在某些情况下，还必须记得加载 Windows 多媒体库。同样，我们需要构建几个用户定义函数，最后用一个 main 函数来控制这个游戏（根据需要参考前面的章节）。

## 角色动画：飞船动画

为飞船制作动画的关键是跟踪飞船朝向的方向，然后为该方向绘制相应的图像。由于每个玩家都可以转动飞船，我们需要更新飞船的方向（见示例 3.45）。既然我们能够跟踪方向，就需要一个函数来显示该方向对应的合适图像（见示例 3.46）。在示例 3.47 中，你可以看到如何为玩家 1 调用此函数。玩家 2 的代码类似。注意，此函数使用了数组，第 4 章将介绍相关内容。

### 示例 3.45. 飞船角色的方向（AnimatedImage.cs）。

```csharp
// Rotate the direction by the specified amount
// increment is in 45 degree steps
virtual public void RotateDirection(int increment) {
    int result = increment + direction;

    if (result > 8) {
        result %= 8;
        if (result == 0)
            result = 8;
    } else if (result < 1) {
        result = (result % 8) + 8;
    }
    direction = result;
}
```

### 示例 3.46. 显示图形（PlayerImageArray.cs）。

```csharp
// overridden member which displays the image with an index ==
// to the heading associated with the image.
override public void Display(Graphics g) {
    if (direction >= 0 && direction <= aImages.GetLength(0))
    g.DrawImage(aImages[direction], imagePosX, imagePosY,
        imageWidth, imageHeight);
}
```

### 示例 3.47. 绘制玩家 1 的飞船和尾焰的代码

```csharp
player1.Display(g);
if (plEvent.IsActive) {
    exhaustImages[player1.direction].imagePosX =
    player1.imagePosX;
    exhaustImages[player1.direction].imagePosY =
    player1.imagePosY;
    exhaustImages[player1.direction].Display(g);
}
```

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_210_0.png)

> 与飞船图像一样，显示尾焰轨迹只需读取飞船的坐标并显示相应的图像。

## 角色动画：投射物与爆炸

与角色对应部分一样，我们的投射物必须依赖函数和事件的组合，包括激活、动画、碰撞检测和停用。虽然这些属性大多集成在其他函数中，但我们仍然可以基于几行代码定义投射物的行为（见示例 3.48）。

### 示例 3.48. 碰撞检测。

```csharp
public bool CheckShipCollision(Player player) {
    Player opponent = (player == player1) ? player2 : player1;

    // Collided with another ship?
    if (player.Intersects(opponent)) {
        // Successful ramming action!!
        ShipCollided (opponent, player);
        return true;
    }

    // Collided with the sun?
    if (player.Intersects(theSun)) {
        ShipCollided (player, null);
        return true;
    }

    // Asteroid collision?
    if (useAsteroids) {
        for (int i = 0; i < MAX_ASTEROIDS; i++) {
            if (asteroids[i].isActive) {
                if (asteroids[i].Intersects(player)) {
                    ShipCollided (player, null);
                    return true;
                }
            }
        }
    }
}
```

## 添加 DirectInput：键盘和操纵杆

太空中的飞船移动方式与网球场中的人截然不同。因此，可以合理地认为，我们为键盘和操纵杆构建的结构会大不相同。同样重要的是要注意，Space Fighter 不需要使用鼠标；因此，不会包含鼠标应用程序。Space Fighter 确实需要一个推力和两个移动角度，即正 45 度和负 45 度，从而有效地让飞船向左和向右转向。考虑到两艘飞船起始位置不同，并且我们的算法需要通用解决方案，我们得出结论：需要一个抽象的旋转模型（见示例 3.49）。

### 示例 3.49. 键盘和操纵杆控制。

```csharp
private void Keyboard_Tick(object sender, System.EventArgs e) {

    keyboard = new Microsoft.DirectX.DirectInput.Device(SystemGuid.Keyboard);
    keyboard.Properties.BufferSize = 8;
    keyboard.Acquire();

    KeyboardState state = keyboard.GetCurrentKeyboardState();

    for (Key k = Key.Escape; k <= Key.MediaSelect; k++) {
        if (state[k] && k == Key.W) {
            ...
        }

private void Joystick_Tick(object sender, System.EventArgs e) {
    foreach (DeviceInstance instance in
        Manager.GetDevices(DeviceClass.GameControl,
            EnumDevicesFlags.AttachedOnly)) {
        joystick = new Microsoft.DirectX.DirectInput.Device(instance.InstanceGuid);
        break;
    }

    if (joystick == null) {
        return;
    }

    joystick.SetDataFormat (DeviceDataFormat.Joystick);
    foreach (DeviceObjectInstance d in joystick.Objects)
        if ((0 != (d.ObjectId & (int)DeviceObjectTypeFlags.Axis))) {
            d.Properties.SetRange (ParameterHow.ById,
                d.ObjectId, new InputRange(-1000, 1000));
            ...
        }
    joystick.Acquire();
    joystick.Poll();
    State = joystick.CurrentJoystickState;

    if (-600 > State.Y) {
        if (!player2.isActive)
            player2.isActive = true;
            player2.RandomizePosition();
        }

        if (player2.isActive == true) {
            if (-400 < State.X && -600 > State.Y) {
                player2.RotateDirection(1);
            }
            ...
        }

    byte[] buttons = State.GetButtons();
    foreach (byte b in buttons) {
        if (0 != (b & 0x80)) {
            for (int i = 0; i < MAX_MISSILES; i++) {
                if (player2Missiles[i].isActive == false) {
                    FireMissile (player2, player2Missiles);
                    break;
                }
            }
            ...
        }
    }
}
```

当然，我们也可以使用太阳的较小版本来表示飞船燃烧起来的样子（请记住：已被摧毁的飞船不会受到额外武器火力的影响，也不应受到太阳引力的影响）。同样，会结合使用 if 和 switch 语句来减少杂乱。

### OnPaint

我们将重写 Windows 的 OnPaint 方法，以创建一个简单但综合的显示命令列表，这些命令生成游戏的视觉部分。重要的是包含条件命令，以限制/控制飞船和尾焰（它们将是独立实体）的方向，并根据需要显示和/或隐藏小行星。我们将使用 OnPaint 方法显示介绍性文字以及一些背景星星和太阳。（见示例 3.50。）小行星将在本章后面定义。

### 示例 3.50. Space Fighter 图形。

```csharp
// Draw the scores
buffer.ColorFill(Color.Black);
buffer.ForeColor = Color.Red;
buffer.DrawText(4 * SCALE, 2 * SCALE, player1.score.ToString(), false);
buffer.ForeColor = Color.Blue;
buffer.DrawText(16 * SCALE, 2 * SCALE, player2.score.ToString(), false);

// Draw player 1 & its appropriate exhaust
try {
    destination = new Rectangle(player1.imagePosX, player1.imagePosY,
        SCALE, SCALE);
    buffer.Draw(destination, Player1Draw [player1.direction],
        DrawFlags.Wait);
} catch (SurfaceLostException) {
    CreateSurfaces();
    ...
    if (plEvent.IsActive) {
        try {
            int X = player1.imagePosX
                + exhaustImages[player1.direction].imageOffsetX;
            int Y = player1.imagePosY
                + exhaustImages[player1.direction].imageOffsetY;
            destination = new Rectangle(X, Y, SCALE / 2, SCALE / 2);
            buffer.Draw(destination, ExhaustDraw [player1.direction],
                DrawFlags.Wait);
        } catch (SurfaceLostException) {
            CreateSurfaces();
            ....
        }
    }
}
```

## 定义超空间

我们大多数人将世界视为一个四维平台，即 x、y、z 和时间，这在日常生活中对我们很有用。然而，在处理太空旅行的概念时，我们必须考虑穿越第五维（又称超空间）移动的可能性。在
